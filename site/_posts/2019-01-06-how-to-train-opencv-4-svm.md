---
title: "How to train OpenCV 4.0 Support Vector Machine to recognize facial features"
excerpt: "Train and test support vector machine (SVM), a supervised \
machine learning algorithm in OpenCV 4.0 using the Histogram of Oriented Gradients \
(HOG) as the feature descriptor"

show_hero: false

categories:
  - tutorials

tags:
  - C++
  - OpenCV
  - OpenCV 4.0
  - Histogram of Gradients
  - HOG
  - Machine Learning
  - ML
  - Support Vector Machine
  - SVM
---

In this tutorial we learn how to **train a model of support vector machine**,
**save the trained model** and **test the model** to check the percentage of its
prediction accuracy using the latest OpenCV version 4.0.

## Prerequisites

1. Knowledge of Machine Learning algorithm, SVM. (Refer links:
   [OpenCV][l_cv3_svm], [Wikipedia][l_wik_svm])
2. Knowledge of Feature Descriptor Histogram of Oriented Gradient
   (HOG) (Refer links: [Wikipedia][l_wik_hog])
3. Image processing algorithms such as **Histogram Equalization**, image
   scaling and image resizing.
4. CMake, Make, Eclipse IDE project, Git and Linux Bash scripting.

## System setup

### System Info

| Tools     | Version          |
| --------- | ---------------- |
| Ubuntu    | 18.04 (LTS)      |
| CPU       | x86_64           |
| CMake     | 3.10.2           |
| G++       | 7.3.0            |
| Eclipse   | 2018-09          |
| Languages | C++, CMake, Bash |

### Other softwares

1. OpenCV 4.0
2. Python 3
3. [imagenetscraper][l_imagenetscraper]
4. [autocrop][l_autocrop]
5. Fatkun Batch Download Image

<p>
{%- if page.show_ads -%}
  {%- include ads.html ad_src="google-adsense" ad_type="in-article" -%}
{%- endif -%}
</p>

To install the `opencv` and its dependencies refer the official documents
[here][l_cv3_doc]. We can also follow any online tutorial we get from google
search to install the opencv from source.

Install `imagenetscraper` and `autocrop` from `pip` (click on their links).
We need these tools to collect data from the web, crop faces and resize them
to smaller sizes in bulk. Follow their official documents for instructions.

When data from `imagenet` is not sufficient or not available we scrape the
data from the search engine results using `Fatkun Batch Download Image`
chrome extension. But this method is not encouraged to avoid copyright
and legal issues when using the images from web.

Once we collect the data we need to organize it meaningfully so we can access
it programmatically and manually.

## Data Organization

While collecting data from the web store the images in the below folder
structure.

```
FFR_dataset/
├── Age
│   ├── adult
│   ├── child
│   ├── old
│   └── teen
├── Emotion
│   ├── anger
│   ├── contempt
│   ├── happy
│   ├── neutral
│   ├── sad
│   └── surprise
└── Gender
    ├── female
    └── male
```

We will use the same directory names in the code to access them to **train**,
**save** and **predict** the recognition results. A minimum of 50 images in each
folder is required to train the models to get good prediction results.
Training more images can improve the results but not recommended as it takes
a lot of time to execute that and does not give significant improvements.

## Test OpenCV installation

Run a sample or a test binary to confirm the working of opencv components.
This is necessary to avoid any problems later. Some samples like the
`example_cpp_videocapture_basic` do not work if we don't have the video
manipulation library `ffmpeg` installed. Hence we run the below samples to
confirm the working of all the required modules.

1. **opencv_version**
  - To confirm the opencv version
2. **opencv_test_videoio**
  - To confirm the working of **videoio** module. 
     Use google test filter
     `videoio/Videoio_Bunny.read_position/4  # GetParam() = ("mp4", FFMPEG)`
     to test mp4 video read using ffmpeg
3. **opencv_test_ml**
  - To confirm the working of **ml** module.
     Use google test filter
     `ML_SVM.save_load`
     to test SVM model train, save and load.

