# carcinoma-cells-classification
A semi supervised learning based approach to classify HES stained histopathological slices. I have compred different state-of-the art models for this classification task. VGG-16 and VGG-19 showed the best results in this task.
<br />
Here are the different classes <br />
__Carcinoma neg (-1) --> 0__ <br />
__Carcinoma pos, benign (0) --> 1__ <br />
__Carcinoma pos, malignant (1) --> 2__ <br />

The following steps are performed in this task <br />

1.Preprocessing: <br />
Loading and preprocessing the HES stained images. As mentioned, cropping may miss target cells, and resizing may change features, so it's recommended to maintain the original image sizes if possible. Normalize the pixel values to a consistent range (e.g., [0, 1]).

2. Prepare the labeled data: <br />
Spliting the labeled dataset (62 images) into training, validation, and test sets, maintaining a balanced class distribution. We have used 80% of the data for training, 10% for validation and remaining 10% for testing.
3. Transfer learning with pretrained models: <br />
We have used Vgg16, Vgg19 and Resnet50.
Modifying the last fully connected layer to match the number of classes in your task (3 classes: -1, 0, 1).
Freezing the weights of the pretrained layers.
4. Training with labeled data: <br />
Using the labeled training set to train the modified model, following the steps mentioned earlier.
5. Pseudo-labeling for unlabeled data:
Using the trained model to predict labels for the unlabeled images.
Assigning pseudo-labels to the unlabeled images based on the model's predictions. These pseudo-labels act as proxies for the true labels.
Combining the labeled training set and the unlabeled data with their pseudo-labels to create a larger training set.
6. Semi-supervised learning training: <br />
Training the model on the combined training set (labeled + pseudo-labeled unlabeled) using appropriate loss functions that take into account both the labeled and unlabeled samples.
Common techniques for semi-supervised learning include entropy minimization, consistency regularization, or using a combination of supervised and unsupervised losses.
7. Evaluation and fine-tuning: <br />
Evaluating the trained model on the labeled test set to measure its performance using appropriate evaluation metrics.
If needed, fine-tune the model by unfreezing and updating some of the pretrained layers while keeping others frozen.
8. Predicting on unlabeled data: <br />
Using the trained model to predict the class labels of the remaining unlabeled images.
Applying the same preprocessing steps used during training and pass the unlabeled images through the model to obtain predictions.
<br />






