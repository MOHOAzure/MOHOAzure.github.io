## Google Cloud Machine Learing APIs Experience

- Participated in [Google Cloud Training Machine Learning APIs](https://google.qwiklabs.com/) labs.
- Learned env setup, Google Shell commands, Google Clould ML Restful API calls...etc. Check out [Appendix](#appendix) below.
- Practiced ML APIs in several scenarios.

## Practiced ML scenarios
* [Text detection](/text%20detection)
* [Text translation](/text%20translation)
* [Text analysis](/text%20analysis)
  * analyzing sentiment and syntax, and classifying text into categories.
  * mid: an ID that maps to an entity in Google's Knowledge Graph.
  * salience: a [0,1] range indicating how important the entity is to the text as a whole.   
* [Label Detection]()
  * mid: an ID that maps to an entity in Google's Knowledge Graph.
  * score: a number from 0 - 1 indicating how confident it is that the description matches what's in the image.
* [Web Detection]()
  * fullMatchingImages
  * partialMatchingImages
  * pagesWithMatchingImages
  * visuallySimilarImages
* [Face Detection]()
  * position of face (head & skin)
  * direction & angle of eyes
  * mood (joy, sorrow, anger, and surprise.)
  * head wear
* [Landmark annotation]()
  * the mid of the landmark
  * it's name (description) 
  * a confidence score
  * The boundingPoly shows the region in the image where the landmark was identified.
  * The locations key tells us the latitude longitude coordinates of the picture.
* [Classify a news article]()
  * find categories for the article
* [Classifying news (a large text dataset) and storing results in BigQuery]()
  * require: BigQuery (datatable for storage) & python
  * SQL knowledge to handle BigQuery for analyzing categorized data
  * A python script to access Cloud Storage, the Natural Language API, and BigQuery.
* [Sentiment analysis]()
  * providing sentiment details on the entire text document
  * break down sentiment by the entities in the text
  * score: a number from -1.0 to 1.0 indicating how positive or negative the statement is.
  * magnitude: a number ranging from 0 to infinity that represents the weight of sentiment expressed in the statement, regardless of being positive or negative.
* [Syntax analysis]()
  * Automatic language detection
  * Part of Speech
  * DependencyEdge
* [Awwvision]()
  * classify (label) images from Reddit's /r/aww subreddit and display the labelled results in a web app.
  * require: Redis & Kubernetes
* [Predict income category of a person]()
  * using the [United States Census Income Dataset](https://archive.ics.uci.edu/ml/datasets/Census+Income)
  * tensorFlow 2.3 model training and validation (locally). 3 python programs are involved for training.
    * util.py: contain utility methods for cleaning and preprocessing the data, as well as performing any feature engineering needed by transforming and normalizing the data.
    * model.py: define the input function and the model architecture.
    * task.py: train on data loaded and preprocessed in util.py
  * train & deploy a tensorflow model to AI Platfom
    * run training job on a single worker instance in the cloud, then deploy the trained model to support prediction.
  * request an online prediction and see [the response](https://i.imgur.com/5EVwTp7.png).
    * since the model's last layer uses a sigmoid function for its activation, outputs between 0 and 0.5 represent negative predictions ("<=50K") and outputs between 0.5 and 1 represent positive ones (">50K")
 * Dataprep
   * with Trifacta

## Practicing ML scenarios
* Logo detection
  * identify common logos and their location in an image.
* Safe search detection
  * determine whether or not an image contains explicit content (adult, medical, violent, and spoof content).
* []()
  
## Appendix
- Basic cloud environment setup
  * A standard internet browser (Chrome)
  * A Google Clould account
  * A GCP project (Qwiklabs provisions a new project for a lab instance, it enables most APIs behind the scenarios)
  
- Prepare API for project usage
  * Access to API library
  * Search API by name or usage scenario
  * Enable API and retreive API key
  
- Usually used Google Shell commands
  * **curl** CLI tool: used for API call. 
  * **export**: set API key, OAuth2 token, or project ID as an environment variable, therefore API call could be concise.
  * **nano**, **vim**, **emacs**: create and edit a file. For example, editing a request.json passed into API call.
  * **cat**: view a file, such as request.json and resonse.json

- Cloud storage (bucket)
  * Upload an image/file to a cloud storage bucket. 
     ```
    At GCP > Navigation menu > Storage > Create bucket > 
       give a "globally unique name" > Create > 
       Upload files (or just Drag the file) > 
       Edit Permission (clicked 3 dots beside the file) > 
       Add a permission item(Entity: Public, Name: allUsers, Access: Reader)  > Save
      ```
  * Create a bucket with the Cloud Storage JSON/REST API.
    ```
    curl -X POST --data-binary @values.json \
      -H "Authorization: Bearer $OAUTH2_TOKEN" \
      -H "Content-Type: application/json" \
      "https://www.googleapis.com/storage/v1/b?project=$PROJECT_ID"
    ```
  * Upload a file using the Cloud Storage JSON/REST API.
    ``` 
    curl -X POST --data-binary @$BUCKET_OBJECT \
      -H "Authorization: Bearer $OAUTH2_TOKEN" \
      -H "Content-Type: image/png" \
      "https://www.googleapis.com/upload/storage/v1/b/$BUCKET_NAME/o?uploadType=media&name=$IMAGE_NAME"
    ```

