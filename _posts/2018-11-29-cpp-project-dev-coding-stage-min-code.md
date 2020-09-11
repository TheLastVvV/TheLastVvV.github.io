---
title: "Initial coding stage in C++ project"
excerpt: "Writing the minimum code for the top level code design \
          developed in the design Stage"

header:
  teaser: post_cpp_coding_2/header_image.svg
  alt: "Initial coding stage C++ project teaser image"
  caption: "Initial coding stage C++ project"

categories:
  - tutorials

tags:
  - C++
  - Coding
  - Testing
  - Refactoring
---

<span style="color:green; font-family: Courier New; font-weight: bold;
font-size: 18pt">Coding</span>
is the most interesting phase of
the Software Development. :smile:
By the time we get here we must already know the below items to proceed:

1. The **problem  definition**, we must know exactly what the problem is.
   In our hobby project we are exploring i.e. [Facial Features Recognizer][1]
   we know we want to recognize the facial features from people's faces in
   the video and print it on the same video frames.
2. The **initial solution** to the problem, i.e. the result from the
   [design phase][2]. I get the visuals of imaginary code in my mind when
   scribbling down my design in paper.

At this point the rush to write code is at its peak because I might forget my
solution. And it will be very difficult to get it back. So let's start coding.

## Project Structure

First we create the project folder structure or simply project structure.
This is necessary because we will be writing a minimum of four classes and
a main function. And also the code for unit testing.
So totally we will be writing one kilo lines of code by blind guess backed by
my work experience.
Ya, its called one kilo lines instead of one thousand lines. :grin:
In case you dont understand any part of my tutorial please follow my
instructions blindly and do your experiments and try to learn on your own.
<span style="color:red; font-style: italic;">
As coding cannot be taught step-by-step and cannot be explained line-by-line.
</span>

We create the project structure from the command line using the terminal.
Because we are hardcore programmers and terminal is our everything. So we
start from here, we create the project structure as explained in my
first blog [Hello World C++ CMake project for Eclipse IDE][3].
We make use of the tools I have written about in my second blog
[About C++ Tools][4]. We arrive at the below project structure.

<!-- img_1 - Code structure screenshot -->
![C++ Project Structure][img_1]
*Project Structure*

**Note:** This project structure is that of the completed one.
In coding stage we just have to create **inc**, **src**,
and **CMakeLists.txt**. We create the rest later and as needed.
{: .notice--info}

## Initial code

| Tools     | Version     |
| --------- | ----------- |
| Ubuntu    | 18.04 (LTS) |
| CPU       | x86_64      |
| CMake     | 3.10.2      |
| G++       | 7.3.0       |
| Eclipse   | 2018-09     |
| Languages | C++, CMake  |

I always begin my project by writing the minimum code required to print a
simple statement. As we are going to use many components here such as cmake,
opencv and google tests library, writing the minimal code and testing its
execution ensures that the required component works as expected.

First we write the cmake script to set the project name and add a target to
build the project executable. The cmake script should be placed at the root
of the project structure i.e. in `FacialFeaturesRecognizer` folder.
The cmake code for the same is written in `CMakeLists.txt` as shown below.

{% highlight cmake linenos %}
cmake_minimum_required(VERSION 2.8)
set (CMAKE_CXX_STANDARD 11)

project(FacialFeaturesRecognizer)
get_filename_component(MODULE_NAME ${CMAKE_CURRENT_SOURCE_DIR} NAME)

