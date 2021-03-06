## <b>Position-independent-cod PIC</b> ##

1. fPIC 作用于编译阶段，告诉编译器产生与位置无关代码。作用: 动态库可以加载在内存任意位置。
2. fPIC 使用与位置无关的相对地址,通过GOT全局偏移量表实现。
3. 不加-fPIC,加载.so文件的代码段时,代码段引用的数据对象需要重定位修改代码段的内容,造成每个使用这个.so的进程在内核里都会生成这个.so文件代码段的copy。
4. 从GCC来看，shared应该是包含fPIC选项的，但似乎不是所以系统都支持，所以最好显式加上fPIC选项。
5. 目的/需求：节省内存使用

## <b>Position-independent-exec PIE</b> ##
1. PIE: 应用程序代码段数据段加载进内存的位置不固定. 版本：内核2.6以上.
2. 目的/需求：安全, 提供ASLR(Address Space Layout Randomization,地址空间分布随机化)机制
3. 兼容问题：与某些32位库混编时会导致，莫名其妙的段错误。原因是：程序的指针地址会一会是64位，过一会又变成32位
4. 小技巧：查看程序运行时的内存分配 cat /proc/pid/maps
5. ELF类型：DYNAMIC. 
6. 小细节：编译参数要加-fpie，链接参数要加-pie
