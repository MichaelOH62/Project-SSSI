# Project-SSSI
Project for CS301 F22
Project Members: Michael O'Hanlon & Adira Samaroo

For this project we will be using the repository under Adira S.'s GitHub account. We are using Google Colab for the environment of the project.

<h1>Model Compression:</h1>

For the model compression in this milestone we utilized the concept of Knowledge Distillation.

<h1>Results Obtained:</h1>

We took the original model and used that as the teacher model, and we also created a new student model that would be the same in structure to the teacher model but have smaller layers and thus less parameters.

We compiled the student model the same way that the teacher model is compiled, but to train it we used a Distiller instead of fitting the model to the data. The Distiller takes both the teacher model and student model as input and trains the student model to perform similarly to the teacher model. This is what allows the student model to be compressed in size and still achieve the same accuracy as the teacher model.

<h2>Segmented Images:</h2>

*segmented images pictures*

<h2>Training and validation loss vs. epochs:</h2>

*loss vs epochs graph*

<h2>Precision and Recall Values:</h2>

*precision recall values*

*precision recall graph*
