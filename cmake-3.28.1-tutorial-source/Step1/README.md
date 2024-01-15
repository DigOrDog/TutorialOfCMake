# 知识点
CMake的基本语法、命令和变量

# 教程

## 练习 1 - 构建基本项目
### 目标
了解如何创建一个简单的 CMake 项目。
### 前置知识介绍
最基本的 CMake 项目是从单个源代码文件构建的可执行文件。对于这样的简单项目，只需要一个包含三个命令的 CMakeLists.txt 文件。

注意：虽然 CMake 支持大写、小写和混合大小写的命令，但在本教程中，我们更倾向于使用小写命令。

任何项目的顶级 CMakeLists.txt 文件都必须通过使用 cmake_minimum_required() 命令指定最低 CMake 版本。这会建立策略设置，并确保以下 CMake 函数在兼容版本的 CMake 上运行。

为了启动一个项目，我们使用 project() 命令来设置项目名称。此调用在每个项目中都是必需的，并且应该在 cmake_minimum_required() 之后尽早调用。正如我们稍后将看到的，此命令还可用于指定其他项目级信息，如语言或版本号。

最后，add_executable() 命令告诉 CMake 使用指定的源代码文件创建一个可执行文件。

### cmake命令
> add_executable()  
> cmake_minimum_required()  
> project()

### 总结
对于一个只使用标准函数库的项目，即可以简单地使用clang++ main.cpp -o main的项目，编写的CMakeLists.txt只需要包含三条命令就行。第一个命令是cmake_minimum_required() ，指定最低 CMake 版本。第二个命令是 project()，设置项目名称，（不过这块我还不是特别明白有什么用？难道是为了给其他模块引用？。第三个命令是add_executable() ，告诉 CMake 使用指定的源代码文件创建一个可执行文件。

## 练习 2 - 指定 C++ 标准

### 目标
添加需要 C++11 的功能。

### 前置知识
CMake 具有一些特殊变量，这些变量在幕后被创建，或者在由项目代码设置时对 CMake 有意义。其中许多变量以 CMAKE_ 开头。在为项目创建变量时，请避免使用这种命名约定。其中两个特殊的用户可设置变量是 CMAKE_CXX_STANDARD 和 CMAKE_CXX_STANDARD_REQUIRED。可以将它们一起使用来指定构建项目所需的 C++ 标准。

### CMake变量以及命令
> CMAKE_CXX_STANDARD  
> CMAKE_CXX_STANDARD_REQUIRED  
> set()

### 总结
在CMake中，可以通过set进行变量的设置，但是注意不要与CMake内置变量名有冲突


## 练习 3 - 添加版本号和配置头文件

### 目标
定义并报告项目的版本号。

### 前置知识
有时，在 CMakelists.txt 文件中定义的变量也希望在源代码中使用。在这种情况下，我们想要打印项目的版本号。

实现这一目标的一种方法是使用一个配置好的头文件。我们创建一个输入文件，其中包含一个或多个要替换的变量。这些变量具有特殊的语法，看起来像 @VAR@。然后，我们使用 configure_file() 命令将输入文件复制到给定的输出文件，并在 CMakelists.txt 文件中用 VAR 的当前值替换这些变量。

虽然我们可以直接在源代码中编辑版本，但使用此功能更可取，因为它创建了一个单一的真相来源并避免了重复。

### CMake变量
> \<PROJECT-NAME>_VERSION_MAJOR  
> \<PROJECT-NAME>_VERSION_MINOR  
> configure_file()  
> target_include_directories()  

### 总结
代码中如果想要使用CMakelists.txt中定义的变量，那么就需要使用configure_file()命令，然后将input文件中的@var@或者${var}替换成cmake中指定的值。  
可执行文件如果需要引入某个头文件，那么就需要使用target_include_directories()来把对应的文件加进去。

