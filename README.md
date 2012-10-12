kmemcache
=========

实现在内核空间内的Cache系统
[优点]
1. 更多的代码优化。工作在内核空间，性能会尽量做到最优化。如果性能不够，就继续优化。
2. 基于VFS，底层会实现成一个文件系统，如果需要支持永久化Cache功能，则是一个Cache的文件系统，否则就是一个类似于procfs的虚拟化文件系统，或者采用混合模式，内存超过预期配置则使用本地磁盘，如SSD等。
3. 文件系统天生的继承关系可以用来实现分namespace，ACL控制
4. 更好的状态信息，如访问时间，最后修改时间等等，还可以通过扩展属性支持更多的功能。
5. 动态扩容

[缺陷]
1. 以Linux模块的方式发布，自然不能做到跨多平台了。
2. 工作在内核空间内，如有Bug后果将会非常严重，当然，必须对代码的质量进行保证。
3. 安装过程可能略显麻烦，当然熟悉的人自然不会觉得麻烦。

[计划中更多的Feature列表]
1. 分布式的支持


[发布与使用]
发布包括kmemcachefs模块，以及kmemcache-progs两个包。

...
mkdir /kmemcache
mount -t kmemcachefs /dev/loop0 /kmemcache
...

[预览版的功能列表]
1. 最小化的基本的文件virtual fs结构


[客户端代码实例]

[php]
$cache_server = KMemcache::Connect("127.0.0.1", 32268, username, passwd);
$a = $cache_server->NewCache("/infrastructure/production1/p2/lines");
$a->set(1000);
var_dump($a->get());
[/php]



