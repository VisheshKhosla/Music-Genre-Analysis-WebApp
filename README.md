# Music-Genre-Classifier </br>
Implementation of music genre classifier using Deep Learning Model called Convolutional Neural Networks(CNNs) on Marsyas Dataset,CNNs are widely used for image classification problems because with the help of filters we can try to identify lines which further identifies shapes which leads to the detection of objects.The filters can be used as detectors and we can change their weights with the help of back-propagation.</br>
There are a total of 10 genres in the dataset:</br>
1.Blues</br>
2.Reggae</br>
3.Rock</br>
4.Disco</br>
5.Pop</br>
6.Metal</br>
7.Classical</br>
8.Jazz</br>
9.Hiphop</br>
10.Country</br>

## Preparation of Data
</br>
Since CNNs work really well on images we can represent audio as  images of depth 1 using spectrogram by applying short time fourier transformation or by using MFCCS(mel frequency cepstral coeffecients) which helps us in perceiving the sound as human auditory system,in the given project MFCCS have been used as inputs.In order to create more samples,the songs which are of 30 seconds have been chopped off into 10 segments leading to a total of 10,000 samples.The data has been then saved into a json file.Each of the segment has a  (130x13)  input data  where we have 130 MFCC vectors,each of them having 13 coeffecients.Librosa is a great library for doing anny work related to audio processing and we can easily convert an audio to a spectrogram or MFCC using librosa.The data has been furthere split into Train,Validation and Test data,validation data really helps us in testing our accuracy and we change the parameters before the application of the model on test data.


![MFCC](https://user-images.githubusercontent.com/44138895/87200956-46f1b380-c31b-11ea-9ce6-f7cbaf4b12a8.jpeg)

This is how MFCCs look like.</br>
## Architecture of the Model
</br>
First of all the input is fed in the form of MFCC to a convolutional layer with the activation function relu and 32 filters with a grid size of (3x3) and then to a pooling layer with a filter of (3x3) and a stride of 2 in the horizontal and vertical direction.Similary  another convolutional and a pooling layer is  with the same parameters is added  in order to improve the performance by increasing the complexity of the network.After that data is flattened and fed into the dense layer with activation function relu and a total of 64 neurons in it.Dropout layer has been added to avoid overfitting by elimination some neurons,the dropout probability is 0.3 and the elimination of neurons deletes all of its connections which leads to making the model robust.Finally the output has a total of 10 neurons,each of them having their activation function as softmax in order to have a uniform probability distrubution.</br>

## Optimizers and Loss Function
</br>
There are a total of 100 epochs and the batch size is 64,the weights are changed in order to minimize the cost.To minimize the cost adam optimizer has been used.</br>
The loss function used here is sparse categorical cross entropy which is very helpful in case the output is not one hot encoded and finally the output predcited is the one which is having the highest probability.</br>
Application of the model on test data lead to an accuracy of 63.1% which can be considered quite good provided this is not binary classification and a lot of confusion can happen in differentiating some of the similar genres.
