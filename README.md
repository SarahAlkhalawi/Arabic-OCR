# Arabic-OCR
The implementation of the OCR system for Arabic historical documents using the selected data from [KITAB corpus](https://kitab-corpus-metadata.azurewebsites.net). The figure below shows the main phases in our methodology for recognizing Arabic text using deep learning. The process begins with the pre-processing of the input page image, followed by line and word segmentation. The segmented word images are then divided into three distinct sets, consisting of a training set (80%), a validation set (10%) for monitoring the model's performance during training, and a testing set (10%) for evaluating the model. 

<img width="416" alt="Picture1" src="https://user-images.githubusercontent.com/66424485/218816002-dbcdb89c-0232-4b08-bc73-fb9ded26c1ec.png">

## Step 1: Pre-processing
 The books chosen from KITAB corpus have already been pre-processed. Thus, only resizing is required. We resized the word images to have a width of 64 pixels and height of 32 pixels. Resizing images is a critical pre-processing step, due to deep learning models learning faster on small images.
## Step 2: Line and Word Segmentation
 Line segmentation steps include blurring the image and the horizontal projection algorithm. As for the word segmentation, we used findContours function in OpenCV library, which finds the boundary of each word after smoothing the image.
 ### The results of the line segmentation method 
 ![Picture1](https://user-images.githubusercontent.com/66424485/218825258-fcd33957-fb59-4bc3-a514-c42edd87a9d1.jpg)
 ### The results of the word segmentation method 
 <img width="433" alt="Picture2" src="https://user-images.githubusercontent.com/66424485/218825345-33da5ba8-fce3-4520-b554-b948723c97e3.png">
 
## Step 3:	Deep Learning Model
The architecture of this model consists of 15 layers including the input and output layers. The architecture begins with an input layer, where every pre-processed word-segmented image in the dataset is resized to a width of 64 pixels and a height of 32 pixels with the number of channels as 1 since the image is grey-scaled and binarized. Followed by two convolution and pooling layers. The first convolution layer consists of 32 filters and the second convolution layer consists of 64 filters. Both layers have a filter of size (3, 3), ‘ReLu’ as the activation function, ‘he_normal’ weight initializer, and zero padding. After each convolution layer is a batch normalization layer. Next is a reshaping layer, followed by a dense layer then a dropout layer with 20% dropout rate. This architecture consists of two Bi-LSTM layers with 128 and 64 hidden units respectively. Lastly, the output of the Bi-LSTM layers is fed to a dense layer followed by the output layer to compute the CTC loss.
