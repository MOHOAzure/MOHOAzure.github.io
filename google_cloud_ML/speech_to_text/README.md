# Speech to Text with Speech API

## environment
In order to perform speech to text, please connect to VM instance provisioned for the lab via ssh:
![](https://i.imgur.com/S3qAzFL.png)

## input
  * [English speech](https://storage.cloud.google.com/cloud-samples-tests/speech/brooklyn.flac)
  * request.json
  ```json
    {
      "config": {
          "encoding":"FLAC",
          "languageCode": "en-US"
      },
      "audio": {
          "uri":"gs://cloud-samples-tests/speech/brooklyn.flac"
      }
    }  
  ```
  
## API call
```
curl -s -X POST -H "Content-Type: application/json" --data-binary @request.json \
"https://speech.googleapis.com/v1/speech:recognize?key=${API_KEY}" > result.json
```
  
## ouput: result.json
```json
{
  "results": [
    {
      "alternatives": [
        {
          "transcript": "how old is the Brooklyn Bridge",
          "confidence": 0.98314303
        }
      ]
    }
  ]
}
```


# Multilingual
The Speech API supports speech to text transcription in over 100 languages

## input
  * [French speech](https://storage.cloud.google.com/cloud-samples-tests/speech/brooklyn.flac)
  * input: request.json
  ```json
   {
     "config": {
         "encoding":"FLAC",
         "languageCode": "fr"
     },
     "audio": {
         "uri":"gs://speech-language-samples/fr-sample.flac"
     }
   }
  ```
  
## API call
As the same as above

## output: result.json
```json
{
  "results": [
    {
      "alternatives": [
        {
          "transcript": "maître corbeau sur un arbre perché tenait en son bec un fromage",
          "confidence": 0.9385558
        }
      ]
    }
  ]
}
```
