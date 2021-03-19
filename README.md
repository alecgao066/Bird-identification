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
Resnext achieves better accuracy than Resnet on ImageNet rankings. It pretains the low complexity as the Resnet but accomplished more accurate predictions by adding cardinals. To further bring up the accuracy, I adopted Resnext50 32 * 4d as the prediction modal. However, by the competition deadline, the resnext model only reached to an accuracy of **66.65%**. I still need some more tuning to get it work better!

The future work will be mainly about parameter tuning, including increasing the batch size, using more training epochs and larger learining rates. The reasons are as below. 
1. The loss curve seems to contain much oscillation, due to the small batch size. Small batch size helps to avoid local minimum but slows down the convergence. Now the modal needs 55 epochs and it still needs further training. I believe in this case trying larger batch size should help to increase the accuracy.
2. Before switching to a lower learning rate, I notice that the loss curve seems to be still decreasing. It indicates the epochs for large learning rates are not enough. Therefore, I think it's helpful to increase the training epochs especially for the initial stage, and also try larger learning rate.

Loss curve

![Loss curve](https://github.com/alecgao066/Bird-identification/blob/main/Demo/download2.png)

### Dicussions on accuracy improvement
1. The project is based on the starter's codes posted on Kaggle. The initial accuracy of the starter's codes is about 50%. After data augmentation, anneal learning, batch size and image size adjustment, the accuracy jumped to 78%.
2. I tested how epoch number influences accuracy and decided current epoch number setting is proper. I trained from a checkpoint that we obtained before and applied less and more epochs seperately. The accuracy indicates epoch change doesn't influence a lot (only 0.5 % variance for plus/minus 3 epochs).My interpretation is that the current modal is accurate, not under fitted nor over fitted. Otherwise it should be more sensitive to epochs. (For example, the modal is over fitted then the accuracy will be enhanced notably when we decrease the epochs)
3. In the testing phase, the algorithm randomly crops some patches and then computes their predictions. The final prediction is based on the voting counts of all predictions. It further improves the accuracy by about 1%.
4. I also tried a more accurate modal interms of Image Net rankings, which is the Resnext. However, before the deadline, I only achived an accuracy of 66.5%. I believe the classification accuracy should be beeter if I fine tune Resnext in the future.
### Video
The presentation video talks about detailed implementations.
Link: https://drive.google.com/file/d/1L3f4WMDvi7jEqMOYAWiCfxM02D2c4E8u/view?usp=sharing
