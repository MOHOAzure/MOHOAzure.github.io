## Google Cloud Machine Learing APIs Experience

- Participated in [Google Cloud Training Machine Learning APIs](https://google.qwiklabs.com/) labs.
- Learned env setup, Google Shell commands, Google Clould ML Restful API calls...etc. Check out [Appendix](#appendix) below.
- Practiced ML APIs in several scenarios, such [Image](#image), [Speech, and Text](#nature-language)...[etc](#others).

## Practiced ML scenarios
### Image
* [Label Detection](label_detection)
  * mid: an ID that maps to an entity in Google's Knowledge Graph.
  * description: the name of the item.
  * score: a number from 0 - 1 indicating how confident it is that the description matches what's in the image.
* Web Detection
  * entityId: mid
  * description: the name of the item.
  * score: a number from 0 - 1 indicating how confident it is that the description matches what's in the image.
  * The following 4 responsed objects are urls point to websites containing images as names suggest
    * fullMatchingImages
    * partialMatchingImages
    * pagesWithMatchingImages
    * visuallySimilarImages
* [Face Detection](face_detection)
  * position of face (head & skin)
  * direction & angle of eyes
  * mood (joy, sorrow, anger, and surprise.)
  * head wear
* [Landmark annotation](landmark_annotation)
  * the mid of the landmark
  * it's name (description) 
  * a confidence score
  * The boundingPoly shows the region in the image where the landmark was identified.
  * The locations key tells the latitude longitude coordinates of the picture.  
* [Classify Images of Clouds in the Cloud with AutoML Vision](image_classification)
  * AutoML Vision helps developers with limited ML expertise train high quality image recognition models.
  * Once you upload images to the AutoML UI, you can train a model that will be immediately available on Google Cloud for generating predictions via an easy to use REST API.  
* [Awwvision](awwvision)
  * classify (label) images from Reddit's /r/aww subreddit and display the labelled results in a web app.
  * require: Redis & Kubernetes
  
### Nature language
* [Multilingual speech to text](speech_to_text)
* [Text detection](text_detection)
* [Text translation](text_translation)
* Text analysis
  * analyzing sentiment and syntax, and classifying text into categories.
  * mid: an ID that maps to an entity in Google's Knowledge Graph.
  * salience: a [0,1] range indicating how important the entity is to the text as a whole.   
* [Classify a news article](classify_a_ariticle)
  * find categories for the article
* [Classifying news and storing results in BigQuery](classify_news)
  * news: a large text dataset
  * require: BigQuery (datatable for storage) & python
  * SQL knowledge to handle BigQuery for analyzing categorized data
  * A python script to access Cloud Storage, the Natural Language API, and BigQuery.
* [Entity Recognition](entity_recognition)
  * Identify entities and label by types such as person, organization, location, events, products and media
* [Sentiment analysis](sentiment_analysis)
  * Provide sentiment details on the entire text document or on each entity
* [Syntax analysis](syntax_analysis)
  * Extract tokens and sentences, identify parts of speech (PoS) and create dependency parse trees for each sentence.
  * Automatic language detection
  
### Others
 * Dataprep
   * with Trifacta
* [Predict income category of a person](predict_income)

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
  * **gsutil cp [OPTION]... src_url dst_url**
    * upload a file to a bucket : gsutil cp \*.txt gs://my-bucket
    * download a file from a bucket: gsutil cp gs://my-bucket/*.txt .

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

