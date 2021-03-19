# Bird Identification
### Background
Bird identification is an in-class Kaggle competition, where we train a neuron network to classify in total 555 species of birds from photos. 
The trainning data set contains over 38000 images with corresponding labels, and the test set has 10000 images for us to predict. Below are some samples of the dataset.
![Examples from the data set](https://github.com/alecgao066/Bird-identification/blob/main/Demo/examples.JPG)
### Resnet 18
Resnet 18 pretrained on Imagenet data set is selected as the model. It's an effective model with light number of parameters. Here is some training tips.
1. Data augumentation by random cropping/ flipping/ rotation.
2. Anneal learning schedule.
3. Multi-view testing and voting-based predictions.
4. Recommended parameters are as below:

| Parameter  | Adopted value |  
| --------   | -----:   | 
| Image size | 256*256  |  
| Batch size | 256      |  
| Epochs     |20        |
| Schedule   | {0:0.1, 5:0.01, 15: 0.001}      | 

Achieved best accuracy is **79.5%**!

### Resnext 32*4d
Resnext achieves better accuracy than Resnet on ImageNet rankings. It pretains the complexity as Resnet but have more accurate predictions. However, due to the time limit, the resnext model involved only reached to an accuracy of **66.65%**. I still need some more tuning to get it work better!

### Video
The presentation video talks about detailed implementations.
Link: https://drive.google.com/file/d/1L3f4WMDvi7jEqMOYAWiCfxM02D2c4E8u/view?usp=sharing
