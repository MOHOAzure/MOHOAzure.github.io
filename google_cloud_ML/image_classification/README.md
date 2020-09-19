# Classify Images of Clouds in the Cloud with AutoML Vision

AutoML Vision helps developers with limited ML expertise train high quality image recognition models. Once you upload images to the AutoML UI, you can train a model that will be immediately available on Google Cloud for generating predictions via an easy to use REST API.
[[Intro Video](https://www.youtube.com/watch?v=GbLQE2C181U)]
[[GCP podcast](https://www.gcppodcast.com/post/episode-109-cloud-automl-vision-with-amy-unruh-and-sara-robinson/)]

## Input: 
  * Some cloud images (uploaded to cloud storage: qwiklabs-bucket)
  * a CSV file where each row contains a URL to a training image and the associated label for that image.
    * format of lines in theCSV file: {PATH_TO_IMAGE}, {LABEL}
    * e.g.:
    ```csv
    gs://qwiklabs-bucket/cirrus/1.jpg,cirrus
    gs://qwiklabs-bucket/cirrus/2.jpg,cirrus
    gs://qwiklabs-bucket/cirrus/3.jpg,cirrus
    gs://qwiklabs-bucket/cumulonimbus/1.jpg,cumulonimbus
    gs://qwiklabs-bucket/cumulonimbus/2.jpg,cumulonimbus
    gs://qwiklabs-bucket/cumulonimbus/3.jpg,cumulonimbus
    gs://qwiklabs-bucket/cumulus/1.jpg, cumulus
    gs://qwiklabs-bucket/cumulus/2.jpg, cumulus
    gs://qwiklabs-bucket/cumulus/3.jpg, cumulus
    ```
    * this CSV file is provided as **DATASET** for AutoML Vision API
      * Three types of model objective of the DATASET
        * single-labe classification (selected for this scenario)
        * multi-label classification
        * object detection
  * **NOTE**
    * If you were building a production model, you'd want at least 100 images per label to ensure high accuracy
    * Ideally, each label should have at least 10 images. Fewer images often result in inaccurate precision and recall.
    * You must also have at least 8, 1, 1 images each assigned to your Train, Validation and Test sets.
  * Appendix: [Youtube: preparing an image data in AutoML](https://www.youtube.com/watch?v=_2eG8xpRYZ4&feature=youtu.be)
  
## API call:
  * Operations are conducted on **Vision Dashboard** of GCP, including import images and labels, train/validate/test a model. No cmd API call is required.
  * Import images requires 5 to several minutes. Imported images' label can be relabeled.
  * Train a model requires 30 minutes to several hours. A Model can be cloud-hosted or downloaded to local machine.
  * Evaluation ![](https://i.imgur.com/RvglDvv.png)
  * Deployment a model requires 20 minutes to an hour.
  * Prediction
    * Generating predictions on the trained model using data it hasn't seen before.
    * Results are shown as the following section.
    
## Prediction
* ![](https://i.imgur.com/ScNYGOO.png)
* ![](https://i.imgur.com/gC8v51P.png)
* ![](https://i.imgur.com/QLSet6Q.png)
* ![](https://i.imgur.com/nkBMRpr.png)
* ![](https://i.imgur.com/x4dg6QC.png)
* ![](https://i.imgur.com/EN73YjP.png)
* ![](https://i.imgur.com/eQCB3Pe.png)
* ![](https://i.imgur.com/nwIaOD9.png)
  
## Readings
* https://www.blog.google/topics/google-cloud/cloud-automl-making-ai-accessible-every-business/
* https://cloud.google.com/vision/automl/docs/beginners-guide
