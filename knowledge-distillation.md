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

![segmented_images_mc_1](https://github.com/adiraCode/Project-SSSI/blob/milestone-4/pictures/segmented_images_mc_1.png?raw=true)
![segmented_images_mc_2](https://github.com/adiraCode/Project-SSSI/blob/milestone-4/pictures/segmented_images_mc_2.png?raw=true)
![segmented_images_mc_3](https://github.com/adiraCode/Project-SSSI/blob/milestone-4/pictures/segmented_images_mc_3.png?raw=true)

<h2>Training and validation loss vs. epochs:</h2>

![loss_vs_epoch_graph_mc](https://github.com/adiraCode/Project-SSSI/blob/milestone-4/pictures/loss_vs_epoch_graph_mc.png?raw=true)

<h2>Precision and Recall Values:</h2>

![precision_recall_values_mc](https://github.com/adiraCode/Project-SSSI/blob/milestone-4/pictures/precision_recall_values_mc.png?raw=true)

![precision_recall_mc](https://github.com/adiraCode/Project-SSSI/blob/milestone-4/pictures/precision_recall_mc.png?raw=true)
