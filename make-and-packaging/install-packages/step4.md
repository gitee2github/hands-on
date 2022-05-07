在本章前面的几节内容中，我们已经了解到了如何使用 `Tarball`、`RPM` 以及 `DNF` 来安装软件。在本节我们将学习如何创建一个简单的RPM软件包。

RPM软件包使用 `rpmbuild` 工具进行制作，工具初始化完成后，会在当前用户的家目录下创建相应的工作目录(以root用户为例)：

- `/root/rpmbuild/SPECS/`：该软件的配置文件，例如软件的信息参数、设置项目等
- `/root/rpmbuild/SOURCES/`：软件的原始文件（*.tar.gz 的文件） 以及 config 配置文件
- `/root/rpmbuild/BUILD/`：在编译过程中，有些暂存的数据都会放置在该目录中
- `/root/rpmbuild/RPMS/`：经过编译之后，并且顺利编译成功之后，将打包完成的文件放在该目录中，包含了 x86_64，noarch... 等的次要目录
- `/root/rpmbuild/SRPMS/`：与 RPMS 目录相似，放置的是 SRPM 封装的文件

在开始制作的过程前，我们需要做的是：
1. 将源码文件放置到 `/root/rpmbuild/SOURCES/` 目录中
2. 编写 `*.spec` 文件并放置到 `/root/rpmbuild/SPECS/` 目录中

SPEC文件是指导 `rpmbuild` 工作的配置文件，通常包含了该软件包的名称、版本、开源协议等相关信息以及构建各环节的脚本等配置：

- `Summary`：软件的主要说明
- `Name`：软件的名称（最终会是 RPM 文件的名称构成之一）
- `Version`：软件的版本（也是 RPM 文件名构成之一）
- `Release`：该版本打包的次数说明（也是 RPM 文件名构成之一）。
- `License`：软件的授权模式，看起来涵盖了所有知名的 Open source 授权
- `URL`：源码的主要官网
- `SourceN`：软件的来源，如果是网络上下载的软件，通常这里一定会有这个信息来告诉大家这个原始文件的来源，此外，如果有多个软件来源，则会以 Source0、Source1... 开处理源码
- `PatchN`：作为补丁的 patch file，也是可以有多个
- `BuildRoot`：作为编译时，该使用哪个目录来暂存中间文件（如果编译过程的目标文件、链接文件等）
上述信息为必须存在的项目，下面的则为可使用的额外设置
- `Requires`：如果这个软件运行时还需要其他的软件支持，就必须配置，则当你制作成 RPM 后，系统就会自动去检查，这就是软件依赖的来源
- `BuildRequires`：编译过程中所需要的软件。Requires 指的是安装时需要检查，因为与实际运行有关，而 BuildRequires 则是 编译时 所需要的软件，只有在 SRPM 编译为 RPM 时才会检查的项目

对于软件构建的脚本控制则位于指定的宏定义后：

- `%description`: 将你的软件做一个简短的说明，这个也是必须的，在使用 rpm -qi 软件名称 出现的一些基础说明就包括这里的设置信息

- `%prep` 尚未进行设置或安装之前，你要编译完成的 RPM 帮你实现做的事情，就是 prepare 的简写，它的主要任务可以包括：
    - 进行软件的补丁（patch）等相关工作
    - 寻找软件所需要的目录是否已经存在

- `%build`: 该段落在配置 make 编译称为可执行的程序。会发现在此部分的程序代码，就是 ./configure,make 等命令。

- `%install`: 编译完成后，就要安装了，也就是类似 Tarball 里面的 make install

- `%files`: 这个软件安装的文件都需要写到这里来，也包括目录，以备查验用。此外也可以指定每个文件的类型，包括帮助文件（%doc 后面接的文件）与配置文件 %config 后面接的文件

- `%changelog`: 主要记录该软件曾经的更新记录，星号 * 后面应该要以时间、修改者、email 与软件版本来作为说明，减号 - 后面则是你详细的说明。

## 任务

1. 执行 `[[sudo rpm -e anglerpm-0.1-1.x86_64.rpm]]{{RUN}}` 卸载上一节中完成安装的软件。

2. 执行 `[[mkdir -p /home/coder/rpmbuild/SOURCES/ && cd /home/coder/rpmbuild/SOURCES/ && wget https://github.com/opensourceways/playground-courses/releases/download/v0.1/anglerpm-0.1.tar.gz]]{{RUN}}` 下载Tarball软件包并放置到 `SOURCES` 目录下。

3. 执行 `[[mkdir -p /home/coder/rpmbuild/SPECS/ && cd /home/coder/rpmbuild/SPECS/ && vi anglerpm.spec]]{{RUN}}` 创建并开始编辑spec文件。

4. 按照以下内容编辑 `anglerpm.spec`, 其中`changelog`部分请根据实际情况填写 :
    ```
    Name: anglerpm
    Version: 0.1
    Release: 1%{?dist}
    Summary: Get your name and show sin and cos value.

    Group: Scientific Support
    License: GPLv2
    URL: http:/playground.openeuler.org/
    Source0: anglerpm-0.1.tar.gz

    # BuildRequires:

    %description
    This package will let you input your name and calculate sin cos value

    %prep
    %setup -q


    %build
    ./configure
    make

    %install
    mkdir -p %{buildroot}/usr/local/bin
    install -m 755 anglerpm %{buildroot}/usr/local/bin

    %files
    /usr/local/bin/anglerpm

    %changelog
    * Mon Feb 14 2022 openEuler Playground <playground@openeuler.org> - 0.1
    - Build the program & Happy Valentine's Day

    ```

5. 执行 `[[rpmbuild -ba anglerpm.spec]]{{RUN}}` 开始制作rpm软件包

6. 执行 `[[cd /home/coder/rpmbuild/RPMS/x86_64 && ls -l]]{{RUN}}` 进入到生成目录并查看内容。

7. 执行 `[[sudo rpm -i anglerpm-0.1-1.x86_64.rpm]]{{RUN}}` 尝试安装新构建完成的rpm软件包。

8. 执行 `[[anglerpm]]{{RUN}}` 运行并与程序交互。

## Tips

更多有关 `rpmbuild` 的详细内容请参考：https://rpm-software-management.github.io/rpm/manual/ 

