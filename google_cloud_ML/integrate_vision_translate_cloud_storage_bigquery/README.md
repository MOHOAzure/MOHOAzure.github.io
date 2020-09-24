# Integrate with Machine Learning APIs: Challenge Lab

## Scenario
You have been asked to develop a process to analyze sets of images of signage to extract and translate any text in the images. This extracted text information will be used to help classify the images as part of a machine learning project that will use this image dataset for model training and evaluation. The images all contain text, but the text may be in any language. The images are stored in a Cloud Storage bucket that has been provided for you.
You must use a Python script to process each of the image files by sending them to the Google Vision API to identify the text in the image. The text from each image must be saved back to files on Cloud Storage, with a separate file for the text from each image. If the text locale is not English (locale='en'), you must then send the text to the Google Translate API to get an English translation for the original text. Once all of the images have been processed, the script must upload the results to a BigQuery table.

![](https://cdn.qwiklabs.com/kycp4xbmAC9zE7Eufr48Q31ubz7DvPFfoYCIEIMBgAs%3D)

## Topics:
* Grant the service account admin privileges for BigQuery and Cloud Storage.
* Create and download a service account credentials file to provide Google Cloud credentials to a Python application.
* Modify a Python script to extract text from image files using the Google Cloud Vision API.
* Modify a Python script to translate text using the Google Translate API.
* Check which languages are in the extracted data by executing a BigQuery SQL query.

## Grant the service account
```
export PROJECT=<your_project_name>
gcloud iam service-accounts create my-account --display-name my-account
gcloud projects add-iam-policy-binding $PROJECT --member=serviceAccount:my-account@$PROJECT.iam.gserviceaccount.com --role=roles/bigquery.admin
gcloud projects add-iam-policy-binding $PROJECT --member=serviceAccount:my-account@$PROJECT.iam.gserviceaccount.com --role=roles/storage.admin
gcloud iam service-accounts keys create key.json --iam-account=my-account@$PROJECT.iam.gserviceaccount.com
export GOOGLE_APPLICATION_CREDENTIALS=key.json
```

## Python script
* extract text from images
    * https://googleapis.dev/python/vision/latest/gapic/v1/types.html#google.cloud.vision_v1.types.Image
    * https://googleapis.dev/python/vision/latest/gapic/v1/api.html#google.cloud.vision_v1.ImageAnnotatorClient.document_text_detection
* translate text to english
    * https://googleapis.dev/python/translation/latest/client.html#google.cloud.translate_v2.client.Client.translate
* upload text to BigQuery

## BigQuery
* Take a look

  ![](https://i.imgur.com/8wPrysa.png)

* SQL query
  ```sql
  SELECT locale,COUNT(locale) as lcount FROM image_classification_dataset.image_text_detail GROUP BY locale ORDER BY lcount DESC
  ```

  Row | locale | lcount
  ----| ------ | ------
  1 | en | 8
  2 | ja | 4
  3 | fr | 3
  4 | el | 2
  5 | ga | 2
  6 | it | 2
  7 | zh | 1
