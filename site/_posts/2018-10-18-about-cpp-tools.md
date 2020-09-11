---
title: "About popular tools used in C++ project development"
excerpt: "Short notes on popular tools used in C++ Project development. \
          Eclipse IDE, CMake and Linux."

header:
#  image: /assets/images/post_cpp_coding_1/header_image.png
  teaser: post_about_cpp_tools/header_image.png
  alt: "About popular C++ tools teaser image"
  caption: "About popular C++ tools"

categories:
  - notes

tags:
  - C++
  - Build
  - Make
  - CMake
  - IDE
  - Editor
  - Project
---

## Preface

Following my first blog post on [Hello World][1] application in C++,
I felt the need to explain about the tools I use for C++ projects.
I am using Ubuntu 16.04 LTS 64bit OS. Because Ubuntu is the most popular OS for personal computers. Easy to install and easy to use. But its not the focus of this article. I want to explain the C++ build tool and the IDE.

## Build process

The process of converting the source files into executables or libraries is called the <span style="color:green">build</span> step. Usually in school or competitive programming we dont focus on the Software Development. We focus on coding, data structures and algorithms, mathematics and everything we need for creating the source code. I have unintentionally ignored how to convert the plain text files (i.e. source code) into object files and link them to create an executable. Because I saw it as a trivial step in coding. It is ok for the projects with a few files like 5 or 10 source files as in the case of most college projects. When the number of source files increase to 1,000 or 10,000 with different executables or object archives to build then it will be quite hard and time consuming to do one by one. Hence we write a script to execute the build step for each binary and also to do some additional tasks like generating the documentation files, running the unit tests and creating the package for the software. This is accomplished by using a <span style="color:green">build tool</span>.

<p>
{%- if page.show_ads -%}
  {%- include ads.html ad_src="google-adsense" ad_type="in-article" -%}
{%- endif -%}
</p>

## Tools

### Make

Make is a build automation tool that builds executable programs and libraries from the source code by reading a set of rules defined in a special file called <span style="color:#ff3300">Makefile</span> which tell how to build each binary.
When we develop a C++ project for Linux OS and have no plans to use the same project for any other platform then writing the build script in Makefile directly is a good option. But if we decide to deploy our software for other platforms then we might need to write the build script for that build systems. It will be quite hard and impractical when we can make use of a program that generates the build script for any OS. CMake is one such tool and it is the most popular one.

### CMake

The process of <span style="color:#0052cc">compiling</span>, <span style="color:green">building</span> and <span style="color:#ff3300">running tests</span> are same on each platform except for the tools being used. These tools are commonly [Make][2] for Linux and [NMake][3] for Windows Visual C++ based development. These two are not compatible. When we do not know about the target user's build system we can not write the build script. We need a tool to generate the target user's build script. This step is taken care by the [CMake][4]. CMake is a build script generator i.e. it generates the Makefiles. It detects the target user's OS and it's compiler, and then it generates the build script which is compatible with that OS and the compiler.

It is used by many popular open source projects such as the [OpenCV][5], [Google Test][6]. I got introduced to CMake when learning OpenCV for my image processing projects. As we know OpenCV is a multi-platform image processing and computer vision library, it achieves building on multiple platforms using CMake. I have spent a considerable amount of time trying to understand how OpenCV software is built, tested, packaged and deployed. It is quite fascinating that all these steps in OpenCV are automated. Human interference  is needed only for developing the code and reviewing the test results. Can't wait to write about one of my C++ hobby project where I can show the practical use of CMake and its advantages in a large C++ project.

By using CMake we make the C++ projects to be able to build in multiple platforms using the same build scripts. We learn more with a practical project. I use CMake for all my projects. In the next blog post I'll explain the software development steps in C++ projects where I make use of the CMake to build, run tests and generate the documentation for the project.

<p>
{%- if page.show_ads -%}
  {%- include ads.html ad_src="google-adsense" ad_type="in-article" -%}
{%- endif -%}
</p>

### IDE

<span style="color:DeepSkyBlue">**Eclipse**</span> is the <span style="color:#0033cc">Integrated Development Environment (IDE)</span> I use for my C++ projects. I have experience using many IDEs some of them I remember are [Visual Studio][8], [Qt Creator][9], [Android Studio][10]. The purpose of using the IDE is that they assist us in trivial tasks which otherwise would require a lot of manual work. For example navigating through the code is easier in IDE as the IDE stores a database of all the symbols it finds in the code. It predicts the syntax errors on the fly and helps us in preventing the compile time error. An IDE also abstracts the common functions like compiling the code and running the binary by using the keyboard shortcuts. These things are very useful in a large codebase. It will be much better if an IDE assists us with AI capabilities like the <span style="color:#0055cc">JARVIS</span>.

<span style="color:Blue">**Visual Studio**</span> is the best in the world IDE for any kind of project and it is somewhat closer to being Jarvis :smiley:. Its intellisense is flawless. I had used it almost a year back for a C# based project for <span style="color:green">**Excel**</span>. I always wanted to use that but since it is not free and my present company does not have license to it so I had to find an alternative IDE. <span style="color:green">_The reason is that over time the IDE a software tool becomes a valuable skill to posses_</span>. It doesn't matter which IDE I was going to use I just want to use something that could help me with the redundant and boring tasks like for example automatically adding a license header at the top of every source file.

Since I view the tools I use as <span style="color:red">valuable skills</span> I need something that stays with me wherever I go. Which means I need something that's platform independent and free too. So I turned my attention to Eclipse which is a well known java based IDE mainly for projects in java. But for C++ projects we need to use the [CDT][11] plugin for Eclipse. It provides a fully functional C and C++ Integrated Development Environment with support for project creation, standard make build, source code navigation and various source knowledge tools.

But it does not support the CMake build natively :disappointed:. It does not have a superior intellisense like the Visual Studio. It hangs more often when predicting the symbol name in a large codebase. Since it runs on Java Virtual Machine it consumes more memory and loads very slow compared to Visual Studio. Due to this I use a combination of IDE, a code editor such as <span style="color:Brown">Vim</span> and the terminal. IDE for code navigation and intellisense. Code editor for small code changes and quick editing. Terminal for building the code, executing it and testing the code.

Editing code in Vim is not as smooth as it is in GUI based modern editors such as the Atom, Geany or just recently I started using <span style="color:MediumBlue">Visual Studio Code</span> as an alternative to atom editor as it was loading too slow and was not giving me a good experience. So overall I stick to using just the <span style="color:DeepSkyBlue">Eclipse</span>, <span style="color:Brown">Vim</span> and <span style="color:MediumBlue">Visual Studio Code</span> for my C++ projects.

## Postface

I will be writing about [Facial Features Recognizer][7]. It'll be an interesting project to explore. So stay tuned and wait for my updates.

<!-- Links in the post -->
[1]: {{ site.url }}{{ site.baseurl }}/tutorials/hello-world-cpp-cmake-eclipse/
[2]: https://www.gnu.org/software/make/
[3]: https://docs.microsoft.com/en-us/cpp/build/nmake-reference?view=vs-2017
[4]: https://cmake.org/
[5]: https://opencv.org/
[6]: https://github.com/google/googletest
[7]: https://github.com/manid2/FacialFeaturesRecognizer
[8]: https://visualstudio.microsoft.com/vs/
[9]: https://www.qt.io/qt-features-libraries-apis-tools-and-ide/#ide
[10]: https://developer.android.com/studio/
[11]: https://www.eclipse.org/cdt/