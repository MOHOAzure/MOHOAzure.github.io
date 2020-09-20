# Text Translation with Tranlation API

- Pre-condition: [Text detection with Vision API](../text_detection)

### Prepare
Create a request file: translation-request.json 
```
  {
    "q": "your_text_here",
    "target": "en"
  }
```
  
### Parse text extraced by Vision API to the request file
```
STR=$(jq .responses[0].textAnnotations[0].description ocr-response.json) 
  && STR="${STR//\"}" 
  && sed -i "s|your_text_here|$STR|g" translation-request.json
```
    
### Input translation request file
* translation-request.json
```
{
  "q": "Please use
        Hand Sanitiser",
  "target": "zh-TW"
}
```
* ```target```: https://cloud.google.com/translate/docs/languages
    
### API call :
```
curl -s -X POST 
      -H "Content-Type: application/json" 
      --data-binary @translation-request.json 
      https://translation.googleapis.com/language/translate/v2?key=${API_KEY} 
      -o translation-response.json
```

### Output
* translation-response.json
```
{
  "data": {
    "translations": [
      {
        "translatedText": "請使用洗手",
        "detectedSourceLanguage": "en"
      }
    ]
  }
}
```

### Change ```target``` of translation-request.json

target | translatedText |
--- | ---
ja | ハンドサニタイザーをご利用ください
fr | Veuillez utiliser un désinfectant pour les mains
ru | Пожалуйста, используйте дезинфицирующее средство для рук
de | Bitte verwenden Sie Händedesinfektionsmittel
la | Quaeso uti manus Sanitiser
