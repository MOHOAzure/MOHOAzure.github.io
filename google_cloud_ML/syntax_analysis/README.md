# Syntax analysis
* with analyzeSyntax API
  * Extract tokens and sentences, identify parts of speech (PoS) and create dependency parse trees for each sentence.
  * [DependencyEdge](#dependencyEdge)
* with analyzeEntities API
  * [Automatic language detection](#automatic-language-detection)

### Input: request.json

```json
{
  "document":{
    "type":"PLAIN_TEXT",
    "content": "Joanne Rowling is a British novelist, screenwriter and film producer."
  },
  "encodingType": "UTF8"
}
```

### API call
```
curl "https://language.googleapis.com/v1/documents:analyzeSyntax?key=${API_KEY}" \
  -s -X POST -H "Content-Type: application/json" --data-binary @request.json
```

### Output
```json
{
  "text": {
    "content": "is",
    "beginOffset": 15
  },
  "partOfSpeech": {
    "tag": "VERB",
    "aspect": "ASPECT_UNKNOWN",
    "case": "CASE_UNKNOWN",
    "form": "FORM_UNKNOWN",
    "gender": "GENDER_UNKNOWN",
    "mood": "INDICATIVE",
    "number": "SINGULAR",
    "person": "THIRD",
    "proper": "PROPER_UNKNOWN",
    "reciprocity": "RECIPROCITY_UNKNOWN",
    "tense": "PRESENT",
    "voice": "VOICE_UNKNOWN"
  },
  "dependencyEdge": {
    "headTokenIndex": 2,
    "label": "ROOT"
  },
  "lemma": "be"
}
 ```
 * lemma: the canonical form of the word. For example, the words run, runs, ran, and running all have a lemma of run. The lemma value is useful for tracking occurrences of a word in a large piece of text over time.
 * dependencyEdge: includes data that you can use to create a dependency parse tree of the text
  * create dependency parse trees in the browser with the Natural Language demo available: https://cloud.google.com/natural-language
    
## Automatic language detection

### Input: request.json
* No language is specified
```json
{
  "document":{
    "type":"PLAIN_TEXT",
    "content":"日本のグーグルのオフィスは、東京の六本木ヒルズにあります"
  }
}
```

### API call
```
curl "https://language.googleapis.com/v1/documents:analyzeEntities?key=${API_KEY}" \
  -s -X POST -H "Content-Type: application/json" --data-binary @request.json
```

### Output
```json
{
  "entities": [
    {
      "name": "日本",
      "type": "LOCATION",
      "metadata": {
        "mid": "/m/03_3d",
        "wikipedia_url": "https://en.wikipedia.org/wiki/Japan"
      },
      "salience": 0.23854347,
      "mentions": [
        {
          "text": {
            "content": "日本",
            "beginOffset": 0
          },
          "type": "PROPER"
        }
      ]
    },
    {
      "name": "グーグル",
      "type": "ORGANIZATION",
      "metadata": {
        "mid": "/m/045c7b",
        "wikipedia_url": "https://en.wikipedia.org/wiki/Google"
      },
      "salience": 0.21155767,
      "mentions": [
        {
          "text": {
            "content": "グーグル",
            "beginOffset": 9
          },
          "type": "PROPER"
        }
      ]
    },
    ...
  ]
  "language": "ja"
}
 ```
