关于gcc对字符集的支持

	1. 代码文件的字符集A
	2. gcc内部处理的字符集B（UTF-8）
	3. gcc输出的二进制文件的字符集C（默认是UTF-8，可以使用-fexec-charset选项进行指定）

	具体来说，当我们运用gcc命令将代码文件进行编译，它就直接认为代码文件的字符集是finput-charset选项中所指定的字符集（默认是utf-8），
	也就是说他也许根本就不知道你的字符集是字符集A。他根据finput-charset选项中的字符集向自己的内部所使用的字符集B进行转码。
	经过编译之后，就再次将二进制输出从内部字符集B转为字符集C。图示为，
