# vs2017跨平台开发

#配置 visual studio

Tools/Options/Cross Platform
add host name port username password

# vs c/c++ for linux多项目开发

## 新建linux启动项目

新建项目>跨平台>linux>控制台linux程序

(这个设置为启动项目)

## 新建库项目

右键 解决方案"{$project_name}" > 添加 > 新建项目 > 跨平台 > linux> 空项目

## 属性选项配置

1. 配置主程序

```
本地输出目录："$(ProjectDir)bin\$(Platform)\$(Configuration)\"修改为"$(ProjectDir)..\bin\$(Platform)\$(Configuration)\"，是为了将所有项目输出文件放到同一个目录中，方便相互引用。

目标文件扩展名：".out"修改为""，是为了不生成文件后缀，一般的Linux可执行程序是没有扩展名称的，可修改也可不修改。

远程生成根目录："~/projects"修改为"/home/username/projects/$(SolutionName)"，"~"和"/root"是等价的，但是运行时动态库搜索目录不支持~路径，添加“$(SolutionName)”是为了区分不同的解决方案下相同名称的项目。
```

2. 配置动态库：```"$(RemoteRootDir)/$(ProjectName)"```

```
本地输出目录："$(ProjectDir)bin\$(Platform)\$(Configuration)\"修改为"$(ProjectDir)..\bin\$(Platform)\$(Configuration)\"

目标文件扩展名：".out"修改为".so"

远程生成根目录："~/projects"修改为"/root/projects/$(SolutionName)"

配置类型："应用程序(.out)"修改为"动态库(.so)"
```

3. 配置静态库

```
本地输出目录："$(ProjectDir)bin\$(Platform)\$(Configuration)\"修改为"$(ProjectDir)..\bin\$(Platform)\$(Configuration)\"

目标文件扩展名：".out"修改为".a"

远程生成根目录："~/projects"修改为"/root/projects/$(SolutionName)"

配置类型："应用程序(.out)"修改为"动态库(.a)"
```

## 调试配置
```
程序："$(RemoteTargetPath)"修改为"$(RemoteRootDir)/bin/$(Platform)/$(Configuration)/$(TargetName)$(TargetExt)"，因为前面修改了本地输出目录导致远程输出目录也相应发生变化，这里修改一致。

工作目录："$(RemoteOutDir)"修改为"$(RemoteRootDir)/bin/$(Platform)/$(Configuration)"，这个是远程主机CentOS上的路径，如果设置不正确将找不到引用的动态库，调试程序无法启动。

其他调试程序命令：""修改为"set solib-search-path $(SolutionDir)bin/$(Platform)/$(Configuration)"，这个是本地路径，调试符号是从本地加载的，否则调试动态库时，gdb会输出没有找到调试符号文件。
```

## "C/C++"配置
***这一步可以省略***
```
附加包含目录：在"$(StlIncludeDirectories);%(AdditionalIncludeDirectories)"前面添加"./..;"，这个是远程主机CentOS上的路径，相当于gcc编译时指定"-I[路径]"选项；一般是先把需要的头文件从CentOS复制到windows，然后设置"配置属性"->"VC+ +目录"->"包含目录"，这样在编写Linux程序时，提示信息更加的友好^^。
```

## "链接器"配置

```
附加库目录：在"%(AdditionalLibraryDirectories)"前面添加"$(RemoteRootDir)/bin/$(Platform)/$(Configuration);"，这个是远程主机CentOS上的路径，相当于gcc编译时指定"-L[路径]"选项，用于指定引用动态库和静态库的目录；

库依赖项：添加"dynamic_library;static_library"，相当于gcc设置"-l[库名称]"选项，用于指定链接时所需要的动态库和静态库名称，如果找不到依赖的库文件，链接时会错误，显示"无法解析的符号"。

其他选项：添加"-Wl,-rpath=$(RemoteRootDir)/bin/$(Platform)/$(Configuration) "，指定程序运行时搜索动态库的路径。
```
