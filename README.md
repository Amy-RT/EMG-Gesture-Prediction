## EMG-Based Gesture Recognition using Neural Networks:

This project implements and compares the performance of several TensorFlow neural networks to recognize a set of user gestures based on EMG data. <br/>
The model is trained on EMG data collected by the MYO Thalmic bracelet: <br/>
![image](https://github.com/user-attachments/assets/3eee859a-3f88-4120-b658-05905d0643fb)
<br/>
[Image ref](https://www.digitaltrends.com/computing/myo-gesture-control-armband-review/)

Dataset source: https://archive.ics.uci.edu/dataset/481/emg+data+for+gestures 

The project follows the ‘Universal workflow of machine learning’ proposed by Francois Chollet (creator of Keras) in his textbook ‘Deep Learning with Python’:
1. Define the problem and assemble a dataset
2. Choose a measure of success 
3. Decide on an evaluation protocol 
4. Prepare the data
5. Develop a model that outperforms the baseline 
6. Scaling up: Develop a model that overfits 
7. Regularize model and tune hyperparameters

F1 and Cohen Kappa are the chosen measures of success for this project. 

Stage 4 in the universal workflow consisted of the following steps:
- The original dataset consists of over 1 million samples and has been pre-processed in the following ways:
- Removed unmarked EMG readings that were causing a class imbalance
- Further resolved the class imbalance using a stratified train test split 
- Experimented with SMOTE and Tomek Links to address the class imbalance
- Normalized EMG readings based on the findings of a Pubmed Research paper: 'Because of the inherent EMG signal variability, clinical interpretation of surface EMG signals requires normalization of the signal for physiologic interpretation and for comparison between bilateral muscles and between the same muscle on different days and between different subjects.' (McGill)
- Convert to tensor form and one-hot encode

A custom Keras callback class is utilized to automate plotting of training/validation loss curves and calculation of F1 score during training.

Learning rate scheduling was incorporated to smooth validation loss. Hyperparameter tuning was performed to using Bayesian hyperparameter optimization (KerasTuner)

The top performing architecture achieved an F1 score of 0.7 (+0.429 to the F1 statistical baseline)
