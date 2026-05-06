
## Qestion 1-50 

1. Which of the following best describes Machine Learning (ML) compared to traditional programming?  
A) It relies strictly on rule-based systems written by programmers.  
B) It learns rules automatically by being fed data and correct answers.  
C) It does not require any data to function.  
D) It is the broadest category of AI.  

1. What is the primary characteristic that makes a neural network "deep" in Deep Learning?  
A) It processes large volumes of unstructured data.  
B) It relies on trial-and-error with rewards.  
C) It has multiple hidden layers in its structure.  
D) It uses knowledge from previous tasks.  

1. In which type of learning does the model learn hidden patterns and structures from entirely unlabeled data?  
A) Supervised Learning  
B) Reinforcement Learning  
C) Unsupervised Learning  
D) Transfer Learning  

1. Which learning approach uses an environment where an agent learns through trial-and-error with rewards and penalties?  
A) Supervised Learning  
B) Semi-Supervised Learning  
C) Reinforcement Learning  
D) Self-Supervised Learning  
 
1. What is the primary benefit of Transfer Learning?  
A) It creates labels from the data itself.  
B) It uses knowledge from one task to learn another, resulting in faster training and needing less data.  
C) It automatically tunes hyperparameters without the need for validation data.  
D) It groups similar items together without needing correct answers.  



1. Which metric is the most appropriate choice to evaluate a classification model trained on a highly imbalanced dataset, such as predicting spam in an inbox where 99% of emails are legitimate and only 1% are spam?  
A) Accuracy  
B) Mean Squared Error (MSE)  
C) F1-Score  
D) R² Score  

1. During the training of a neural network, what is the primary purpose of the backpropagation algorithm?  
A) To convert categorical variables into binary columns.  
B) To calculate how much each weight contributed to the prediction error using the chain rule from calculus.  
C) To randomly "turn off" neurons during training to make  predictions more robust.  
D) To scale input features to a standard range of 0 to 1.  

1. A student trains a model that achieves 99% accuracy on the training data but only 50% accuracy on the test data. Based on these symptoms, what is the most likely problem and an appropriate solution?  
A) The model is underfitting; the student should use a simpler model.  
B) The model is underfitting; the student should increase the learning rate.  
C) The model is overfitting; the student should use a more complex model.   
D) The model is overfitting; the student should add regularization or use a simpler model.  

1. In deep learning, why is the ReLU (Rectified Linear Unit) activation function often preferred over the Sigmoid function for hidden layers?  
A) ReLU outputs a probability distribution that sums to 1.  
B) ReLU maps outputs strictly to a -1 to 1 range, providing stronger gradients.  
C) ReLU helps solve the vanishing gradient problem because its derivative is 1 for positive inputs, unlike Sigmoid which has small derivatives.  
D) ReLU acts as a penalty for squared weights, preventing the model from becoming too complex.  

1.  In a standard machine learning pipeline, why is it considered a critical mistake to apply feature scaling (like standardization) to the entire dataset *before* splitting it into training and testing sets?  
A) It causes Data Leakage, where information from the test set inappropriately influences the training process.  
B) It forces the model to memorize the training data instead of learning general patterns.  
C) It causes the gradient descent algorithm to get stuck in a local minimum.  
D) It prevents the use of Cross-Entropy as a loss function.  

1.  What is the primary purpose of the Validation Set during the model training lifecycle?  
A) To prove the model works on completely unseen data for final evaluation.   
B) To adjust model settings (hyperparameters) without cheating by using the test data.  
C) To allow the model to adjust its internal weights and biases.  
D) To create new features by combining existing ones.

1.  In the context of feature engineering, why is it necessary to scale features like Age (0-100) and Income ($0-$1,000,000) to a similar range?  
A) To convert categorical variables into numerical ones.  
B) To prevent the model from learning spurious correlations.  
C) Because some algorithms work better when data is on a similar scale.  
D) To increase the complexity of the neural network.  

1.  Which of the following is considered a model parameter rather than a hyperparameter?  
A) The learning rate of a neural network.  
B) The number of hidden layers in a neural network.  
C) The batch size used during training.  
D) The weights in a neural network.   

1.  A practitioner uses Mean Squared Error (MSE) as a loss function. What characteristic makes MSE particularly sensitive to outliers?  
A) It uses the absolute difference between actual and predicted values.  
B) It averages the errors across all training examples.  
C) It squares the prediction errors, penalizing large errors heavily.  
D) It maps outputs to a probability distribution.  

