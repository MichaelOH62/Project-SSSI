# Project-SSSI
Project for CS301 F22
Project Members: Michael O'Hanlon & Adira Samaroo

For this project we will be using the repository under Adira S.'s GitHub account. We are using Google Colab for the environment of the project.

Here is an explanation fo UNet and the results of the baseline performance using the edited code from 228_semantic_segmentation_of_aerial_imagery_using_unet.

<h1>U-Net:</h1>

UNet is a special architecture for image segmentation that resembles the shape of the letter 'U'. This is the result of the expansive path of the architecture sharing similarities to the contracting path. The network only uses the valid part of each convolution, in this case the pixels of each segmented part of the image, for which the full context is available in the input image. This allows for arbitrary large images to be seamlessly segmented through an overlap-tile strategy. 

![U-Net_Archetecture_1](https://github.com/adiraCode/Project-SSSI/blob/milestone-2/pictures/U-Net_Archetecture_1.png?raw=true)
![U-Net_Archetecture_2](https://github.com/adiraCode/Project-SSSI/blob/milestone-2/pictures/U-Net_Archetecture_2.png?raw=true)

To predict the pixels in the border region of the image, the missing context is extrapolated by mirroring the input image. This tiling strategy is important to apply the network to large images, since otherwise the resolution would be limited by the GPU memory. [1.] The network consists of a contracting layer, the general convolutional process, and an expansive path, which is composed of transposed 2D convolutional layers. [2.]

![Convolutional_Neural_Network](https://github.com/adiraCode/Project-SSSI/blob/milestone-2/pictures/Convolutional_Neural_Network.png?raw=true)

The contracting path is the typical path of a convolutional network, that repeats the application of two 3x3 convolutions which extract the high level features of the input image. Each followed by a rectified linear unit and a 2x2 max pooling operation which returns the maximum value for the portion of the image with stride 3 for downsampling, or reducing the sample rate from the majority cases to make the dataset more manageable. Max pooling acts as a noise suppressant while reducing the dimensionality. The convolution layers and pooling layer both form the i-th layer of the convolutional network, which is then used as the input for the next convolutional network.

The expansive path is where the network learns to confine the object using context from the previous layers. This path goes through steps of upsampling of the feature map followed by a 2x2 convolution, (up-convolution that increases the dimensions of the output that halves the number of feature channels), a concatenation with the correspondingly cropped feature map from the contracting path, and two 3x3 convolutions contracted by the 2x2 output of the up-convolution and the contracted output, each followed by a rectified linear unit. The cropping is necessary due to the loss of border pixels in every convolution.

At the final layer a 1x1 convolution is used to map each 64- component feature vector to the desired number of classes. In total the network has 23 convolutional layers. To allow a seamless tiling of the output segmentation map, it is important to select the input tile size such that all 2x2 max-pooling operations are applied to a layer with an even x- and y-size. [3.]

<h2>Sources:</h2>
[1. Introduction. Paragraph 5]] [3. Network Architecture. Paragraph 2] U-Net: Convolutional Networks for Biomedical Image Segmentation. https://arxiv.org/pdf/1505.04597.pdf

[2. Overview. Paragraph 1] UNet — Line by Line Explanation. https://towardsdatascience.com/unet-line-by-line-explanation-9b191c76baf5

<h1>Baseline Performance:</h1>

<h2>Segmented Images:</h2>

<h3>100 epochs</h3>

![Segmented_Images_100_1](https://github.com/adiraCode/Project-SSSI/blob/milestone-2/pictures/Segmented_Images_100_1.png?raw=true)
![Segmented_Images_100_2](https://github.com/adiraCode/Project-SSSI/blob/milestone-2/pictures/Segmented_Images_100_2.png?raw=true)

<h3>50 epochs</h3>

![Segmented_Images_50_1](https://github.com/adiraCode/Project-SSSI/blob/milestone-2/pictures/Segmented_Images_50_1.png?raw=true)
![Segmented_Images_50_2](https://github.com/adiraCode/Project-SSSI/blob/milestone-2/pictures/Segmented_Images_50_2.png?raw=true)
![Segmented_Images_50_3](https://github.com/adiraCode/Project-SSSI/blob/milestone-2/pictures/Segmented_Images_50_2.png?raw=true)

<h2>Training and Validation Loss vs. Epochs:</h2>

<h3>100 epochs</h3>

![Training_and_Validation_loss_100](https://github.com/adiraCode/Project-SSSI/blob/milestone-2/pictures/Training_and_Validation_loss_100.png?raw=true)

<h3>50 epochs</h3>

![Training_and_Validation_loss_50](https://github.com/adiraCode/Project-SSSI/blob/milestone-2/pictures/Training_and_Validation_loss_50.png?raw=true)

<h2>Precision and Recall Values:</h2>

<h3>100 epochs</h3>

![P-R_Curve_100](https://github.com/adiraCode/Project-SSSI/blob/milestone-2/pictures/P-R_Curve_100.png?raw=true)

<h3>50 epochs</h3>

![P-R_Curve_50](https://github.com/adiraCode/Project-SSSI/blob/milestone-2/pictures/P-R_Curve_50.png?raw=true)

The ten segmented images from the validation set are results of the model’s predictions after training itself. Overall, the model seems to have difficulty with recognizing differences in colors/labels on the images. Certain images appear with great success, those being the 8th image from the 100 epoch run and the last image from the 50 epoch run. However, a majority of the predictions do not appear to have a high accuracy when predicting an image from the validation set.

The training and validation loss curves are close in precision until the fifth epoch where a large gap is shown, this shows signs of overfitting. The assumption is that the model does not include enough parameters to handle the dataset. The model seems to only be optimized for up to fifty epochs, afterwards the tests diverge from the training losses and increase in inaccuracy.

For the precision and recall values, these numbers were generated using the precision_score and recall_score functions from the sklearn.metrics library. Both values come out to be the same for both the 100 epoch and 50 epoch run. A run was made after changing the average values to measure the precision and recall from micro to weighted and the scores reflected the results shown in the images more accurately. For precision and recall, both values dropped by ~0.1 for each value and both values were unique.

![P-R_Curve_weighted](https://github.com/adiraCode/Project-SSSI/blob/milestone-2/pictures/P-R_Curve_weighted.png?raw=true)

![P-R_values_and_Classification_Table_weighted](https://github.com/adiraCode/Project-SSSI/blob/milestone-2/pictures/P-R_values_and_Classification_Table_weighted.png?raw=true)
