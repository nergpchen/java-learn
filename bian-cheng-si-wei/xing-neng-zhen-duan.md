常用命令:

1.找繁忙线程时，top -h , 再jstack， 再换算tid比较累，而且jstack会造成停顿。

推荐用vjtools里的vjtop, 不断显示繁忙的javaj线程，不造成停顿。

2.还可以用火焰图来辅助使用分析



