# TODO 14: Remove mysqrt.cxx from the list of sources

# TODO 1: Add a library called MathFunctions with sources MathFunctions.cxx
# and mysqrt.cxx
# Hint: You will need the add_library command
add_library(MathFunctions MathFunctions.cxx mysqrt.cxx)

# TODO 7: Create a variable USE_MYMATH using option and set default to ON
option(USE_MYMATH "Use tutorial provided math implementation" ON) 

# TODO 8: If USE_MYMATH is ON, use target_compile_definitions to pass
# USE_MYMATH as a precompiled definition to our source files
if(${USE_MYMATH})
    # 这个命令将在编译 MathFunctions 时，向编译器传递 -DUSE_MYMATH 选项
    # 相当于在源代码中添加了 #define USE_MYMATH
    # 这个宏的定义将影响 MathFunctions 库中的源代码文件的编译过程。
    target_compile_definitions(MathFunctions PUBLIC "USE_MYMATH")
endif()


# TODO 12: When USE_MYMATH is ON, add a library for SqrtLibrary with
# source mysqrt.cxx

# TODO 13: When USE_MYMATH is ON, link SqrtLibrary to the MathFunctions Library
