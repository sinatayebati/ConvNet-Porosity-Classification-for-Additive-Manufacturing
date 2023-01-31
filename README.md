# CNN Porosity Detection and Segmentation using Transfer-Learning and XCT Images in Additive Manufacturing

In this repository a CNN model was developed using transfer learning to classify the X-CT images taken from samples produced with additive manufacturing. The target is to train the model on learning the attribute of each image based on the amount of porosity that has been measured for each individual image.
Images are preprocessed using ImageJ to add filters, convert to a 2D image, and measure the porosity. Then the images are labeled manually.

# Smaples of preprocessed X-CT images using ImageJ


![X-CT](https://user-images.githubusercontent.com/56824605/215649938-03c95882-fd9c-4c5b-9fa2-5d7275c18a1d.png)
![X-CT2](https://user-images.githubusercontent.com/56824605/215650336-c7d4f2f9-4e3a-4407-974c-66a9ea43a6cd.png)
![X-CT3](https://user-images.githubusercontent.com/56824605/215650346-c6b9bcce-7c07-4e7d-ba5e-6327f9eb7874.png)
![X-CT4](https://user-images.githubusercontent.com/56824605/215650351-9e9fad08-6de7-4627-a003-03878b8803fe.png)

# Prerequisites
The following modules and packages are required in order to run the associated code:

* TensorFlow
* Keras
* Numpy
* Matplotlib

They can be installed independently, or all at once by running `pip install`.

# CNN model and transfer learning

This model uses the Inception_v3 as the pretrained base model. Inception_v3 is an image recognition model developed by Google that has been shown to attain greater than 78.1% accuracy on the ImageNet dataset. The model is the culmination of many ideas developed by multiple researchers over the years. It is based on the original paper [https://arxiv.org/abs/1512.00567] by Szegedy, et. al.

The model itself is made up of symmetric and asymmetric building blocks, including convolutions, average pooling, max pooling, concatenations, dropouts, and fully connected layers. Batch normalization is used extensively throughout the model and applied to activation inputs. Loss is computed using Softmax.

A high-level diagram of the model is shown in the following screenshot:

![image](https://user-images.githubusercontent.com/56824605/215655885-21832e7c-aaca-42d1-bbc8-176eab8d217e.png)

The Inception model [README](https://github.com/tensorflow/models/tree/master/research/inception) has more information about the Inception architecture.

After loading the the pretrained Inception_v3 model, the output of the last layer was flattened and fed into a dense layers with 1024 neurons, a dropout layer with a ratio of 0.2, and ultimately into the last dense layer with 5 neurons which identifies the predicted class of the passed image.

```python
from tensorflow.keras.optimizers import RMSprop

# Flatten the output layer to 1 dimension
x = layers.Flatten()(last_output)
# Add a fully connected layer with 1,024 hidden units and ReLU activation
x = layers.Dense(1024, activation='relu')(x)
# Add a dropout rate of 0.2
x = layers.Dropout(0.2)(x)                  
# Add a final sigmoid layer for classification
x = layers.Dense  (5, activation='softmax')(x)           

model = Model( pre_trained_model.input, x) 

model.compile(optimizer = RMSprop(lr=0.0001), 
              loss = 'categorical_crossentropy', 
              metrics = ['accuracy'])
model.summary()
```

This model was able to obtain testing accuracy close to 100% in labeling the X-CT images based on the level of porosity.

# Author
Sina Tayebati
