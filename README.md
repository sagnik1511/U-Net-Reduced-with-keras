# U-Net-Lowered-with-keras
Complete U-net Implementation with keras

<img align="left" width="80px" src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/c3/Python-logo-notext.svg/165px-Python-logo-notext.svg.png"/><img align="left" width="120px" src="https://colab.research.google.com/img/colab_favicon_256px.png"/><img align="left" width="80px" src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/2d/Tensorflow_logo.svg/173px-Tensorflow_logo.svg.png"/><img align="left" width="80px" src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/ae/Keras_logo.svg/768px-Keras_logo.svg.png"/><br><br><br><br><br>




## Original Paper Link : [https://arxiv.org/abs/1505.04597](https://arxiv.org/abs/1505.04597)

## Special Implementations :
---

The model is implemeted using the original paper. But I have changed the filter size of the layers.
The implemented layers are reduced to 25% of the original paper.

## Original Model Architecture :

![](https://github.com/sagnik1511/U-Net-Lowered-wiith-keras/blob/main/images/u-net-architecture.png)

## Dataset :
---
   The dataset has been taken from kaggle . It had a spefici directory shape, but it was tough to execute dataset building from it, so prepared an usable dataset.
   #### Link :  [https://www.kaggle.com/azkihimmawan/chest-xray-masks-and-defect-detection](https://www.kaggle.com/azkihimmawan/chest-xray-masks-and-defect-detection)
   #### Primary Directory Tree :
   
    .
    └── root/
        ├── train_images/
        │   └── id/
        │       ├── images/
        │       │   └── id.png
        │       └── masks/
        │           └── id.png
        └── test_images/
            └── id/
                └── id.png
                
   #### Given Images :
   
   | Image | Mask |
   |-|-|
   | <img align="center" width="1280px" src="https://github.com/sagnik1511/U-Net-Lowered-wiith-keras/blob/main/images/00071198d059ba7f5914a526d124d28e6d010c92466da21d4a04cd5413362552_image.png"/> | <img align="center" width="1280px" src="https://github.com/sagnik1511/U-Net-Lowered-wiith-keras/blob/main/images/00071198d059ba7f5914a526d124d28e6d010c92466da21d4a04cd5413362552_mask.png"/> |
   
## Supporting Libraries :

| Numpy | opencv | Matplotlib |
|-|-|-|
| <img align="center" width="80px" src="https://numpy.org/images/logos/numpy.svg"/> | <img align="left" width="80px" src="https://quintagroup.com/cms/python/images/opencv-logo.png/@@images/45c400ef-455a-40a1-93b3-5f0c6a81e746.png"/> | <img align="center" width="70px" src="https://matplotlib.org/stable/_images/sphx_glr_logos2_001.png"/> |


## Dataset Directory Generation :
---

We have performed operations  to ceate the data directory like this :

                  .
                  └── root/
                      ├── train/
                      │   ├── images/
                      │   │   └── id.png
                      │   └── masks/
                      │       └── id.png
                      └── test/
                          └── id.png



## Model Architectures ( U-Net Lowered ):
            
#### Model: “UNet”

| Layer Type |  Output Shape |  Param |  Connected to |
|-|-|-|-|
| input_1 (InputLayer)| [(None, 512, 512, 1) | 0 | |
| conv2d (Conv2D) |(None, 512, 512, 16) |160 |input_1[0][0] |
|conv2d_1 (Conv2D) |(None, 512, 512, 16) |2320 |conv2d[0][0]|
|max_pooling2d (MaxPooling2D)| (None, 256, 256, 16)| 0 |conv2d_1[0][0]|
|conv2d_2 (Conv2D)| (None, 256, 256, 32)| 4640| max_pooling2d[0][0]|
|conv2d_3 (Conv2D)| (None, 256, 256, 32)| 9248| conv2d_2[0][0]|
|max_pooling2d_1 (MaxPooling2D)| (None, 128, 128, 32)| 0 |conv2d_3[0][0]|
|conv2d_4 (Conv2D) |(None, 128, 128, 64)| 18496 |max_pooling2d_1[0][0]|
|conv2d_5 (Conv2D)| (None, 128, 128, 64)| 36928 |conv2d_4[0][0]|
|max_pooling2d_2 (MaxPooling2D)| (None, 64, 64, 64)| 0 |conv2d_5[0][0]|
|conv2d_6 (Conv2D) |(None, 64, 64, 128)| 73856| max_pooling2d_2[0][0]|
|conv2d_7 (Conv2D) |(None, 64, 64, 128) |147584| conv2d_6[0][0]|
|dropout (Dropout) |(None, 64, 64, 128) |0| conv2d_7[0][0]|
|max_pooling2d_3 (MaxPooling2D) |(None, 32, 32, 128) |0| dropout[0][0]|
|conv2d_8 (Conv2D)| (None, 32, 32, 256) |295168 |max_pooling2d_3[0][0]|
|conv2d_9 (Conv2D) |(None, 32, 32, 256)| 590080 |conv2d_8[0][0]|
|dropout_1 (Dropout)| (None, 32, 32, 256)| 0 |conv2d_9[0][0]|
|up_sampling2d (UpSampling2D)| (None, 64, 64, 256) |0| dropout_1[0][0]|
|conv2d_10 (Conv2D) |(None, 64, 64, 128)| 131200 |up_sampling2d[0][0]|
|concatenate (Concatenate) |(None, 64, 64, 256) |0 |dropout[0][0]
conv2d_10[0][0]|
|conv2d_11 (Conv2D)| (None, 64, 64, 128)| 295040| concatenate[0][0]|
|conv2d_12 |(Conv2D)| (None, 64, 64, 128) |147584|conv2d_11[0][0]|

up_sampling2d_1 (UpSampling2D) (None, 128, 128, 128 0 conv2d_12[0][0]

conv2d_13 (Conv2D) (None, 128, 128, 64) 32832 up_sampling2d_1[0][0]

concatenate_1 (Concatenate) (None, 128, 128, 128 0 conv2d_5[0][0]
conv2d_13[0][0]

conv2d_14 (Conv2D) (None, 128, 128, 64) 73792 concatenate_1[0][0]

conv2d_15 (Conv2D) (None, 128, 128, 64) 36928 conv2d_14[0][0]

up_sampling2d_2 (UpSampling2D) (None, 256, 256, 64) 0 conv2d_15[0][0]

conv2d_16 (Conv2D) (None, 256, 256, 32) 8224 up_sampling2d_2[0][0]

concatenate_2 (Concatenate) (None, 256, 256, 64) 0 conv2d_3[0][0]
conv2d_16[0][0]

conv2d_17 (Conv2D) (None, 256, 256, 32) 18464 concatenate_2[0][0]

conv2d_18 (Conv2D) (None, 256, 256, 32) 9248 conv2d_17[0][0]

up_sampling2d_3 (UpSampling2D) (None, 512, 512, 32) 0 conv2d_18[0][0]

conv2d_19 (Conv2D) (None, 512, 512, 16) 2064 up_sampling2d_3[0][0]

concatenate_3 (Concatenate) (None, 512, 512, 32) 0 conv2d_1[0][0]
conv2d_19[0][0]

conv2d_20 (Conv2D) (None, 512, 512, 16) 4624 concatenate_3[0][0]

conv2d_21 (Conv2D) (None, 512, 512, 16) 2320 conv2d_20[0][0]

conv2d_22 (Conv2D) (None, 512, 512, 2) 290 conv2d_21[0][0]

conv2d_23 (Conv2D) (None, 512, 512, 1) 3 conv2d_22[0][0]
Total params: 1,941,093
Trainable params: 1,941,093
Non-trainable params: 0
