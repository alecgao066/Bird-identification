# Bird Identification
### Background
Bird identification is an in-class Kaggle competition, where we train a neuron network to classify in total 555 species of birds from photos. 
The trainning data set contains over 38000 images with corresponding labels, and the test set has 10000 images for us to predict. Below are some samples of the dataset.
![Examples from the data set](https://github.com/alecgao066/Bird-identification/blob/main/Demo/examples.JPG)
### Resnet 18
Resnet 18 pretrained on Imagenet data set is selected as the model. It's an effective model with light number of parameters. 
![Resnet 18](https://github.com/alecgao066/Bird-identification/blob/main/Demo/res18.JPG)

Here is some training tips.
1. Data augumentation by random rotation/cropping/ flipping. This can generate more training images to avoid overfitting the modal.
2. Anneal learning schedule, starting with a large learning rate and then samll ones. It helps the modal not to trapped in the local minimum. 
3. Multi-view testing and voting-based predictions. In the testng phase, randomly crop different regions from the testing image and then do multiple predictions. The final prediction is based on the voting counts of all predictions. It prevents the problem where a single cropped test image is biased.
4. Recommended parameters are as below:

| Parameter  | Adopted value |  
| --------   | -----:   | 
| Image size | 256*256  |  
| Batch size | 256      |  
| Epochs     |20        |
| Schedule   | {0:0.1, 5:0.01, 15: 0.001}      | 

Achieved best accuracy is **79.5%**!

### Resnext 32 * 4d
Resnext achieves better accuracy than Resnet on ImageNet rankings. It pretains the low complexity as the Resnet but accomplished more accurate predictions by adding cardinals. To further bring up the accuracy, I adopted Resnext 32 * 4d as the prediction modal. However, due to the time limit, the resnext model involved only reached to an accuracy of **66.65%**. I still need some more tuning to get it work better!
The future work will include trying increasing the batch size, using more training epochs and larger learining rates.

### Dicussions
The project is based on the starter's codes posted on Kaggle. The initial accuracy of the starter's codes is about 50%. After data augmentation, anneal learning, batch size and image size adjustment, the accuracy jumped to 78%.
I hoped to test the best epoch number of training. Therefore, I trained from a checkpoint and trained the modal with less and more epochs seperately. The accuracy indicates epoch change doesn't help a lot. The assumption is that in this case, the modal should not be under fitting or over fitting.
In the testing phase, the algorithm randomly crop some patches and then idnetify the predictions. The final prediction is based on the voting counts of all predictions
### Video
The presentation video talks about detailed implementations.
Link: https://drive.google.com/file/d/1L3f4WMDvi7jEqMOYAWiCfxM02D2c4E8u/view?usp=sharing
