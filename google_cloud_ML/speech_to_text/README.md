# Speech to Text with Speech API

## input
  * [speech](https://storage.cloud.google.com/cloud-samples-tests/speech/brooklyn.flac)
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
