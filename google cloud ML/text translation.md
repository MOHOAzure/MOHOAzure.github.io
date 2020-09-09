## Text Translation with Tranlation API

- Pre-condition: [Text detection with Vision API](https://mohoazure.github.io/google%20cloud%20ML/text%20detection)

- Activity
  1. Create a request file: translation-request.json 
  ```
    {
      "q": "your_text_here",
      "target": "en"
    }
  ```
  
  2. Parse text extraced by Vision API to the request file
    ```
    STR=$(jq .responses[0].textAnnotations[0].description ocr-response.json) 
      && STR="${STR//\"}" 
      && sed -i "s|your_text_here|$STR|g" translation-request.json
    ```
    
    * Example request file: translation-request.json
    ```
    {
      "q": "LE BIEN PUBLIC\nles dépêches\nPour Obama,\nla moutarde\nest\nde Dijon\n",
      "target": "en"
    }
    ```

  3. API call :
  ```
    curl -s -X POST 
          -H "Content-Type: application/json" 
          --data-binary @translation-request.json 
          https://translation.googleapis.com/language/translate/v2?key=${API_KEY} 
          -o translation-response.json
  ```

- Post-condition
  * Example output file: translation-response.json
  ```
  {
    "data": {
      "translations": [
        {
          "translatedText": "PUBLIC PROPERTY dispatches For Obama, mustard is from Dijon",
          "detectedSourceLanguage": "fr"
        }
      ]
    }
  }
```
