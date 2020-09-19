# Predict income category of a person

  * using the [United States Census Income Dataset](https://archive.ics.uci.edu/ml/datasets/Census+Income)
  * tensorFlow 2.3 model training and validation (locally). 3 python programs are involved for training.
    * util.py: contain utility methods for cleaning and preprocessing the data, as well as performing any feature engineering needed by transforming and normalizing the data.
    * model.py: define the input function and the model architecture.
    * task.py: train on data loaded and preprocessed in util.py
  * train & deploy a tensorflow model to AI Platfom
    * run training job on a single worker instance in the cloud, then deploy the trained model to support prediction.
  * request an online prediction and see the response.
    * since the model's last layer uses a sigmoid function for its activation, 
        outputs between 0 and 0.5 represent negative predictions ("<=50K") and 
        outputs between 0.5 and 1 represent positive ones (">50K")
  * the response
    
    ![](https://i.imgur.com/5EVwTp7.png)