1.  If a training dataset contains 1,000 examples and the batch size is set to 10, how many batches constitute one full epoch?  
A) 10  
B) 100  
C) 1,000  
D) 10,000  

1.  What is the likely consequence of setting a learning rate too high (e.g., 0.1) during gradient descent?  
A) The model will train exceptionally fast and converge smoothly.  
B) The model might overshoot the optimal weights and the loss will bounce around.  
C) The model will get stuck in a local minimum.  
D) The algorithm will default to batch gradient descent.  

1.  A model exhibits a training accuracy of 60% and a test accuracy of 58%. Which concept best describes this scenario?  
A) Overfitting  
B) Underfitting  
C) Convergence  
D) Data Leakage

1.  How does Dropout prevent a deep neural network from overfitting?  
A) By adding a penalty for large weights.  
B) By stopping training when validation loss increases.  
C) By randomly "turning off" neurons during training, forcing the network to learn redundant patterns.  
D) By normalizing the input features to a standard range.  

1.  In a medical diagnostic model where missing an actual disease (false negatives) is highly dangerous, which evaluation metric should be prioritized?  
A) Precision  
B) Accuracy  
C) Recall  
D) Mean Absolute Error  

1.  What does an Area Under the Curve (AUC) score of 0.5 on an ROC curve indicate?  
A) A perfect model.  
B) An excellent model.  
C) Random guessing (no skill).  
D) An overfitted model.  

1.  Logistic Regression is primarily used for which type of problem?  
A) Predicting continuous values.  
B) Unsupervised clustering.  
C) Binary classification into 2 classes.  
D) Generating new realistic data.  

1.  What is the primary difference in how Random Forests operate compared to a single Decision Tree?  
A) Random Forests use a single, extremely deep tree.  
B) Random Forests build multiple random decision trees and average their predictions.  
C) Random Forests can only be used for classification, not regression.  
D) Random Forests do not use features to make splits.  

1.  When using the K-Nearest Neighbors (KNN) algorithm, what is the risk of setting K=1?  
A) Underfitting (the model becomes too general).  
B) Overfitting (the model becomes too specific).  
C) The algorithm will ignore distance metrics.  
D) It will automatically convert to a Support Vector Machine.  

1.  How does a Support Vector Machine (SVM) handle non-linear data?  
A) By averaging the predictions of multiple linear models.  
B) By using the "kernel trick" to transform data into higher dimensions.  
C) By applying dropout to the input features.  
D) By converting continuous variables into categorical ones.  

1.  In the K-Means clustering algorithm, how is the optimal number of groups (K) typically chosen?  
A) By using the ROC curve.  
B) By applying L1 regularization.  
C) By using the Elbow method (plotting loss vs K).  
D) By calculating the F1-Score.  

1.  Which layer in a Convolutional Neural Network (CNN) is responsible for reducing dimensions while keeping important information, thereby reducing computation?  
A) Dense layer  
B) Convolutional layer  
C) Pooling layer   
D) Softmax layer  

1.  What specific problem do LSTMs (Long Short-Term Memory networks) solve that regular Recurrent Neural Networks (RNNs) struggle with?  
A) The inability to process images.  
B) Forgetting long-term context after many steps.  
C) The requirement for strictly labeled data.  
D) The inability to use the ReLU activation function.  

1.  What key innovation allows Transformer architectures to process sequential data faster than RNNs while maintaining better long-term context?  
A) The kernel trick  
B) The Attention mechanism enabling parallel processing  
C) Max pooling layers  
D) The Generator and Discriminator networks  

1.  In a Generative Adversarial Network (GAN), what is the role of the Discriminator?  
A) To create convincing fake data.  
B) To judge whether the data provided is real or fake.  
C) To focus attention on relevant parts of a sentence.  
D) To scale input features.  

1.  In K-Fold Cross-Validation where K=5, what percentage of the data is used for testing in each individual iteration (fold)?  
A) 5%  
B) 20%  
C) 80%  
D) 100%  

1.  During gradient descent, what does a "zero gradient" signify?  
A) The learning rate is too high.  
B) The model has reached a minimum (a good stopping point).  
C) The vanishing gradient problem has occurred.  
D) The data has leaked from the test set.  

1.  What is the purpose of One-Hot Encoding?  
A) To reduce the number of features.  
B) To convert categorical variables into binary columns because algorithms need numbers.  
C) To scale numerical values to a standard range.  
D) To map outputs to probabilities.  

