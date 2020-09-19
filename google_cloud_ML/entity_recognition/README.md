# Entity Recognition with Nature Language API

Identify entities and label by types such as person, organization, location, events, products and media

## Create API Key for **Nature Language API** (not by APIs & Services > Credentials)
0. using GCP shell cmd

1. set an **environment variable** (GOOGLE_CLOUD_PROJECT) with the PROJECT_ID which you will use throughout this codelab
```
export GOOGLE_CLOUD_PROJECT=$(gcloud config get-value core/project)
```

2. create a new service account to access the Natural Language API
```
gcloud iam service-accounts create my-natlang-sa \
  --display-name "my natural language service account"
```

3. create credentials to log in as your new service account. Create these credentials and save it as a JSON file "~/key.json"
```
gcloud iam service-accounts keys create ~/key.json \
      --iam-account my-natlang-sa@${GOOGLE_CLOUD_PROJECT}.iam.gserviceaccount.com
```

4. set an **environment variable** (GOOGLE_APPLICATION_CREDENTIALS), which is a path to the created API key
```
export GOOGLE_APPLICATION_CREDENTIALS="/home/USER/key.json"
```

## API call
* Environment
  Compute Engine > VM > SSH session

* API call
```
gcloud ml language analyze-entities 
        --content="Michelangelo Caravaggio, Italian painter, is known for 'The Calling of Saint Matthew'." 
        > result.json
```

## Output
```json
{
  "entities": [
    {
      "mentions": [
        {
          "text": {
            "beginOffset": 0,
            "content": "Michelangelo Caravaggio"
          },
          "type": "PROPER"
        },
        {
          "text": {
            "beginOffset": 33,
            "content": "painter"
          },
          "type": "COMMON"
        }
      ],
      "metadata": {
        "mid": "/m/020bg",
        "wikipedia_url": "https://en.wikipedia.org/wiki/Caravaggio"
      },
      "name": "Michelangelo Caravaggio",
      "salience": 0.82904786,
      "type": "PERSON"
    },
    {
      "mentions": [
        {
        "text": {
            "beginOffset": 25,
            "content": "Italian"
          },
          "type": "PROPER"
        }
      ],
      "metadata": {},
      "name": "Italian",
      "salience": 0.13981608,
      "type": "LOCATION"
    },
    {
      "mentions": [
        {
          "text": {
            "beginOffset": 56,
            "content": "The Calling of Saint Matthew"
          },
          "type": "PROPER"
        }
      ],
      "metadata": {
        "mid": "/m/085_p7",
        "wikipedia_url": "https://en.wikipedia.org/wiki/The_Calling_of_St_Matthew_(Caravaggio)"
      },
      "name": "The Calling of Saint Matthew",
      "salience": 0.031136045,
      "type": "EVENT"
    }
  ],
  "language": "en"
}
```

