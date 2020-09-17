# Landmark annotation

## Image
https://cdn.qwiklabs.com/%2Fv47QS0KOC28%2F03bZx0R%2FO0iLLvtYQUOZyvnjIfz%2BIE%3D

## Request
```json
{
  "requests": [
      {
        "image": {
          "source": {
              "gcsImageUri": "gs://{bucket}/city.png"
          }
        },
        "features": [
          {
            "type": "LANDMARK_DETECTION",
            "maxResults": 10,
          }
        ]
      }
  ]
}
```

## API call
```
curl -s -X POST -H "Content-Type: application/json" --data-binary @request.json  https://vision.googleapis.com/v1/images:annotate?key=${API_KEY} -o response.json
```

## Response
```json
{
  "responses": [
    {
      "landmarkAnnotations": [
        {
          "mid": "/m/041cp3",
          "description": "Boston",
          "score": 0.74245083,
          "boundingPoly": {
            "vertices": [
              {
                "y": 553
              },
              {
                "x": 969,
                "y": 553
              },
              {
                "x": 969,
                "y": 1122
              },
              {
                "y": 1122
              }
            ]
          },
          "locations": [
            {
              "latLng": {
                "latitude": 42.359637,
                "longitude": -71.080942
              }
            }
          ]
        }
      ]
    }
  ]
}
```
