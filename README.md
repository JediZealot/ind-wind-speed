# ind-wind-speed

# Objective
The objective of this topic is to develop accurate and reliable models for predicting wide area wind speed in the Indian Ocean region. 
The primary aim is to improve our understanding of the complex atmospheric dynamics and weather patterns that influence wind speeds in this area, and to develop predictive tools that can help stakeholders make informed decisions regarding a wide range of activities, including offshore energy production, maritime navigation, and cyclone forecasting. 
Ultimately, the goal is to increase safety, efficiency, and sustainability across a broad range of sectors by providing better insights into the behavior of wind patterns in this important region.

# Abstract
This research topic focuses on the development of a predictive model for wind speed in the Indian Ocean region, covering a wide area. The study aims to utilize machine learning algorithms to analyze the complex wind patterns and provide accurate wind speed predictions for various purposes such as maritime operations, renewable energy planning, and weather forecasting. 

The research involves collecting and analyzing large datasets from satellite data, to train the predictive model. The findings of this research have the potential to improve the accuracy of wind speed predictions and contribute to the sustainable development of the region.

# Dataset
Data has been collected from Earth Nullschool website, which obtains its weather data from the Global Forecast System (GFS) of the National Oceanic and Atmospheric Administration (NOAA) and Ocean Currents data from the Ocean Surface Current Analyses Real-time (OSCAR) project of Earth and Space Research (ESR), which is supported by NASA. 
The website offers a variety of data, including but not limited to wind speed and its direction, current speed and its direction, humidity, temperature and more for historical weather data
As shown in the figure, data has been scraped over the zone of 30°N, 60°E to 10°S, 100°E with jumps of 0.20 degree change in longitude and 0.20 degree change in latitude. Finally, a wind speed matrix of shape 201x202 is obtained for each time slot. Total 1213 time slots data was collected with an interval of 6 hours for each day
![image](https://github.com/user-attachments/assets/5f2a35ec-7032-4bfd-ae55-b446e1d30f39)


# ConvLSTM
ConvLSTM is a neural network architecture that combines convolutional layers and LSTM (Long Short-Term Memory) layers to process spatiotemporal data.
The convolutional layers are used to extract spatial features from input data, such as images or video frames, while the LSTM layers are used to capture temporal dependencies between the sequences of input data.
The key innovation of ConvLSTM is the introduction of convolutional operations in the LSTM cell, which allows the network to learn both spatial and temporal patterns simultaneously.
This makes ConvLSTM well-suited for tasks such as video prediction, where it is necessary to model both spatial and temporal dependencies in the input data.
![image](https://github.com/user-attachments/assets/5def81cd-019f-41d4-bf59-1cb1c7c64209)

# ANN
ANN (Artificial Neural Network) is a type of machine learning model inspired by the structure and function of the human brain.
It consists of a series of interconnected nodes, or neurons, organized into layers. Each neuron receives inputs from other neurons, and uses a mathematical function to calculate an output value, which is then passed on to the next layer of neurons.
The network is trained using a supervised learning approach, where it is presented with a set of input-output pairs, and adjusts its internal parameters (weights and biases) to minimize the difference between its predicted outputs and the true outputs.
Once trained, an ANN can be used to make predictions on new input data, by passing it through the network and obtaining the output value at the final layer.
ANNs are versatile and can be applied to a wide range of tasks, such as classification, regression, and pattern recognition. They are also used in many real-world applications, such as image and speech recognition, natural language processing, and finance.
![image](https://github.com/user-attachments/assets/b0936124-2975-47e1-b8cc-7917dd000c1d)

# Test Train split
Given the size of the dataset, loading it all at once would cause the RAM to crash. As this is time series data, the training was done in 4 batches, with 33% of each batch's data being used for validation. The validation data is taken from the end for both the ANN and ConvLSTM based models. There was an 80:20 Train-test split. 

# ConvLSTM model training
For each batch of data, the ConvLSTM based model underwent 25 epochs of training. Over the course of the 4 batches, it was trained for a total of 100 epochs. The table demonstrates that while the validation loss stays small, the training loss steadily declines. It is because, in contrast to the ANN, this model depends on the neighbouring values and can distinguish between copy values with small changes in the timeslots across various coordinates. The wind speed coordinate is irrelevant to the ANN model, which cannot distinguish between longitudes and latitudes.
![image](https://github.com/user-attachments/assets/69b25b6c-2825-4b64-ae31-6e13ff73e1c8)


# ANN model Training
The use of a new batch of data for model training as well as the conversion of the 2D data to 1D can be blamed for the abrupt variations seen in the graph of the ANN models. As a result of the same values being present in neighbouring cells for extended periods of time, the likelihood of the same data increases. The ANN model underwent three epochs of training for each batch of data. In order to cover all four batches, a total of 12 epochs were used to train the model. The validation loss falls below the training loss in the last batch. The fact that both the validation and training data's loss ranges are small, the ANN model appears to be reliable. 
![image](https://github.com/user-attachments/assets/668e2f20-90ee-43cd-939e-164890be616d)

# Evaluation Metrics
![image](https://github.com/user-attachments/assets/f2862997-da98-4ffa-907b-2f54301270f2)
![image](https://github.com/user-attachments/assets/7a068bcb-0dcb-4b73-a25d-f8758db7c9f2)
![image](https://github.com/user-attachments/assets/a5c5a1d9-4fb1-484f-8ca2-b563d29d17f8)

# 6Hrs Prediction
**ConvLSTM Model**<br>
![image](https://github.com/user-attachments/assets/7a01d6db-c5e5-463f-a04c-1909d1d48f1a)

**ANN Model**<br>
![image](https://github.com/user-attachments/assets/6bd531e3-c53c-418d-8c17-5719da0fcf2f)

# 12 Hrs Prediction
**ConvLSTM Model**<br>
![image](https://github.com/user-attachments/assets/61a4c2de-df5c-4da9-8142-13cb00f346f9)

**ANN Model**<br>
![image](https://github.com/user-attachments/assets/798bfbc8-8f08-43fd-8a06-42f5f16ca410)


# 24 Hrs Prediction
**ConvLSTM Model**<br>
![image](https://github.com/user-attachments/assets/e95b9b53-ff61-4ebd-85c7-c5dc472c4657)

**ANN Model**<br>
![image](https://github.com/user-attachments/assets/cbdb139a-b5f8-4b6e-afcf-1dad6181b20b)