<p>
{%- if page.show_ads -%}
  {%- include ads.html ad_src="google-adsense" ad_type="in-article" -%}
{%- endif -%}
</p>

## Write Code

Its a 20 hour long process :sweat_smile: to create the code we need to train
the SVM model using HOG feature descriptors. There are not enough tutorials
or sample code online to train a SVM model in C++. There is just one sample
provided in the official opencv repo to train the SVM with HOG,
[train_HOG.cpp][l_train_HOG]. It uses Support Vector Regression to detect
people in a video or a list of images.

We have three feature types: Age, Emotion and Gender. Four age groups,
six emotions and two gender types. Hence we implement a
**n-class classifier** to recognize each feature on a face data.

The code for the same is hosted at [example_cpp_train_HOG.cpp][l_modified_train_HOG].
Strangely the prediction result is below expected values for Age and Emotion
features. The prediction results for Gender detection is ok. Need to confirm
with the ML experts if the calculation of HOG features is ok as I had got
satisfactory results with opencv 2.4 APIs. Check the result logs at the below
links.

1. [Results log for HOG SVM using OpenCV 2.4][l_cv2_hog_svm_results_log]
2. [Results log for HOG SVM using OpenCV 4.0][l_cv4_hog_svm_results_log]

**TODO** need to fix the issue to improve the prediction results for Age
and Emotion facial features.
{: .notice--warning}

I prefer to write python scripts to execute non-core and repetitive tasks to save time.
Python scripts to do the repetitive tasks like training the SVM model with
variations is created and hosted at [py_train_save_svm_model.py][l_py_train_HOG].
But I am facing a bug with OpenCV 4.0 which stops the execution of the code.
Hence will update the working code soon with the result logs until then make
use of the procedure described here.

## Summary

1. Installed OpenCV 4.0 library on linux.
2. Learnt how to scrape **imagenet**, **google image search results**.
3. Learnt how to crop the faces from images in batches
4. Learnt to prepare the dataset to train a ML algorithm.
5. Converted a real world data into a feature vector.
6. Trained and tested a machine learning algorithm to classify an object.
7. Created ML models ready to be used in [Facial Features Recognition][l_ffr_code].

{% capture note %}

## Note

- Leave a comment to ask anything related to the blog post.
- Contact me via social media for consultation, guidance, tutorials or any suggestions.

{% endcapture %}
<div class="bg-warning p-3">{{ note | markdownify }}</div>

<!-- links in the post -->
[l_cv3_svm]: https://docs.opencv.org/master/d1/d73/tutorial_introduction_to_svm.html
[l_wik_svm]: https://en.wikipedia.org/wiki/Support_vector_machine
[l_wik_hog]: https://en.wikipedia.org/wiki/Histogram_of_oriented_gradients
[l_cv3_doc]: https://docs.opencv.org/master/d7/d9f/tutorial_linux_install.html
[l_ffr_code]: https://github.com/manid2/FacialFeaturesRecognizer.git
[l_imagenetscraper]: https://pypi.org/project/imagenetscraper/
[l_autocrop]: https://pypi.org/project/autocrop/
[l_img_net]: http://www.image-net.org/

[l_train_HOG]: https://github.com/opencv/opencv/blob/master/samples/cpp/train_HOG.cpp
[l_modified_train_HOG]: https://github.com/manid2/ProgramsForFun/blob/master/LearnOpenCV/ModifiedSamples/src/example_cpp_train_HOG.cpp
[l_cv2_hog_svm_results_log]: https://github.com/manid2/FacialFeaturesRecognizer/blob/cv2.4/results_log.txt
[l_cv4_hog_svm_results_log]: https://github.com/manid2/ProgramsForFun/blob/master/LearnOpenCV/ModifiedSamples/cv4_hog_svm_success_log.txt
[l_py_train_HOG]: https://github.com/manid2/FacialFeaturesRecognizer/blob/master/util/py_train_save_svm_model.py