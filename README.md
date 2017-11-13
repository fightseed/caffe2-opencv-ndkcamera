# What is it?
For the purpose of real-time image classificaiton (e.g., open a camera, classify an image as fast as you can), an android app integrating native camera, caffe2, opencv in C++ is created.

# Why real-time image classification?
You could take a photo and classify it. But often people like me are impatient and not interested in the photo itself, but only the classification result which is computd at bullet speed.

# There are already similar apps based on tensorflow, caffe or torch. Why created this app, in other words, what is the difference?
Since both caffe and opencv are written in c++, I think it is better to integrate all of them in c++. 

Believe me, I am A BIG Java fan. Java, is so neat and clean to read and write. But, for the sake performance, people like me have doubts, others dont. 

Anyway, I intended to speed up real-time image classification by eliminating java code as much as possible.

# Where is caffe classification taken place? 
The whole caffe classification process is taken place in cpp/camera/ImageReader.cpp, runcaffe() method if I remember correctly.
I appologize for the extreamly messy and unorganized code. Well, this is my first app after all.
# Screenshot on huawei Mate 9
-----------
![screenshot](https://github.com/yge58/caffe2-opencv-ndkcamera/blob/master/device-2017-10-23-185701.png)


Source code is based upon the following,

[1] Android app is based on [Google NDK camera texture-view sample](https://github.com/googlesamples/android-ndk/tree/master/camera)

[2] The Caffe2 C++ classification procedure is from [Caffe2 example](https://github.com/leonardvandriel/caffe2_cpp_tutorial/blob/master/src/caffe2/binaries/pretrained.cc)

[3] The Caffe2 pretrained protobuf and related libraries are obtained from [AIcamera](https://github.com/bwasti/AICamera)

[4] The OpenCV libraries are obtained from [OpenCV4Android](https://github.com/opencv/opencv/tree/master/samples/android)      

Issues and bugs (memory leaks, resource allocation and free, threads concurrency, how to balance workload between threadd and etc ... ) if you see any of them or have any improvement suggestions, please help me by filing as many issues as you want. I will be very grateful. 


# Source Code Structure

  In texture-view,
           
              |__build
              |__build.gradle
              |__src
                   |__main
                         |__assets
                               |__squeeze_init_net.pb    (squeeze net architecture file)
                               |__squeeze_predict_net.pb (squeeze net pretrained weights)
                         |__cpp
                               |__caffe2  (caffe2 headers)
                               |__camera  (Android NDK native Camera API)
                               |__Eigen   (Eigen headers)
                               |__google  (protobuf headers)
                               |__opencv  (opencv headers)
                               |__opencv2 (opencv2 headers)
                               |__android_main.cpp   ( 1. contains all c++ files that are called from Java via JNI)
                                                     ( 2. handles all the native activities including camera, caffe, opencv.)
                               |__classes.h (Imagenet classes)
                               |__CMakeLists.txt     ( CMake )
                         |__Java
                               |__com__sample__textureview
                                                       |__ViewActivity.java (App's life cycle, UI)
                         |__libs
                               |__armeabi-v7a (This is the only ABI supported unfortunately)
                                            |__opencv (opencv4android libraries)
                                            |__(the rest libraries are copied from AICamera)
                         |__res
                         |__AndroidManifest.xml
                               



