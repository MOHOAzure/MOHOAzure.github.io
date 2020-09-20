# Classify a news article 
  * find categories for the article with Language API
  
### Environment
GCP > Compute Engine> VM instances

### Input
* request.json
```json
{
  "document":{
    "type":"PLAIN_TEXT",
    "content":"A Smoky Lobster Salad With a Tapa Twist. This spin on the Spanish pulpo a la gallega skips the octopus, but keeps the sea salt, olive oil, pimentón and boiled potatoes."
  }
}
```
### API call
```
curl "https://language.googleapis.com/v1/documents:classifyText?key=${API_KEY}" \
      -s -X POST -H "Content-Type: application/json" --data-binary @request.json > response.json
```

### Output
* response.json
```json
{
  "categories": [
    {
      "name": "/Food & Drink/Cooking & Recipes",
      "confidence": 0.85
    },
    {
      "name": "/Food & Drink/Food/Meat & Seafood",
      "confidence": 0.63
    }
  ]
}
```
* Two categories are returned
   * "/Food & Drink/Cooking & Recipes"
   * "/Food & Drink/Food/Meat & Seafood"
* Content Categories: https://cloud.google.com/natural-language/docs/categories
