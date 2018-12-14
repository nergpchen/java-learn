Java动态代理

java动态代理可以用来生成任何接口的任何一个类,可以理解为代码生成工具。

在java中的动态代理的通用代码如下:

Proxy.newProxyInstance\(loader, interfaces, handler\)

通过这个方法来生成一个代理类

 那么怎么实现的呢？

java提供了Proxy这个类，任何代理类都是继承了这个类，所以java代理动态只能支持接口.

我们通过实现 InvocationHandler 接口 实现我们的业务逻辑.



`public static Object newProxyInstance(ClassLoader loader,`

`                                          Class<?>[] interfaces,`

`                                          InvocationHandler h)`

`        throws IllegalArgumentException {`

`        if (h == null) {`

`            throw new NullPointerException();`

`        }`

` `

`        final Class<?>[] intfs = interfaces.clone();`

`        final SecurityManager sm = System.getSecurityManager();`

`        if (sm != null) {`

`            checkProxyAccess(Reflection.getCallerClass(), loader, intfs);`

`        }`

`        // 这里是生成class的地方`

`        Class<?> cl = getProxyClass0(loader, intfs);`

`        // 使用我们实现的InvocationHandler作为参数调用构造方法来获得代理类的实例`

`        try {`

`            final Constructor<?> cons = cl.getConstructor(constructorParams);`

`            final InvocationHandler ih = h;`

`            if (sm != null && ProxyAccessHelper.needsNewInstanceCheck(cl)) {`

`                return AccessController.doPrivileged(new PrivilegedAction<Object>() {`

`                    public Object run() {`

`                        return newInstance(cons, ih);`

`                    }`

`                });`

`            } else {`

`                return newInstance(cons, ih);`

`            }`

`        } catch (NoSuchMethodException e) {`

`            throw new InternalError(e.toString());`

`        }`

`    }`

private static final WeakCache&lt;ClassLoader, Class&lt;?&gt;\[\], Class&lt;?&gt;&gt;

        proxyClassCache = new WeakCache&lt;&gt;\(new KeyFactory\(\), new ProxyClassFactory\(\)\);

--------------------- 



private static final class ProxyClassFactory

        implements BiFunction&lt;ClassLoader, Class&lt;?&gt;\[\], Class&lt;?&gt;&gt; {

        // 所有代理类名字的前缀

        private static final String proxyClassNamePrefix = "$Proxy";

 

        // 用于生成代理类名字的计数器

        private static final AtomicLong nextUniqueNumber = new AtomicLong\(\);

 

        @Override

        public Class&lt;?&gt; apply\(ClassLoader loader, Class&lt;?&gt;\[\] interfaces\) {

            // 省略验证代理接口的代码……

 

            String proxyPkg = null;     // 生成的代理类的包名

            // 对于非公共接口，代理类的包名与接口的相同

            for \(Class&lt;?&gt; intf : interfaces\) {

                int flags = intf.getModifiers\(\);

                if \(!Modifier.isPublic\(flags\)\) {

                    String name = intf.getName\(\);

                    int n = name.lastIndexOf\('.'\);

                    String pkg = \(\(n == -1\) ? "" : name.substring\(0, n + 1\)\);

                    if \(proxyPkg == null\) {

                        proxyPkg = pkg;

                    } else if \(!pkg.equals\(proxyPkg\)\) {

                        throw new IllegalArgumentException\(

                            "non-public interfaces from different packages"\);

                    }

                }

            }

 

            // 对于公共接口的包名，默认为com.sun.proxy

            if \(proxyPkg == null\) {

                proxyPkg = ReflectUtil.PROXY\_PACKAGE + ".";

            }

 

            // 获取计数

            long num = nextUniqueNumber.getAndIncrement\(\);

            // 默认情况下，代理类的完全限定名为：com.sun.proxy.$Proxy0，com.sun.proxy.$Proxy1……依次递增

            String proxyName = proxyPkg + proxyClassNamePrefix + num;

 

            // 这里才是真正的生成代理类的字节码的地方

            byte\[\] proxyClassFile = ProxyGenerator.generateProxyClass\(

                proxyName, interfaces\);

            try {

                // 根据二进制字节码返回相应的Class实例

                return defineClass0\(loader, proxyName,

                                    proxyClassFile, 0, proxyClassFile.length\);

            } catch \(ClassFormatError e\) {

                throw new IllegalArgumentException\(e.toString\(\)\);

            }

        }

    }



--------------------- 

引用:https://blog.csdn.net/mhmyqn/article/details/48474815

