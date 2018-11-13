### 3.1 标记-清除算法

算法分为“标记”和“清除”阶段：首先标记出所有需要回收的对象，在标记完成后统一回收所有被标记的对象。它是最基础的收集算法，会带来两个明显的问题；1：效率问题和2：空间问题（标记清除后会产生大量不连续的碎片）![](https://mmbiz.qpic.cn/mmbiz_png/hvUCbRic69sDOMkMYwE1nhEJFZN46xicicaw1iaSkaHmorye79qTka8Ew8mY4zkvG80Dx4DgdxpwX6osZZQ13bgC4g/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

### 3.2 复制算法

为了解决效率问题，“复制”收集算法出现了。它可以将内存分为大小相同的两块，每次使用其中的一块。当这一块的内存使用完后，就将还存活的对象复制到另一块去，然后再把使用的空间一次清理掉。这样就使每次的内存回收都是对内存区间的一半进行回收。

![](https://mmbiz.qpic.cn/mmbiz_png/hvUCbRic69sDOMkMYwE1nhEJFZN46xicicaSia9w6GX34d7VYicWgyec1wiaF47ibicvibkLZBfn6XVvibcnI6XMZaw2ZBCw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



引用:[https://mp.weixin.qq.com/s?\_\_biz=MzU4NDQ4MzU5OA==&mid=2247483914&idx=1&sn=9aa157d4a1570962c39783cdeec7e539&chksm=fd98546bcaefdd7d9f61cd356e5584e56b64e234c3a403ed93cb6d4dde07a505e3000fd0c427&scene=21\#wechat\_redirect](https://mp.weixin.qq.com/s?__biz=MzU4NDQ4MzU5OA==&mid=2247483914&idx=1&sn=9aa157d4a1570962c39783cdeec7e539&chksm=fd98546bcaefdd7d9f61cd356e5584e56b64e234c3a403ed93cb6d4dde07a505e3000fd0c427&scene=21#wechat_redirect)

