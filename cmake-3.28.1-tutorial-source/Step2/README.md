# 知识点
学习如何在项目中创建和使用库。我们还将看到如何使我们的库的使用成为可选的。

# 教程

## 练习 1 - 创建一个库
### 目标
添加并使用一个库。

### 前置知识介绍
要在 CMake 中添加一个库，使用 add_library() 命令并指定哪些源文件应组成库。

与将所有源文件放在一个目录中不同，我们可以通过一个或多个子目录来组织我们的项目。在这种情况下，我们将创建一个专门用于我们的库的子目录。在这里，我们可以添加一个新的 CMakeLists.txt 文件和一个或多个源文件。在顶层 CMakeLists.txt 文件中，我们将使用 add_subdirectory() 命令将子目录添加到构建中。

一旦库被创建，它就会通过 target_include_directories() 和 target_link_libraries() 与我们的可执行目标连接。

### cmake命令
> add_library()  
> add_subdirectory()  
> target_include_directories()  
> target_link_libraries()  
> PROJECT_SOURCE_DIR  

### 总结
当存在不只一个CMakelists.txt的时候，可以考虑使用add_subdirectory() 来添加子目录，使得子目录的CMakelists.txt都可以构建  
组成库：在 CMake 中添加一个库的时候，可以使用 add_library() 命令并指定哪些源文件应组成库。 
使用库：target_link_libraries使得库与目标可执行文件进行了链接，target_include_directories可以指明去哪里找头文件  
PROJECT_SOURCE_DIR，目前我对它的理解就是声明project()的CMakelist.txt位置

## 练习 2 - 添加一个选项
### 目标
在 MathFunctions 库中添加一个选项，允许开发人员选择是使用自定义平方根实现还是使用内置的标准实现。

### 前置知识介绍
现在，让我们在 MathFunctions 库中添加一个选项，允许开发人员选择是使用自定义平方根实现还是使用内置的标准实现。虽然在教程中实际上没有必要这样做，但对于更大的项目，这是一个常见的情况。

CMake 可以使用 option() 命令来实现这一点。这为用户提供了一个变量，他们可以在配置其 CMake 构建时更改。此设置将存储在缓存中，以便用户无需每次在构建目录上运行 CMake 时都设置该值。

### cmake命令
> if()  
> option()  
> target_compile_definitions()

### 总结
1.在MathFunctions/CMakeLists.txt中使用option()命令定义一个变量USE_MYMAT，使得这个变量后续可以控制是使用自定义的平方根实现还是使用内置的标准实现。  
2.在方法实现的源代码中引入USE_MYMAT(#ifdef USE_MYMAT)，来控制是使用自定义的平方根实现还是使用内置的标准实现。  


