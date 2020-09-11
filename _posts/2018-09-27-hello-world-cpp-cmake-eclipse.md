---
title: "Hello World C++ application setup using CMake for Eclipse IDE"
excerpt: "Configuring a simple Hello World C++ project using CMake Builder for Eclipse IDE."

header:
  teaser: post_hw_cpp/header_image.png
  alt: "Hello World C++ Project Setup teaser image"
  caption: "Hello World C++ Project"

categories:
  - tutorials

tags:
  - C++
  - CMake
  - Project
---

## Introduction

This is my first blog post. So I ll be presenting a simple introduction to C++ project developement.
Let us create a simple `Hello World` application in C++.

<!-- img_1 - HelloWorld C++ Project Setup in Eclipse IDE screenshot -->
![Hello World C++ Project Setup in Eclipse IDE][img_helloworld_C++_project_eclipse_ide]

## Info

| Tools        | Version                |
| ------------ | ---------------------- |
| OS           | Ubuntu 16.04           |
| CPU          | x86_64                 |
| Builder      | cmake 3.8.0            |
| Compiler     | g++ 5.4.0              |
| IDE / Editor | Eclipse, Vim & VS Code |
| Languages    | C++, CMake             |

<p>
{%- if page.show_ads -%}
  {%- include ads.html ad_src="google-adsense" ad_type="in-article" -%}
{%- endif -%}
</p>

## Instructions

1. First we create a folder to host the project files such as header files, source files and the build system files. This is called the source folder `HelloWorld` *(it is recommended to avoid spaces in file and folder names)* as it hosts only the source files.
2. We create another folder to host the build results files such as the object files, compiled files and binaries. This is called build folder `build`.
3. For convenience sake we create a top level folder `HelloWorld_top` to host the source and build folders. This type of project structure is useful to separate the source code from the build files and hence has many advantages which I'll be writing about in the following blog posts.
4. Combining the above 3 steps we get a folder structure as:
   ```
   |-- HelloWorld_top
       |-- build
       |-- HelloWorld
   ```
5. Go to source folder `HelloWorld` and create folder to host:
   1. Header files `inc`, i.e. *.h, *.hpp files
   2. Source files `src`, i.e. *.c, *.C++ files
   3. Test files `test`, i.e. test code required for testing the source files.
   4. Document files `doc`, i.e. *.dox, *.rst to store the documentation for the code. Will be used in bigger project for automatic generation of documents in various popular file formats such as PDF, HTML.
   5. Data files `data`, i.e. any data required for building/testing the application such as the images, icons etc. Not applicable here [small projects], will be used in bigger projects.
   6. Utility files `util`, i.e. bash scripts, python scripts to automate or simplify the redundant tasks such as creating the folders for above steps.  
   Now the source folder `HelloWorld` structure is as follows:
   ```
   |-- HelloWorld
       |-- data
       |-- doc
       |-- inc
       |-- src
       |-- test
       |-- util
   ```
6. Write the code for `HelloWorld` project as in the github repo: [HelloWorld][1]
7. Now go to the `build` folder.
   Use the below [cmake][2] command to generate the build files along with the [Eclipse CDT][3] project files. For bigger projects it is recommended to use an IDE like [Eclipse][4], [CLion][5] or [VS Studio][6]. Please read [CMake documentations][7] to understand the below command in depth.
   ```cmake
   cmake -G"Eclipse CDT4 - Unix Makefiles"\
       -DCMAKE_ECLIPSE_GENERATE_SOURCE_PROJECT=TRUE\
       -DCMAKE_BUILD_TYPE=Debug\
       -DCMAKE_CXX_FLAGS="-std=c++11"\
       -DCMAKE_CXX_COMPILER_ARG1=-std=c++11
   ```
   It generates the project build files, we can then build the application using a system specific builder such as [Make][8] for Linux system or [NMake][9] for Windows system

## Summary

1. That was a rough explanation of how I setup my projects in C++.
2. I will explain the reason behind the project structure, choice of tools used, code style and many more things in my future posts.
3. It is definitely not an entry level tutorial it is for professional programmers with at-least 1 year of work experience.
4. I have more ideas to share in the future posts all of them follow the same project structure, coding style and tools. Hence this introductory post. Stay tuned and follow me on social medias in my bio.
5. Thank you, for reading. Please leave a comment below or use one of the social media links from my bio.

{% capture note %}

## Note

- This blog post is about **Hello World project** in C++ not a program that can be written in a single file.
- The intent of this post is to give you an idea of how to setup a C++ project with CMake for Eclipse IDE.
- This post assumes that you already know programming and have experience in creating, debugging and executing
  programs in any modern languages such as C, C++, C#, Java or Python.

{% endcapture %}
<div class="bg-warning p-3">{{ note | markdownify }}</div>

<!-- images in the post -->
[img_helloworld_C++_project_eclipse_ide]: {{ site.url }}{{ site.baseurl }}/assets/images/post_hw_cpp/helloworld_cpp.png  "Hello World C++ Project in Eclipse IDE"

<!-- Links in the post -->
[1]: https://github.com/manid2/HelloWorld.git
[2]: https://cmake.org/
[3]: https://www.eclipse.org/cdt/
[4]: https://www.eclipse.org/
[5]: https://www.jetbrains.com/clion/
[6]: https://visualstudio.microsoft.com/
[7]: https://cmake.org/documentation/
[8]: https://www.gnu.org/software/make/
[9]: https://docs.microsoft.com/en-us/cpp/build/nmake-reference?view=vs-2017