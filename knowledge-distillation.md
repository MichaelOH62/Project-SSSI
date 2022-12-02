# Project-SSSI
Project for CS301 F22
Project Members: Michael O'Hanlon & Adira Samaroo

For this project we will be using the repository under Adira S.'s GitHub account. We are using Google Colab for the environment of the project.

<h1>Model Compression:</h1>

For the last part of the project, we performed model compression using Knowledge Distillation, where a compressed, or student, model is trained to imitate a pre-trained, larger model or teacher, then the student model is fine tuned using the knowledge distillation process. The idea is to train one large model to be as optimized as possible then take the knowledge from the large model and use it to train a model that is easier to run on any machine regardless of hardware capability. This is called “distillation”, where the small model is trained to process data and generalize outputs the same way a larger model can with less data processing.

![mc_hello_world](https://github.com/adiraCode/Project-SSSI/blob/milestone-4/pictures/mc_hello_world.png?raw=true)

In a neural network, knowledge typically refers to the learned weights and biases the teacher gained from training to make its generalizations, but knowledge distillation normally uses the logits as the source of teacher knowledge. Other kinds of relevant knowledge include the relationship between different types of activations and neurons or the parameters of the teacher model themselves. To transfer the generalization abilities of the teacher model to the student, class probabilities are produced by the teacher model as “soft targets” for the student model to train on. Soft targets with high entropy provide more helpful information per training case than hard targets and less variance in the gradient between training cases. This allows the student to be trained using less data and a higher learning rate.

![Distillation_Fn](https://github.com/adiraCode/Project-SSSI/blob/milestone-4/pictures/Distillation_Fn.jpg?raw=true)

Neural networks typically produce class probabilities by using a “softmax” output layer that converts the logit computed for each class into a probability by comparing the first logit with the other logits. The logits are softened using a temperature scaling function which smoothes out the probability distribution and inter-class relationships learned by the teacher.

![Knowledge_Distill_Model](https://github.com/adiraCode/Project-SSSI/blob/milestone-4/pictures/Knowledge_Distill_Model.png?raw=true)

Knowledge passes to the student by training the model on a  transfer set and and using a soft target for each case in the transfer set produced by the teacher model with a high temperature in its softmax. That same high temperature is used to train the student model, then the temperature is set to 1 once the model is trained. From there the student model make its own hard predictions using the set temperature. The student model should then make predictions similar to the teacher model using the hard data set used to train the teacher model. 

<h2>Sources:</h2>

Distilling the Knowledge in a Neural Network. Geoffrey Hinton, Geoffrey Hinton, Jeff Dean. https://arxiv.org/pdf/1503.02531.pdf

Knowledge Distillation. Kenneth Borup. https://keras.io/examples/vision/knowledge_distillation/

Knowledge Distillation: Principles, Algorithms, Applications. Sundeep Teki. https://neptune.ai/blog/knowledge-distillation

<h1>Results Obtained:</h1>

We took the original model and used that as the teacher model, and we also created a new student model that would be the same in structure to the teacher model but have smaller layers and thus less parameters.

We compiled the student model the same way that the teacher model is compiled, but to train it we used a Distiller instead of fitting the model to the data. The Distiller takes both the teacher model and student model as input and trains the student model to perform similarly to the teacher model. This is what allows the student model to be compressed in size and still achieve the same accuracy as the teacher model.

<h2>Issues Encountered</h2>

In the end, we encountered several issues with this milestone in trying to get a working student model. First, we struggled with figuring out how to actually compress the model yet have it perform the same as the model that was not compressed. We found a useful tutorial on through keras by Kenneth Borup that covers how to perform knowledge distillation. We figured out that we could reduce the size of the model by changing the first input to the Conv2D layers of the model. This would decrease the number of filters and thus reduce the number of parameters in the model, compressing it.

We elected to create two models, one that was labeled as the “teacher”, and another that would be labeled as the “student” The teacher model was the same as the original model, just renamed. The student model was the same as the teacher model however we reduced the first input to the Conv2D layers by half.

Teacher Model Layer Example:

![teacher_model_layers](https://github.com/adiraCode/Project-SSSI/blob/milestone-4/pictures/teacher_model_layers.png?raw=true)

Student Model Layer Example:

![student_model_layers](https://github.com/adiraCode/Project-SSSI/blob/milestone-4/pictures/student_model_layers.png?raw=true)

Now that we had the model compressed, we struggled with actually figuring out how to perform the knowledge. The same tutorial we referenced had an example of a Distiller class that could be used to perform the knowledge distillation. We utilized this and were able to perform the distillation after making some modifications to work with the semantic segmentation model.

At this point we were able to perform the knowledge distillation, however the student model was not able to make accurate predictions. We tried adjusting the alpha and temperature arguments in the compile() function used on the model, but struggled to make any noticeable improvements. The current model struggles largely with making predictions, although we do believe that the teacher model has an impact on its performance because the teacher model is not very accurate. This was our largest issue, and after troubleshooting the student model and distillation process we could not find a way to substantially improve the student model’s accuracy.

Compiling the Distiller:

![distiller_compile](https://github.com/adiraCode/Project-SSSI/blob/milestone-4/pictures/distiller_compile.png?raw=true)

<h2>Segmented Images:</h2>

![segmented_images_mc_1](https://github.com/adiraCode/Project-SSSI/blob/milestone-4/pictures/segmented_images_mc_1.png?raw=true)
![segmented_images_mc_2](https://github.com/adiraCode/Project-SSSI/blob/milestone-4/pictures/segmented_images_mc_2.png?raw=true)
![segmented_images_mc_3](https://github.com/adiraCode/Project-SSSI/blob/milestone-4/pictures/segmented_images_mc_3.png?raw=true)

<h2>Training and validation loss vs. epochs:</h2>

![loss_vs_epoch_graph_mc](https://github.com/adiraCode/Project-SSSI/blob/milestone-4/pictures/loss_vs_epoch_graph_mc.png?raw=true)

<h2>Precision and Recall Values:</h2>

![precision_recall_values_mc](https://github.com/adiraCode/Project-SSSI/blob/milestone-4/pictures/precision_recall_values_mc.png?raw=true)

![precision_recall_mc](https://github.com/adiraCode/Project-SSSI/blob/milestone-4/pictures/precision_recall_mc.png?raw=true)
