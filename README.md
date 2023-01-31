# CNN Porosity Detection and Segmentation using Transfer-Learning and XCT Images in Additive Manufacturing

In this repository a CNN model was developed using transfer learning to classify the X-CT images taken from samples produced with additive manufacturing. The target is to train the model on learning the attribute of each image based on the amount of porosity that has been measured for each individual image.
Images are preprocessed using ImageJ to add filters, convert to a 2D image, and measure the porosity. Then the images are labeled manually.

Bellow you can find samples of the processed images using ImageJ.


![X-CT](https://user-images.githubusercontent.com/56824605/215649938-03c95882-fd9c-4c5b-9fa2-5d7275c18a1d.png)
![X-CT2](https://user-images.githubusercontent.com/56824605/215650336-c7d4f2f9-4e3a-4407-974c-66a9ea43a6cd.png)
![X-CT3](https://user-images.githubusercontent.com/56824605/215650346-c6b9bcce-7c07-4e7d-ba5e-6327f9eb7874.png)
![X-CT4](https://user-images.githubusercontent.com/56824605/215650351-9e9fad08-6de7-4627-a003-03878b8803fe.png)


Eventually the raw images are utilized and fed to the CNN model for training and validation.
