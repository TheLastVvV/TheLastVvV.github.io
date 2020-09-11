---
title: "Design Stage in C++ project development"
excerpt: "Describing the problem definition, solution to the problem and \
          initial C++ code design using the hand written block diagram."

header:
  teaser: post_cpp_coding_1/header_image.svg
  alt: "Design Stage in C++ project teaser image"
  caption: "Design Stage in C++ project development"

categories:
  - tutorials

tags:
  - C++
  - Project
  - Problem Definition
  - Solution
  - Code Design
---

## Introduction

Following my [blog post][1], I wanted to write about <span style="color:green">
Professional C++ Coding</span> with an example project.
I had written a simple application as a hobby to learn the art of Software Development in C++.
The [Facial Features Recognizer][2] is an interesting project to explore.

I come from <span style="color:blue">Electronics and Communications Engineering</span> background so was
not experienced in C++ coding.
I didn't know C++ coding until I joined
<span style="color:red; font-family: Calibri; font-weight: bold; font-size: 16pt">Toshiba</span>.
I knew programming in C and OOPs concepts but not much in C++. I learnt C++ on the job.
And thought of writing it down here so I can refer my own notes to solve the problems in future.

Back in college I had studied the image processing and had learnt Machine Learning in holidays.
I used to write simple applications in Python to explore
image processing,
machine learning,
computer vision and
embedded systems.

Just two months back I had written the same application in C++ to learn how to a write well designed code in C++.
The hardest challenge in coding is always the testing. So my code style in C++ is inclined towards
making the testing easier.

<p>
{%- if page.show_ads -%}
  {%- include ads.html ad_src="google-adsense" ad_type="in-article" -%}
{%- endif -%}
</p>

## Problem Definition

Before we write code we have to **analyze** the problem and **derive solution** from it.
<span style="color:red; font-style: italic">The problem was to implement an application
to recognize features on face such as the Age, Emotion and Gender</span> Machine Learning
tutorials explain how the recognition is performed.
Hence I will not write about the machine learning side of the project. I just focus on the
C++ coding side of the project.

Most real world problems are presented to us in a very abstract form. For example when we
want to recognize the age on a face then there will be many possibilities of age.
As the age varies from 0 to 100 and above. Also the face doesn't vary much with a few years
gap. The face of a 20 year old and 21 year old remains almost same. Hence this is too
abstract to recognize. It is not possible for a human being to predict the exact age of
a person just by looking at the face. But it is possible to recognize the age group of the
person belongs to just by looking at the face. Hence we use this knowledge in defining our
problem and simplifying the solution. The other features are obvious hence we dont need to
make any modifications to the problem definition.

We have three features to recognize. Let's note down what they are as in below table:

| Age           | Emotion  | Gender |
| ------------- | -------- | ------ |
| Child  [5-10] | Anger    | Male   |
| Teen  [11-20] | Contempt | Female |
| Adult [20-40] | Happy    | --     |
| Old     [40+] | Neutral  | --     |
| --            | Sad      | --     |
| --            | Surprise | --     |

We now have the labels for each feature we want to recognize. We will use this information
to get the actual results at coding time.

## Design Stage

I already had trained **SVM models** to predict the required facial features.
I just need to make use of the models and APIs from the [OpenCV 2.4][3] to perform the recognition.
This stage is called the **Design stage**. Here we identify the current scenario and try to look for
a <span style="color:green">pattern</span>. This pattern is going to help us in realizing the code
we want to write.

As we know from the problem definition we have three different features to recognize.
They are Age, Emotion and Gender. So we need three separate <span style="color:green">
classes to encapsulate them</span>.
In design stage we just draw or scribble the possible solutions for the problem.
For three classes we draw three boxes with labels as Age, Emotion and Gender.
Now what if we want to recognize one more unique feature such as the Eyes later?
So we add one more box with label XXX to represent the unknown feature to be used in future.

Since each recognizer class requires the face data to perform the feature recognition and
gives an unique label representing the feature. We find a common functionality among the
recognizer classes. As a rule of thumb in C++ coding when there is a common functionality
among the classes we have to write a base class. This base class should provide the public APIs
to handle the interaction between the client classes and the recognizer classes.
The implementation of these APIs are hidden to the client classes. This will be explained in
detail in **Coding Stage** for now we just draw another box for the base class and draw the arrows
from the recognizer classes pointing towards the base class.

At the end of the design stage we get the below diagram:
<!-- img_1 - ffr_design_stage.jpg -->
![Hand written block diagram for Facial Features Recognition code design][img_1]
{: .align-center}

### Explanation of design

* **Client**: it is the main function which requests the feature result for an input image.
* **Base class**: It handles the common functionalities for all the recognizer classes. Provides the public APIs for the client to use. Hides the method implementation in a specific recognizer class.
* **Specific recognizer classes**: These are the Age, Emotion and Gender classes. These are isolated from each other hence the testing and fixing bugs later from the code becomes easier.

<p>
{%- if page.show_ads -%}
  {%- include ads.html ad_src="google-adsense" ad_type="in-article" -%}
{%- endif -%}
</p>

## Epilogue

This design is sufficient to realize what code to write. However when writing code we may come
across more functionalities and responsibilities that have to be implemented which we may not
see when designing the solution. Hence we cannot conclude that this will be the final design.
We must anticipate some changes in the design.

The purpose of this design stage is to think through the problem and the possible solutions to
it. We can start coding after this stage using the drawings and the scribbled notes as a reference.
In professional environment such as in my company we use **UML** to draw the class diagrams,
interaction diagrams, sequence diagrams and state diagrams as applicable to the problem at hand.
For this application it is very simple and straight forward hence no need to use UML.

When we start coding the problem definition may expand, we might face difficult sub-problems to solve.
Some times C++ might not allow us to go as planned. Hence we might come back to design stage and
make a few modifications. This can be reduced by coding more often. We must solve the majority of
the problem in the design stage itself. Once a proper design is setup we will not struggle much
in the later stages. This is sufficient to learn about the design stage in C++ coding.
So wait for my next blog post which explains the **Coding Stage** in professional C++ coding.

*If you have any questions then please leave comment below or ask me via social media.*

<!-- images in the post -->
[img_1]: {{ site.url }}{{ site.baseurl }}/assets/images/post_cpp_coding_1/ffr_design_stage.jpg "Block diagram for Facial Features Recognition code design"

<!-- Links in the post -->
[1]: {{ site.url }}{{ site.baseurl }}/notes/about-cpp-tools/
[2]: https://github.com/manid2/FacialFeaturesRecognizer
[3]: https://docs.opencv.org/2.4/index.html
