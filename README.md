# Mask Detection with Convoluited Neural Networks

### Introduction
According to the CDC and other health authorities, cloth or medical masks are an effective method of reducing the spread of covid-19. Many industries are using security guards or other staff members to enforce compliance of mask mandates but an automatic method would be much more efficient. Using still frames from video could be a method of alerting staff of a non-compliant visitor just like the magnetic detectors in retail stores alert staff when a non purchased product is leaving the store. The goal of this project was to develop a model that is capable of detecting whether someone is wearing a mask or not and therefore whether they are in compliance with health and safety regulations. 

### Data and Directories
The input data for this project consisted of two datasets downloaded from Kaggle. These datasets are made up of .jpg images belonging to 2 classes, with a mask and without a mask. They can be found here and here. Between these two datasets, there are 5028 images without masks and 4913 images with masks. The final image counts for each category are 4465 without a mask and 4295 with a mask. For this project to run you must have the following schema and naming convention in place within your working directory:

- yes 
- no   
- mask_detection_random   
  - no   
  - yes   
- test_rand   
  - no   
    - images   
  - yes   
    - images   

The original datasets should be deposited into the '/yes' and '/no' directories within the working directory based on their category of image. The '/yes' and '/no' directories are the directories where all the images are found prior to the randomized split. The '/mask_detection_random' directory is where the train and validation splits are saved while the '/test_rand' directory is where the test split is housed.

### Exploratory Data Analysis
The EDA mostly revolved around the image sizes. The images were between 29x29 and 5760x5760 pixels. When the datasets were uploaded they were resized to 256x256. I found that this was the largest I could make them before my processor gave out and it was within the range of the dataset. These images were manually cleaned. Photos with the following characteristics were removed from the dataset: duplicates, pre augmented images, collages, images with logos, and images with added text. I removed the duplicates and pre augmented images to ensure the same image wasn’t being duplicated in any form in either of the train, validation, or test sets. I didn’t think the collages were representative of many real-life situations and I was also worried about the hard edges made by the multiple borders. Images with logos and/or added text were almost exclusively found in the “yes” category. The original dataset contained many advertisements and I felt these features would be biased and make it too easy for my model to predict the “yes” images. 

### Model
The only model type that was tested in the project was the convoluted neural network. I tested somewhere between 10 and 15 different architectures. The number of convoluted, pooling, and dense layers, as well as the number of nodes for each, was iterated over to find the best fit. I also experimented with different dropout rates and frequencies. The model was compiled with the Adam, SGD, RMSprop, Adadelta, Adagrad, Adamax, and Nadam optimizers all at 0.001 and 0.0001 learning rates. I used graphs of the accuracy and loss as the model epochs ran, validation and training metric comparisons, and the confusion matrix of the test set predictions to gauge the performance of the model parameters and/or architecture. For the architecture and parameter testing, the datasets were relatively stagnant to ensure the changes in performance were not data related as I rarely used the randomizer function during that time. 

### Results
There was a large period of the testing time where the code was written to show the confusion matrix, the main performance indicator that I used, was broken and I did not know it. This likely caused a lot of unnecessary iterations. In the latest batch of 5 iterations, of the 2195 test images, 2134 were classified correctly (97.2%). It was slightly better at predicting the images with masks (97.3%) than it was at predicting the images without masks (97.1%). There is a 1.5% false-positive rate which would be the most problematic error in real life. 

### Application
If this model were to be applied to raw video it would have to run fast enough to handle a large number of frames (images) output by that video. High-quality films and television are typically filmed at 60 frames per second (fps) but other forms of video like CCTV or other security cameras would run at a much lower frame rate. For facial recognition purposes, it is necessary to film at 30 fps. The testing shows that it roughly takes 29ms to predict the image or frame. This speed would support video up to 34 fps and therefore can be implemented on raw video for prediction purposes. 

### Next Steps
The next steps for this project are to investigate the class imbalance to see if it is affecting the validation performance and the results. Testing with fewer dropouts in the model architecture is something else to be tested. A function to isolate the wrongly classified images should also be written so that they can be inspected for common factors. Finally applying this model to raw video is the ultimate goal and would make it applicable to real-world issues. This model could be hooked up to a camera monitoring a hallway within a mall or the entrance to a store where it could then alert staff if someone walks by without a mask. 
