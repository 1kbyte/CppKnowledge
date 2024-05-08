# CMake相关
(待完善)

创建出build目录，在build目录中，有vs的sln文件，使用vs进行后续的编译即可。    
注：build目录为生成目录，不要在目录放置任何有用的文件。     

有安装多个VS的场景下，可以指定使用哪一个版本的

```
set(CMAKE_CXX_STANDARD 11) # 设置使用的C++版本

option(ENABLE_XXX "Enable XXX" ON) # CMake参数，可以在执行cmake指令时，通过 cmake -DENABLE_XXX=ON/OFF 指定该值

find_package(Git QUIET)
if(GIT_FOUND)
  execute_process(
    COMMAND ${GIT_EXECUTABLE} rev-parse --short=7 HEAD
    OUTPUT_VARIABLE COMMIT_HASH
    OUTPUT_STRIP_TRAILING_WHITESPACE
    ERROR_QUIET
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR})
endif()
```

