# Classifying news

## Knowledge requirements for this lab
* BigQuery: datatable for storage
* SQL: handle BigQuery for analyzing categorized data
* Python (or other lang.): a script to access Cloud Storage, the Natural Language API, and BigQuery.
* VM: envrioment of Nature Langauage API. [Ref: classify_a_ariticle](../classify_a_ariticle)
* Service account: used to authenticate to the Natural Language API and BigQuery from a Python script.

## News
* a large text dataset  
* news source: [BBC news articles](http://mlg.ucd.ie/datasets/bbc.html)
    * The dataset consists of 2,225 articles in five topic areas (business, entertainment, politics, sports, tech) from 2004 - 2005
    * .txt format
    
* An example of a news ariticle:
```
$ gsutil cat gs://spls/gsp063/bbc_dataset/entertainment/001.txt

Gallery unveils interactive tree

A Christmas tree that can receive text messages has been unveiled at London's Tate Britain art gallery.

The spruce has an antenna which can receive Bluetooth texts sent by visitors to the Tate. The messages will be "unwrapped" by sculptor Richard Wentworth, who is responsible for decorating the tree with broken plates and light bulbs. It is the 17th year that the gallery has invited an artist to dress their Christmas tree. Artists who have decorated the Tate tree in previous years include Tracey Emin in 2002.

The plain green Norway spruce is displayed in the gallery's foyer. Its light bulb adornments are dimmed, ordinary domestic ones joined together with string. The plates decorating the branches will be auctioned off for the children's charity ArtWorks. Wentworth worked as an assistant to sculptor Henry Moore in the late 1960s. His reputation as a sculptor grew in the 1980s, while he has been one of the most influential teachers during the last two decades. Wentworth is also known for his photography of mundane, everyday subjects such as a cigarette packet jammed under the wonky leg of a table.
```

## Prepare a place to store the text and category for each article.
* Create a BigQuery table for categorized text data
  * GCP > BigQuesry > select current project > create dataset > name the dataset
  * select the created dataset > create table > add 3 fields: (STRING) article_text, (STRING) category, and (FLOAT) confidence
  
## Prepare a service account
* GSP shell cmd
```
gcloud iam service-accounts create my-account --display-name my-account
gcloud projects add-iam-policy-binding $PROJECT --member=serviceAccount:my-account@$PROJECT.iam.gserviceaccount.com --role=roles/bigquery.admin
gcloud iam service-accounts keys create key.json --iam-account=my-account@$PROJECT.iam.gserviceaccount.com
export GOOGLE_APPLICATION_CREDENTIALS=key.json
```

## Prepare a python script
### Logic
First, a client is created for each service; then references are created to the BigQuery table. files is a reference to each of the BBC dataset files in the public bucket. We iterate through these files, download the articles as strings, and send each one to the Natural Language API in our classify_text function. For all articles where the Natural Language API returns a category, the article and its category data are saved to a rows_for_bq list. When classifying each article is done, the data is inserted into BigQuery using insert_rows().

### note
The Natural Language API can return more than one category for a document, but for this lab you're only storing the first category returned to keep things simple.

### python code
```python
from google.cloud import storage, language, bigquery

# Set up our GCS, NL, and BigQuery clients
storage_client = storage.Client()
nl_client = language.LanguageServiceClient()
# TODO: replace YOUR_PROJECT with your project name below
bq_client = bigquery.Client(project='YOUR_PROJECT_ID')

dataset_ref = bq_client.dataset('news_classification_dataset')
dataset = bigquery.Dataset(dataset_ref)
table_ref = dataset.table('article_data')
table = bq_client.get_table(table_ref)

# Send article text to the NL API's classifyText method
def classify_text(article):
        response = nl_client.classify_text(
                document=language.types.Document(
                        content=article,
                        type=language.enums.Document.Type.PLAIN_TEXT
                )
        )
        return response


rows_for_bq = []
files = storage_client.bucket('qwiklabs-test-bucket-gsp063').list_blobs()
print("Got article files from GCS, sending them to the NL API (this will take ~2 minutes)...")

# Send files to the NL API and save the result to send to BigQuery
for file in files:
        if file.name.endswith('txt'):
                article_text = file.download_as_string()
                nl_response = classify_text(article_text)
                if len(nl_response.categories) > 0:
                        rows_for_bq.append((str(article_text), nl_response.categories[0].name, nl_response.categories[0].confidence))

print("Writing NL API article data to BigQuery...")
# Write article text + category data to BQ
errors = bq_client.insert_rows(table, rows_for_bq)
assert errors == []
```

## API call
```python3 classify-text.py```

## Result
### check out BigQuery
  ``` 
    SELECT * FROM `YOUR_PROJECT_ID.news_classification_dataset.article_data` 
  ```
  ![](https://i.imgur.com/hslKRdr.png)
 
### see which categories are most common
  ```
  SELECT
    category,
    COUNT(*) c
  FROM
    `YOUR_PROJECT.news_classification_dataset.article_data`
  GROUP BY
    category
  ORDER BY
    c DESC
  ```
  ![](https://i.imgur.com/vE79Dno.png)


### get only the articles where the Natural language API returned a confidence score greater than 90%
  ```
  SELECT
    article_text,
    category
  FROM `YOUR_PROJECT.news_classification_dataset.article_data`
  WHERE cast(confidence as float64) > 0.9
  ```
  ![](https://i.imgur.com/fJYeL6j.png)
