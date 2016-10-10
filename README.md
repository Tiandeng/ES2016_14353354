# DOL开发环境配置 #
## 一.Description ##
Distributed operation layer (DOL) is a software development framework to program parallel applications. The DOL allows to specify applications based on the Kahn process network model of computation and features a simulation engine based on SystemC. Moreover, the DOL provides an XML-based specification format to describe the implementation of a parallel application on a multi-processor systems, including binding and mapping.
## 二.How To Install ##
- 安装必要的环境

		1. $ sudo apt-get update
		2. $ sudo apt-get install ant
		3. $ sudo apt-get install openjdk-7-jdk
		4. $ sudo apt-get install unzip

- 下载文件

		1. $ sudo wget http://www.accellera.org/images/downloads/standards/systemc/systemc-2.3.1.tgz
		2. $ sudo wget http://www.tik.ee.ethz.ch/~shapes/downloads/dol_ethz.zip
- 解压文件
	1. 新建dol的文件夹

			1. $ mkdir dol
	2. 将dolethz.zip解压到 dol文件夹中

			1. $ unzip dol_ethz.zip -d dol
	3. 解压systemc

			1. $ tar -zxvf systemc-2.3.1.tgz
- 编译systemc
	1. 解压后进入systemc-2.3.1的目录下

			1. $ cd systemc-2.3.1
	2. 新建一个临时文件夹objdir

			1. $ mkdir objdir
	3. 进入该文件夹objdir

			1. $ cd objdir
	4. 运行configure(能根据系统的环境设置一下参数，用于编译)


			1. $	../configure CXX=g++ --disable-async-updates

		下图为运行configure之后的截图 

		![](http://p1.bpimg.com/567571/28262e0db67de54a.jpg)
	5. 编译

			1. $ sudo make install

		编译完后文件目录如下($cd .. $ls) 

		![](http://p1.bpimg.com/567571/6e7c75af10274f50.jpg)

	6. 记录当前的工作路径（会输出当前所在路径，记下来，待会有用）

			1. $ pwd
		编译完后文件目录如下($cd .. $ls) 

		![](http://p1.bpimg.com/567571/953cb81b9f26422b.jpg)

		这里表示我当前的工作路径为 /root/systemc-2.3.1
- 编译dol
	1. 进入刚刚dol的文件夹

			1. $ cd ../dol
	2. 修改build_zip.xml文件

			1. 找到下面这段话，就是说上面编译的systemc位置在哪里，propertyname="systemc.inc"value="YYY/include"/><property name="systemc.lib" alue="YYY/lib-linux/libsystemc.a"/>
			2. 把YYY改成上页pwd的结果（注意，对于  64位 系统的机器，lib-linux要改成lib-linux64）
	3. 然后是编译
 
			1. $ ant -f build_zip.xml all	若成功会显示build successful
	4. 接着可以试试运行第一个例子进入build/bin/mian路径下

			1. $ cd build/bin/main

	5. 然后运行第一个例子


			1. $ ant -f runexample.xml -Dnumber=1

		成功结果如图

		![](http://p1.bpimg.com/567571/56e4402c7e18c07f.jpg)
## 二.Experimental experience ##
1. 这次配置中虽然有ubuntuX64位的配置方法，但是推荐用32位的，因为我和身边同学的亲身经历发现64位总是出现奇怪的问题导致出错。
2. 我在配置时出现了解压无法进行的情况，检查发现我的ubuntu开始没有安装解压工具。我一直按照步骤在进行，不理解为什么会出现这个问题。但通过这些问题我明白了，就算给出讲解和步骤，实际操作还是会有问题发生。这就要我们灵活应对了。比如查博客，问同学。
3. 总的这次试验不是很困难，毕竟TA很贴心的给出了详细的配置方案。按照步骤来选择32位ubuntu基本都能一次过。
