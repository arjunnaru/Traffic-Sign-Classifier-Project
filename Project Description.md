
# Traffic Sign Classifier Project
1. The aim of the prject is to create a classifier to identify traffic signs from teh german dataset
2. Accuracy on validation set must be greater than 93%
3. Accuracy on 5 images downloaded from the internet were also tested

# Rubric Points

I will use the following sections to explain the rubric points and how I addressed them

## Files Submitted 
The following files are submitted
1. Ipython Notebook
2. HTML Version of Ipython Notebook
3. Readme File
4. All images used in the Project and Readme file

## Datatset Exploration
The following sections have the description for the Dataset Summary and Exploratory Visualization sections

## Visualization

### Data Distribution
To start with I just plotted a distribution of the data int eh dataset. This helped me visualize which calsses might have more representatives and which have lesser. Although at this point I still do not know what each class means. But I do get an understanding of if the data is lopsided and favours some calsses over the other. Even though in this data we can see that some calsses have significantly higher bin values compared to the others, I decided to move forward and see if this migth affect the final outcome. If it did I could always come back and work on data augmentation. But for now I decided to leave it as is.

![image.png](attachment:image.png)

### Converting to Grayscale
Althought my intial analysis showed that in a traffic sign colour does matter. I had problems with the size of the dataset and also how much time it was taking to train and validate the model. 

I read a little bit about this dataset online and some of the documentation said that converting images to grayscale still maintains the content and thus decide to convert the images to grayscale

## Visualizing Grayscale
This was an idea I picked up from one fo the implementations online. This helped me Visualize how the grayscale images compared to the coloured images. This was also the first time I had actually seen the different signs  

![image.png](attachment:image.png)

## Dataset Visualization
Next I decided to visualize the complate dataset. This would help me identify the kinds of signs we have in the dataset

## Histogram analysis
I did a histogram plot for all the three sets I had. Training Set, Validation set and the test set. I realized that we have a very similar distribution in terms of the number of signs per type that we have in all these sets.

![image.png](attachment:image.png)

## Preprocessing

I normalized the data using `((pixel)-mean)/(max-min)` This way the data was moved by the mean and also normalized from 0 - 1 at the same time. I found this to work slightly better in terms of the result obtained than the  `(pixel - 128)/ 128`

I then Padded the image to use it as input for my model

### Data set Shuffling
Data set is shuffled to try an drandomize the order in which the data goes into the model

## Model Architecture

Multiple model architectures were tested after which I came to the final model architecture that was used. I am pasting a copy of a spread sheet to show teh different models used and also a graph that I used to determine the best model to be used. All this information is also in the model.xls file

`Review 2`

I will also use this Section to Describe the changes i made to the network and how it evolved.

1. I first began by using a variation of the lenet architecture we had used in the calssroom for digit recognition. I did this because this was probably the only starting point for me to go ahead from. 
2. At this point the network had no dropouts although I did use Pooling in the CNN.
3. I then realized I was able to learn the training set very fast and thus training accuracy was saturation to ~1 very quickly. 
4. I then tweaked my learnin rate parameters to decrese the speed at which I learned and thus might get a better validation accuracy.
5. I then also worked on decreasing the number of Epochs. This was mostly done because the data set was too large but later on I realized that lesser the number of epoch the closer my training and validation accuracy were. 
6. At this point I decided I had to complete 2 basic aspects of the project. first my model was currently not good enough to even reach an accuracy of close to 95% on the training Set. Secondly I was beginning to see signs of overfitting in the data that I was getting. 
7. I then began to tweak the model to make sure I could atleast learn the training parameters properly. 
8. At this point I introduced image preprocessing and realized the model was able to learn the training set very well. And at the same time I was also able to see a higher accuracy on the validation set.
9. Now to counter overfitting I introduced dropouts in my flat layer.
10. I began by introducing it almost after every layer. I then realized this was making me loose too much information and thus had to kee removing them until I reached the final netwrok architecture. 
11. After this It was just a matter of increassing my accuracy on the validation set. I realized that using smaller filters on the convolution network helped the model elarn different features. 
12. Also pooling after evenry CNN also made me lose a lot of data and decreased my accuracy a lot. Once I made these cahnges I was able to easily go ahead and train the model to get the desired accuracy. 

The excel file shown below shows the different model architectures used and also show the accuracy i was able to achieve. This helped me ultimately understand how tweaking certain parameters or adding layers helped affect my result.

At various points in this process when I was stuck and out of idea, I did ask my brother for help and also the ever trustworth google.



![image.png](attachment:image.png)

![image.png](attachment:image.png)

Accumulated growth for all 23 models was plotted adn analysed and ultimately the gree line was selected to be model to use
The green line in the above graph was selected. 


The Final model Archticture is as follows:
1. Input Image of 32X32X1
2. Pad the image to 34X34X1
3. Use a 3X3 CNN Filter with a depth of 10 - output is 32X32X10 - relu and Max pool - 16X16X10
4. Use a 3X3 CNN Filter with a depth of 20 - output is 14X14X20 - relu and Max pool - 7X7X20
5. Use a 3X3 CNN Filter with a depth of 40 - output is 5X5X40
6. Flatten - 1000
7. 1000 - 512 - Relu and Dropout
8. 512 - 256 - Relu and Dropout
9. 256 - 128 - Relu
10. 128 - 43 (Output Labels)
11. Convert to Softmax and optimize



## Hyperparameters

Three major Hyper parameters were tuned
1. Epoch - 100
2. Learning rate - 0.001
3. Batch Size - 128

A detailed analysis of the ones used and the results are provided in the model.xls file

An Adam optimizer was used to otimize the result and update the weights.

## Solution Approach

According to the project report the accuracies are as follows

`Validation Accuracy = 96.9%`

`Test Accuracy = 95.7%`

### Downloaded Images

The following steps were followed to test the model on five images from the internet
1. 5 Images were downloaded and passed through the model.
2. Model predictions were noted and accuracy was calculated for the 5 images

![image.png](attachment:image.png)


`Review 2`

I chose the above 5 pictures. 
1. Warning road Sign - The first sign was chosen because it was one of the few ones I could recognize immediately. 
2. 30 and 50 kmph limit signs - The second and third one were chosen to try and see if not only the shape size and colour but also if the digits are able to confure the model. 
3. Priority Road - I chose the Last picture because it was one of the few with a very different shape. Also in terms of distinct features apart from the shape this sign does not really have any other features. No writing or signs on it and also not a very bright combination of colours. 
4. Stop Sign - The STOP sign was chosen because it is one of the most recognizable signs and was probably one of the first searches that came up when I looked for traffic sign classifier signs. It is also intereesting as one of the signs that has a lot of verbage on it. This could be a good thing as it could be distinctive but could also be a difficult quality for the model to recognize.



The five images were visualed with the correct and predicted labels

![image.png](attachment:image.png)

The top 5 softmax probabilities recorded by the model were show and the corresponding images as well

![image.png](attachment:image.png)
