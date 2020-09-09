## Google Cloud Machine Learing APIs Experience

- Participated in [Google Cloud Training Machine Learning APIs](https://google.qwiklabs.com/) labs.
- Learned env setup, Google Shell commands, Google Clould ML Restful API calls...etc.
- Practiced ML APIs in several scenarios.

## Outline
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
  * **nano** or **vim**: create and edit a file. For example, editing a request.json passed into API call.
  * **cat**: view a file, such as request.json and resonse.json

- Cloud storage (bucket)
  * Upload an image/file to a cloud storage bucket. 
     ```
    At GCP > Navigation menu > Storage > Create bucket > 
       give a "globally unique name" > Create > 
       Upload files (or just Drag the file) > 
       Edit Permission (clicked 3 dots besides the file) > 
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

- Practiced ML scenarios
  * [Text detection with Vision API](https://mohoazure.github.io/google%20cloud%20ML/text%20detection)
  * [Text Translation](https://mohoazure.github.io/google%20cloud%20ML/text%20translation)
  * [Analyzing the image's text with the Natural Language API](https://mohoazure.github.io/google%20cloud%20ML/text%20analysis)
    * analyzing sentiment and syntax, and classifying text into categories.
    * mid: an ID that maps to this entity in Google's Knowledge Graph.
    * salience: a [0,1] range indicating how important the entity is to the text as a whole.
  
