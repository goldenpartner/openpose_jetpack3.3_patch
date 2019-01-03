**This patch has already been updated by the [offical repo](https://github.com/CMU-Perceptual-Computing-Lab/openpose).**

When building [openpose](https://github.com/CMU-Perceptual-Computing-Lab/openpose) with Nvidia Jetson TX2, [doc/installation_jetson_tx2.md](https://github.com/CMU-Perceptual-Computing-Lab/openpose/blob/master/README.md) assumes Jetpack 3.1, cuda 8 and cudnn 6 as default. But if you are trying to install openpose under Jetpack 3.3, an error occurs as [cannot find -Iopencv_cudawarping](https://github.com/CMU-Perceptual-Computing-Lab/openpose/issues/918).

This is becaues by opencv is not compatable with cuda 9 yet, as *opencv_cudawarping* cannot be found. But *opencv_cudawarping* is not required for opepnose to work under *Jecpack 3.3*. Also, caffe provided by openpose and openpose itself use opencv2 as default. Therefore by modifying some files, we can make openpose work under jecpack 3.3

Following is a step by step solution to make changes by yourself (assuming you have already downloaded openpose and corresponding caffe files):

- First we need to enable opencv3 for caffe. 

    - **Uncomment line 21** in ***3rdparty/caffe/Makefile.config.Ubuntu16_cuda8_JetsonTX2***


- Then we need to enable opencv3 for openpose. 
    - **Uncomment line 18** in ***ubuntu/Makefile.config.Ubuntu16_cuda8_JetsonTX2***


- Lastly **change line 215** in ***/ubuntu_deprecated/Makefile.example*** from

    - *LIBRARIES += opencv_imgcodecs opencv_videoio opencv_cudawarping*

  to
    - *LIBRARIES += opencv_imgcodecs opencv_videoio*

Files provided within this repository is the modified version of these files. If you are using these files, copy all files into **openpose/ubutu** and run
***ubuntu/install_caffe_and_openpose_JetsonTX2_JetPack3.3.sh*** will do everything for you.
