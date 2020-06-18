## Dog breed
*What kind of dog does the algorithm think that you look like? If you have a dog, does it predict your dog's breed accurately?*
---
### The Predictive Models
* Detect Humans: 
I used OpenCV's implementation of [Haar feature-based cascade classifiers](http://docs.opencv.org/trunk/d7/d8b/tutorial_py_face_detection.html) to detect human faces in images. OpenCV provides many pre-trained face detectors, stored as XML files on [github](https://github.com/opencv/opencv/tree/master/data/haarcascades).

* Detect Dogs: 
I use a pre-trained [ResNet-50](http://ethereon.github.io/netscope/#/gist/db945b393d40bfa26006) model to detect dogs in images, along with weights that have been trained on [ImageNet](http://www.image-net.org/).

* Classify Dog Breeds: 
I trained Convolutional Neural Network (CNN) to predict dog breeds from dog and human images. The initial model's test accuracy rate is 3.6%. I then used transfer learning to build models upon pre-trained networks. I experimented those bottleneck features as below
- [VGG-19](https://s3-us-west-1.amazonaws.com/udacity-aind/dog-project/DogVGG19Data.npz)
- [ResNet-50](https://s3-us-west-1.amazonaws.com/udacity-aind/dog-project/DogResnet50Data.npz)
- [Inception](https://s3-us-west-1.amazonaws.com/udacity-aind/dog-project/DogInceptionV3Data.npz)
- [Xception](https://s3-us-west-1.amazonaws.com/udacity-aind/dog-project/DogXceptionData.npz)

The final model used the pre-trained `Xception` model as a fixed feature extractor, where the last convolutional output of Xception is fed as input to the model. We added a global average pooling layer, a flattening layer, a fully connected layer equipped with a relu, a dropout, and lastly, a fully connected layer equipped with a softmax. The test accuracy rate is 81.3%.