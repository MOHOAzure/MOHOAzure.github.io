## Text detection with Vision API


- Input: ocr-request.json
  ```  
  {
  "requests": [
      {
        "image": {
          "source": {
              "gcsImageUri": "gs://{unique-bucket-name}/{image-name}"
          }
        },
        "features": [
          {
            "type": "TEXT_DETECTION",
            "maxResults": 10
          }
        ]
      }
  ]
  }

  ```
  
- API call
  ```
    curl -s -X POST 
          -H "Content-Type: application/json" 
          --data-binary @ocr-request.json 
          https://vision.googleapis.com/v1/images:annotate?key=${API_KEY}
  ```
  