#-- target for exe
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/inc/)
file(GLOB module_srcs ${CMAKE_CURRENT_SOURCE_DIR}/src/*.C++)
set(SRCS main.C++ ${module_srcs})

string(TOLOWER ${MODULE_NAME} MODULE_NAME)
add_executable(${MODULE_NAME} ${SRCS})
{% endhighlight %}
*Initial cmake code for the project*

<p>
{%- if page.show_ads -%}
  {%- include ads.html ad_src="google-adsense" ad_type="in-article" -%}
{%- endif -%}
</p>

Write the main function (the entry point to the executable) in a separate file
such as `main.C++`. Let's place the main.C++ file in the project root folder
i.e. in `FacialFeaturesRecognizer` folder.
By separating the main function from the application code
we can add another target to build the same code as a library to be used in
some other scenario.

{% highlight C++ linenos %}
#include <BaseRecognizer.h>

using namespace FFR;

int main(int argc, char **argv) {
  return execute(argc, argv);
}  // end
{% endhighlight %}
*Entry point to the executable*

Create **inc** and **src** the folders to save the project header files and
source files in respectively.

## Generate Eclipse IDE Project

Now we use the cmake script to generate the eclipse project to start coding in
Eclipse IDE. Go to `build` folder and enter the below command in terminal to
generate the eclipse project files.

{% highlight bash linenos %}
cmake ../FacialFeaturesRecognizer \
       -G"Eclipse CDT4 - Unix Makefiles" \
       -DCMAKE_ECLIPSE_GENERATE_SOURCE_PROJECT=TRUE \
       -DCMAKE_BUILD_TYPE=Debug \
       -DCMAKE_CXX_FLAGS="-std=c++11" \
       -DCMAKE_CXX_COMPILER_ARG1=-std=c++11
{% endhighlight %}
*Commands to generate the Eclipse IDE project*

The eclipse project files `.project` and `.cproject` will be generated
along with the cmake build files and stored in the `build` folder.
When we import this folder into eclipse workspace as an existing eclipse
project we can see the project details such as the build targets, binaries,
source files and cmake scripts.

I m creating the eclipse project from terminal and importing it manually
instead of asking eclipse to parse the cmake file and automatically generate
the project files which gives me the advantage of being able to control the
project from my terminal as the IDE hides many processes in working with the
project. For example it hides compilation flags passed to the compiler.

There are few other ways to generate the eclipse project from the cmake,
they are explained in the [link][5] to the official docs.

## Coding in Eclipse IDE

Start the Eclipse IDE.
Click `File->Import->General->Existing Projects into Workspace`.
Browse to the folder containing the cmake generated eclipse project files for
the our project i.e. `build` folder and import it. If the project is
successfully imported then we can click `Finish` to continue editing the code
in the Eclipse IDE.

The C++ project in Eclipse IDE looks like as shown below:
![Eclipse C++ Project][img_2_eclipse_cpp_project]
*Eclipse C++ Project*

Legends:
  1. Title of the project as we set in the `CMakeLists.txt` file.
     The postfix "-Debug" is appended to the project name to indicate that
     it is a debug build type.
  2. The build target we added in the `CMakeLists.txt` file. Since we added
     only one target hence I have highlighted it. The other build targets are
     just utilities. We will use this target, `all`, and `clean` more commonly
     than the other targets. More targets will be added later for unit tests,
     documentations etc and they show up when re-import the project.
  3. It is the link to the source directory i.e. `FacialFeaturesRecognizer`
     folder. Since the eclipse project description `.project` is stored in the
     `build` folder the cmake creates a link to the source folder. The changes
     we make in this linked folder also reflects in the actual source folder.

Let's create the `BaseRecognizer` class with the a simple `printf` statement to
confirm the working of the project setup. Right click `[Source directory]` and
go to `New->Class` enter the name of the class i.e. `BaseRecognizer` and the
namespace `FFR` (can be any unique identifer for the project). Prepend the
header file name with `inc/` and `src/` this will create the header file for
`BaseRecognizer` class in **inc** and **src** folder respectively. At the
bottom there is also an option to add a unit test code for the class. We
ignore the unit test code for now as we do not know what unit tests to write.

After creating the class, write the declarations in the header file and
definitions in the source file as:

{% highlight C++ linenos %}
#ifndef INC_BASERECOGNIZER_H_
#define INC_BASERECOGNIZER_H_

#include <cstdio>

namespace FFR {

class BaseRecognizer {
public:
	BaseRecognizer();
	virtual ~BaseRecognizer();

	void printLog(void);
};

extern int execute(int argc, char **argv);

} /* namespace FFR */

#endif /* INC_BASERECOGNIZER_H_ */
{% endhighlight %}
*BaseRecognizer.h*

{% highlight C++ linenos %}
#include <BaseRecognizer.h>

namespace FFR {

BaseRecognizer::BaseRecognizer() {
	// TODO Auto-generated constructor stub

}

BaseRecognizer::~BaseRecognizer() {
	// TODO Auto-generated destructor stub
}

void BaseRecognizer::printLog() {
	printf("HelloWorld\n");
}

/**
 * Entry point into the application
 */
int execute(int argc, char **argv) {
	int err = 0;

	// Detect facial features in the default video stream
	BaseRecognizer br;
	br.printLog();

	return static_cast<int>(err);
}

} /* namespace FFR */
{% endhighlight %}
*BaseRecognizer.cpp*

<p>
{%- if page.show_ads -%}
  {%- include ads.html ad_src="google-adsense" ad_type="in-article" -%}
{%- endif -%}
</p>

**Build** the project from the eclipse by double clicking the target for the
project. If it shows `undefined reference` error then delete the project from
the `Eclipse Workspace` without deleting the contents from the disk. Run the
same cmake command once again and re-import the project in eclipse. This is
done because the cmake build files were not aware of the newly created source
files.

**Run** the project by selecting `Run As->Local C/C++ Application`.
The `HelloWorld` is printed in the console view of the Eclipse IDE.

## Format code

We are ready to format the code to make it look professional.

1. Add the copyright header comment to indicate its creator, creation date,
   author and brief description about the contents in the file.
2. Click `Ctrl+Shift+F` to automatically format the source code in eclipse.
   I use the [Google Code Style][6] to format the code as it is very good
   and easy to read format. It does not come bundled with the Eclipse IDE.
   So download it from the link and import it in the Eclipse.

The code is made professional and it is ready for writing further coding.

{% capture notice-4 %}
**Note:** It will be a while before I write next blog post which explains full
code because I have to uprgade the OpenCV library to 4.0 as I dont feel like
writing a blog about working with a ten years old library.

The code hosted on my github account for this project is written using the
OpenCV 2.4 with the outdated APIs for SVM and ML modules.
{% endcapture %}
<div class="notice--warning">{{ notice-4 | markdownify }}</div>

<!-- images in the post -->
[img_1]: {{ site.url }}{{ site.baseurl }}/assets/images/post_cpp_coding_2/blog_post_4_ffr_1.jpg "C++ Project Structure"
[img_2_eclipse_cpp_project]: {{ site.url }}{{ site.baseurl }}/assets/images/post_cpp_coding_2/img_2_eclipse_cpp_project.jpg "Eclipse C++ Project"

<!-- Links in the post -->
[1]: https://github.com/manid2/FacialFeaturesRecognizer
[2]: {{ site.url }}{{ site.baseurl }}/tutorials/cpp-project-dev-design-stage/
[3]: {{ site.url }}{{ site.baseurl }}/tutorials/hello-world-cpp-cmake-eclipse/
[4]: {{ site.url }}{{ site.baseurl }}/notes/about-cpp-tools/
[5]: https://gitlab.kitware.com/cmake/community/wikis/doc/editors/Eclipse-CDT4-Generator
[6]: https://github.com/google/styleguide/blob/gh-pages/eclipse-C++-google-style.xml