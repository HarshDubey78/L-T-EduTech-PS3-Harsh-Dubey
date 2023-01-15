# L-T-EduTech-PS3-Harsh-Dubey
#### Problem Statement
Natural disasters and atmospheric anomalies demand remote monitoring and maintenance of naval objects especially big-size ships. For example, under poor weather conditions, prior knowledge about the ship model and type helps the automatic docking system process to be smooth. Thus, this set aims to classify the type of ships from an image data set of ships.
There are 5 classes of ships to be detected which are as follows:
<img width="622" alt="Capture" src="https://user-images.githubusercontent.com/37707687/59141322-6572d600-89c8-11e9-990f-8b7ace8e2582.PNG">

## Dataset Description
There are 6252 images in train and 2680 images in test data. The categories of ships and their corresponding codes in the dataset are as follows -

There are three files provided to you, viz train.zip, test.csv and sample_submission.csv which have the following structure.

train.zip contains the images corresponding to both train and test set along with the true labels for train set images in train.csv
## Evaluation Metric
The Evaluation metric for this competition is weighted kappa Score.
Approach
Here was my approach which I did in stages:



Step 1:
Seeing the slightly skewed distribution of classes in the training set, I decided to first Balance the number of examples belonging to each of the classes so that the model is not biased towards predicting any particular class in specific.
Step 2:
Augmentation
Real-Time Data Augmentations like 
* Flipping
* Rotation
* Lighting Changes
* Warps

were all carried out to make the model learn better
Now coming to the different model architectures used, I used the following architectures -

*Resnet34
*Resnet52
*Resnet101
*Resnet152
*Densenet161
*Densenet201
*SENet154
*ResNext101_64x4d



Here comes a few more additional steps which helped me push the score further and squeeze out those last decimal points - 

1. FastAI by default uses **Adam Optimizer** in order to train the models. 
   Also, Adam Optimizer usually **converges faster than SGD**.
   
   So, I used Adam First till training stagnates and then I switched out the optimizer with SGD because SGD    being the slower one, converges better, squeezing out a bit more from the model.
   
   Thus effectively, I used Adam to get the training parameters near the optimal values and then used SGD to get to the optimal values.
   
   
2.  **Discriminative Learning rates** were used so that the inner layers of the pretrained model do not get changed much, and the outer layers get updated at a greater rate than that.

    *( For a brief idea about Discriminative Learning Rate, please refer to Edit 1 at the end of the kernel )*
    

3. **Cyclical Learning rate scheduler** was used, following the **1-cycle policy** so that the we do not get stuck at an instable minima and get a stabler minima which performs over a wider range of loss functions and not just the train set specifically.

  
   
   
4. Finally, **ensembling** the different models trained gave a great push to the score of about 0.0147 to the F-1 Score.

    

