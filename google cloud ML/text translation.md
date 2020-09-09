## Text Translation with Tranlation API

- Input: translation-request.json 
  ```
    {
      "q": "your_text_here",
      "target": "en"
    }
  ```

- API call
  ```
    curl -s -X POST 
          -H "Content-Type: application/json" 
          --data-binary @translation-request.json 
          https://translation.googleapis.com/language/translate/v2?key=${API_KEY} 
          -o translation-response.json
  ```