1.  How does Principal Component Analysis (PCA) benefit a machine learning pipeline?  
A) By generating new training data when samples are low.  
B) By reducing the number of features while retaining important information.  
C) By automatically tuning hyperparameters.  
D) By preventing data leakage during the train/test split.  

1.  XGBoost is an example of which type of ensemble learning technique?  
A) Bagging  
B) Stacking  
C) Boosting  
D) Clustering  

1.  Which activation function is typically used in the output layer of a neural network for multi-class classification because it maps outputs to a probability distribution that sums to 1?  
A) ReLU  
B) Tanh  
C) Sigmoid  
D) Softmax  

1.  What architectural component helps fix the Vanishing Gradient problem in deep networks?  
A) Sigmoid activation functions  
B) Mean Squared Error loss  
C) ReLU activation functions and LSTMs  
D) K-Means clustering  

1.  What is a primary challenge associated with model deployment in production environments?  
A) Data distribution shifts (new data looks different from training data).  
B) Inference takes significantly longer than training.  
C) The inability to save (serialize) models.  
D) A/B testing is not possible with machine learning models.  

1.  Which of the following is a classic example of Data Leakage?  
A) Using dropout during training but not during inference.  
B) Normalizing the entire dataset before splitting it into train and test sets.  
C) Training a deep neural network on a simple problem.  
D) Using random search for hyperparameter tuning.  

1.  What technique is used to compare two different machine learning models directly in a live production environment?  
A) Cross-Validation  
B) Early Stopping  
C) A/B Testing  
D) PCA  

1.  What is the benefit of applying Batch Normalization between layers in a neural network?  
A) It completely eliminates the need for a loss function.  
B) It allows for faster training by reducing internal   covariate shift.  
C) It converts regression models into classification models.  
D) It converts text data into word embeddings.  

1.  In Computer Vision, how does Object Detection differ from Image Classification?  
A) Object Detection only uses pooling layers.  
B) Classification is unsupervised, while Detection is supervised.  
C) Object Detection locates objects with bounding boxes in addition to providing class labels.  
D) Classification works on videos, while Detection only works on static images.  

1.  In Natural Language Processing (NLP), the process of breaking text into words or subwords (e.g., "Hello world" → ["Hello", "world"]) is called:  
A) Word Embedding  
B) Semantic Segmentation  
C) Attention Mechanism  
D) Tokenization  

1.  Which NLP model architecture relies on dense vector representations where related words have similar vectors (e.g., "king" - "man" + "woman" ≈ "queen")?  
A) Random Forests  
B) Word Embeddings  
C) Discriminators  
D) Decision Trees  

1.  A machine learning engineer notices their model always predicts "not spam" and achieves 99% accuracy. What is the most likely cause of this misleading evaluation?  
A) Class imbalance in the dataset.  
B) The learning rate is too low.  
C) They used L1 regularization instead of L2.  
D) They are using a Transformer instead of an RNN.  

1.  Which of the following is a symptom of underfitting?  
A) Large gap between training accuracy and test accuracy.  
B) High training accuracy and low validation accuracy.  
C) Both training accuracy and test accuracy are low and   similar.  
D) The model converges too quickly.  

1.  What does L1 Regularization specifically encourage during training that L2 Regularization does not?   
A) It encourages some weights to become exactly zero, helping with feature selection.   
B) It encourages the model to learn redundant patterns.  
C) It penalizes squared weights.  
D) It stops training early based on validation loss.

1.  In reinforcement learning, the model learns by taking actions in an environment to maximize what?  
A) Labeled input pairs  
B) Hidden structures  
C) Rewards  
D) Dimensionality  

1.  What is the "Ground Truth" in supervised learning?   
A) The independent variables.  
B) The correct answer or target label the model should predict.  
C) The initial weights of the neural network.  
D) The un-scaled input data.  

1.  Which search strategy for hyperparameter tuning makes smart choices based on previous results rather than trying combinations blindly?  
A) Grid Search  
B) Random Search  
C) Bayesian Optimization  
D) Stratified Sampling  

1.  Semantic Segmentation in computer vision is best described as:  
A) Classifying the primary object in the center of an image.  
B) Drawing a single bounding box around multiple objects.  
C) Classifying every single pixel in an image to create a   pixel-level class map.  
D) Generating new realistic images from noise.  

