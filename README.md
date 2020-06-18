# Image-Matting-U-Net
Automatic portrait segmentation using Wave U-net model 

The model takes a rgb image of 128x128 pixels. It then goes though in_conv layer - which is 2 convolutional layer.

Later, it goes through 3 down_sample layers - which is a maxpooling layer followed by a in_conv layer(2 convolutional layer).
Once the encoder part is done, the model moves to the decoder part. In it, the output of the encoder is presented to a deconvlutional layer(up_sample_conv) which is merged with the parallel layer(concat) in the encoder - Once merged, two convolutions(in_conv) are performed. This process is continued for 3 iterations.

The output of the model is a 4 channel image of 128x128 pixel with the 4th channel being the segmented map of the image and other three being the rgb channels.
All the layers have relu activation functions applied to them except for the last layer which has a tanh function since we want the outputs to be in the range of -1 to 1(same as out input).

The architecture looks something like this :
***Though the dimensions might not match, but the architeure is similar. ***

![](https://github.com/sanketsans/Image-Matting-U-Net/blob/master/U-net-Convolutional-Neural-Network-model-The-U-net-model-contains-two-parts.png)

Reference : https://www.researchgate.net/figure/U-net-Convolutional-Neural-Network-model-The-U-net-model-contains-two-parts_fig6_317493482

**Dataset used for training** : https://www.kaggle.com/laurentmih/aisegmentcom-matting-human-datasets 

Though I did not use the entire dataset(gdrive storage limit). I only partial images for the training (~10k images), which was 
sufficent. 
In the dataset, you get images of people and their segmented output in different folder. So, I created dataloader for the 
training purpose which could provide me a pair of the original (feature image) and its segmented result - which I can compare
the output of my Wave U-net model.

My Partial Dataset : https://drive.google.com/drive/folders/1yzj4VsIrN9RHWDNPm9FcMmIFYCSq5G-J?usp=sharing 

!["Dataloader image pairs"](https://github.com/sanketsans/Image-Matting-U-Net/blob/master/dataloader_output.png)

I have also attached an image for the semgented map of the image. Though dataloader only gives a pair of image and its
segmented output. 

I tried to train the model with MSE loss function which gave me pretty good results. I tried with sum reduction and simple
vanilla MSE. Sum reduction proved to provide better results.

**Actual Images**

![](https://github.com/sanketsans/Image-Matting-U-Net/blob/master/feat_img.png)

**Comparison of actual segmented image with the model's predictions on the test dataset**

![](https://github.com/sanketsans/Image-Matting-U-Net/blob/master/seg_img.png)

------------------------------------------------------------------------------------------------
I also tried to use the model on celeb dataset- http://mmlab.ie.cuhk.edu.hk/projects/CelebA.html

I have uploaded about 200 images for testing purposes on my gdrive. You can access here : https://drive.google.com/drive/folders/1S0Bzbv6l_BrVXzaTMJCcsChIy62Szvf4?usp=sharing

![](https://github.com/sanketsans/Image-Matting-U-Net/blob/master/celeb_pred.png)

