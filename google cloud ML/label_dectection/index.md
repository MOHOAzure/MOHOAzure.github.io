# Label detection with Vision API

## input img
![](https://i.imgur.com/Tmn3eul.jpg)

## input: request.json
```
{
  "requests": [
    {
      "features": [
        {
          "type": "LABEL_DETECTION"
        }
      ],
      "image": {
        "source": {
          "imageUri": "gs://MY_BUCKET/demo-image.jpg"
        }
      }
    }
  ]
}
```

## API call
There are many types of ```image``` detection, label, face, landmark, text...etc.
![](https://i.imgur.com/ww4GYf7.png)

## output: response.json
```
{
  "responses": [
    {
      "labelAnnotations": [
        {
          "mid": "/m/06mf6",
          "description": "Rabbit",
          "score": 0.9785983,
          "topicality": 0.9785983
        },
        {
          "mid": "/m/06bs13",
          "description": "Domestic rabbit",
          "score": 0.96371055,
          "topicality": 0.96371055
        },
        {
          "mid": "/m/019dxh",
          "description": "Rabbits and Hares",
          "score": 0.95626986,
          "topicality": 0.95626986
        },
        {
          "mid": "/m/0cx37",
          "description": "Hare",
          "score": 0.8675565,
          "topicality": 0.8675565
        },
        {
          "mid": "/m/01l7qd",
          "description": "Whiskers",
          "score": 0.8448266,
          "topicality": 0.8448266
        },
        {
          "mid": "/m/0cpfn",
          "description": "Easter bunny",
          "score": 0.7117864,
          "topicality": 0.7117864
        },
        {
          "mid": "/m/01jjd7",
          "description": "Snowshoe hare",
          "score": 0.6552328,
          "topicality": 0.6552328
        },
        {
          "mid": "/m/06z_nw",
          "description": "Tail",
          "score": 0.6138409,
          "topicality": 0.6138409
        }
      ]
    }
  ]
}

```
