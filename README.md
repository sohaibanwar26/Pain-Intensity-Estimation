# Pain-Intensity-Estimation Application
This README provides an overview of the Dataset used, CNN model structure and instuctions on running this project. Please ensure that the necessary dependencies such as Pytorch, pandas,  and other relevant libraries as mentioned in the files are installed. 

# Dataset 
The dataset used in this project is from the The UNBC-McMaster Shoulder Pain Expression Archive Database. [Read more here](https://sites.pitt.edu/~emotion/fulltext/2011/Painful_Data.pdf)

It contains the following information:
1) Temporal Spontaneous Expressions: 200 video sequences containing spontaneous facial expressions relating to genuine pain
2) Manual FACS codes: 48,398 FACS coded frames
3) Self-Report and Observer Ratings: associated pain self-report and observer rating sat the sequence level
4) Tracked Landmarks: 66 point AAM landmarks.


# Facial Action Coding System 
The Facial Action Coding System (FACS) refers to a set of facial muscle movements that correspond to a displayed emotion. Each AU is scored on a 6-point scale based on its intensity ranging between “a = 0” for absent intensity and “f = 5” for maximum intensity. 

![FACS](https://github.com/sohaibanwar26/portfolio/blob/main/FACS.png)

[Read more here](https://www.paulekman.com/facial-action-coding-system/)


# PRKACHIN and SOLOMON PAIN INTENSITY METRIC (PSPI)
The PSPI score can be evluated as following:
PSPI score = Intesity(AU4) + max (AU6,AU7) + max ( AU9,AU10) + AU43.

Then, its PSPI score is derived as: PSPI score = 4 + max (3.4) + max (2,3) + 1 = 12
![Example](https://github.com/sohaibanwar26/portfolio/blob/main/nihms-1599641-f0001.jpg)

[Source](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7385931/)


# Preprocessing Data
The encoded frames are subjected to the following image processing technqiues:

Gray Scaling

Histogram equalization

Facial extraction using Haarcascade detection

Mean filtering



# Model Structure
This proposed architecture was inspired by the VGG16 architecture, Images go through two convolutional layers, with 64 (3 × 3) filters, a stride of 1 and a padding of 1, followed by a max-pooling layer with a filter size of 2 × 2 and a padding of 2. The resulting tensors go through additional convolutional layers at each step.The resulting feature maps are flattened and converted to a fully connected layer of 7 × 7 × 512 = 25,088 neurons, which is connected to a second fully connected layer of 1000 neurons, which is finally connected to the output layer of two neurons, corresponding to the two classes (i.e., pain and no-pain).​
![Model](https://github.com/sohaibanwar26/portfolio/blob/main/5-9302898x4%20(1).jpeg)

# Model tuning
Hyperparameter tuning was used such as use of batch normalization so that weights are updated between batches and the number of epochs required to train the model is minimized and also use of dropout regularization to reduce overfitting​
Training was​ done equally-distributed images for each class, using batches of 10 images, and evaluated using the cross entropy loss and the accuracy of each batch in each epoch​.



# Results
The model was evaluated on a set of 200 images and an accuracy of 83% was achieved. The model was then deployed as desktop application using tkinter with basic graphical user interface (GUI) to aid non techincal users to test the system with new images. 

![Accuracy](https://github.com/sohaibanwar26/portfolio/blob/main/Accuracy.png)

Confusion Matrix:
| Tables        | Positive | Negative  |
| ------------- |:-------------:| -----:|
Positive |  TP: 100 | FP: 0    |  |
Negative| FN: 34 | TN: 66    |   |

It was important to note that the model had a perfect performance when no pain is expressed (i.e FP), which in its turn means that the pain detection system is most likely never going to cause false alarms to the medical staff which can be very useful.

![App_Screen](https://github.com/sohaibanwar26/portfolio/blob/main/App_Screenshot.png)

Discussion:
It was important to note that the model had a perfect performance when no pain is expressed (i.e FP), which in its turn means that the pain detection system is most likely never going to cause false alarms to the medical staff which can be very useful in situations of emergency.


## Running on Local PC
Requirements:

    Python 3.7.7
    Git (for cloning the repository)

Installation:

    Open a terminal and clone this repository to your local machine:
    
    git clone git clone https://github.com/sohaibanwar26/Pain-Intensity-Estimation.git

    Select an IDE (E.g Visual Studio, PyCharm) 
    
    Open the project folder and inside the terminal write (pip install -r requirements.txt) to install the required libraries to run the project.
    
    Run the UI.py file.

    
  
