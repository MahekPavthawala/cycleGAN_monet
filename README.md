# cycleGAN_monet
Monet is a French painter, created style of painting named as ‘impressionist’ where he painted the nature as he perceived it. As part of the Kaggle competition ‘I’m Somewhat of Painter Myself’, one must create a GAN algorithm’s generator model needs to recreate Monet style from a photo and discriminator will classify fake or not from real and generated. The cycleGAN will turn the generated Monet style images back to the regular images that will be zipped and the submitted to the Kaggle as part of the competition. The generator model created has similar architecture as the U-Net architecture and the discriminator model is a regular neural network that can classify fake or not. The given dataset from the Kaggle has two types of the dataset, (1) photos of regular and Monet style painting in .jpeg, and (2) photos of regular and Monet style painting in .tfrec formats. The .jpeg format images are not in sequential format while, .tfrec files are in the sequential format that is much easier for algorithm to process as each image are fed into the algorithm in certain sequence where the generator learn and recreate images and discriminator discriminates.

Kaggle Competition - ' I'm Something of Painter Myself ' | Ranked 40 out of 102.

## Pre-processing
For the network to be more robust, data augmentation is done where with TensorFlow keras library the layers are processed through random horizontal flips and random zoom on the image has been done. The input image size is 256 x 256 x 3 as the image ratio is 256 x 256 and the images are RGB, thus 3 channel input.

A function is defined for the image manipulation (image augmentation) for reshaping the image according to height, weight and channels.

In this project, the dataset is fetched from the Kaggle, and the author of the competition has introduced new format for the files that is ‘.tfrec’ which has sequence of records and only can be read sequentially through certain libraries.

## Model Develoment & Improvement
A GAN consists of at least two neural networks: a generator model and a discriminator model. The generator model is a neural network model that creates images from the given input and the discriminator will discriminate those images as actual images or generated images. If a discriminator can easily discriminate the images from original and fake, it means that either the generator is not efficient enough or the given data and the data augmentation methods are not good enough to help generator model to create fake images.

In this algorithm, for the generator model a U-Net architecture has been developed where it has layers of down sampling and upsampling both, concatenating each other and creating a U-shaped architecture where the images are convoluted from 256 x 256 x 3 to 64 x 64 x 3 and back to 256 x 256 x 3 and concatenating both side to help generator model generate and localize using an end-to-end training method. The generator first down samples the image and then up sample while creating a long skip connection between then that are helpful to bypass the vanishing gradient problem by concatenating the output layers to multiple layers instead one layer.

The discriminator is a simple neural network where it takes input from the generator and the original data both and compare them to classify whether the image is fake or not. So, instead of giving single node or value as an output, the discriminator gives a smaller 2D image with high density pixel values suggesting the real classifications and lower dense values as fake.

As per the Kaggle competition, the requirement asks for the GAN model where the model can recreate Monet style painting from the given input photos. During the step in the cycleGAN, the second pair of the generator and the discriminator that are optimized with the Adam Optimizer, will transform a generated Monet style painting back to a photo. The difference between original photo and twice generated photo is the cycle consistency loss. We want the original photo and twice transformed photo to be similar to each other.

## Requirements
A clear requirement of doing the project on it's own is to enter the Kaggle challenge or it will require Python 3.7 and above. Dataset is required to be downloaded or imported with Kaggle API.

## License
Distributed under the GNU License. See <a href = "https://github.com/MahekPavthawala/cycleGAN_monet/blob/main/LICENSE"> LICENSE </a> for more information.
