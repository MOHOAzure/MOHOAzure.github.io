## Text detection with Vision API


### Input: 
* Image

![](https://i.imgur.com/UMCdqTY.png)

* ocr-request.json
```json
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
  
### API call
```
  curl -s -X POST 
        -H "Content-Type: application/json" 
        --data-binary @ocr-request.json 
        https://vision.googleapis.com/v1/images:annotate?key=${API_KEY}
        -o orc-response.json
```

### Output
* orc-response.json
```json
{
  "responses": [
    {
      "textAnnotations": [
        {
          "locale": "en",
          "description": "Please use\nHand Sanitiser\n",
          "boundingPoly": {
            "vertices": [
              {
                "x": 32,
                "y": 349
              },
              {
                "x": 280,
                "y": 349
              },
              {
                "x": 280,
                "y": 419
              },
              {
                "x": 32,
                "y": 419
              }
            ]
          }
        },
        {
          "description": "Please",
          "boundingPoly": {
            "vertices": [
              {
                "x": 66,
                "y": 349
              },
              {
                "x": 176,
                "y": 352
              },
              {
                "x": 175,
                "y": 378
              },
              {
                "x": 65,
                "y": 375
              }
            ]
          }
        },
        {
          "description": "use",
          "boundingPoly": {
            "vertices": [
              {
                "x": 189,
                "y": 356
              },
              {
                "x": 247,
                "y": 358
              },
              {
                "x": 246,
                "y": 377
              },
              {
                "x": 188,
                "y": 375
              }
            ]
          }
        },
        {
          "description": "Hand",
          "boundingPoly": {
            "vertices": [
              {
                "x": 32,
                "y": 393
              },
              {
                "x": 118,
                "y": 393
              },
              {
                "x": 118,
                "y": 419
              },
              {
                "x": 32,
                "y": 419
              }
            ]
          }
        },
        {
          "description": "Sanitiser",
          "boundingPoly": {
            "vertices": [
              {
                "x": 132,
                "y": 393
              },
              {
                "x": 280,
                "y": 393
              },
              {
                "x": 280,
                "y": 418
              },
              {
                "x": 132,
                "y": 418
              }
            ]
          }
        }
      ],
      "fullTextAnnotation": {
        "pages": [
          {
            "property": {
              "detectedLanguages": [
                {
                  "languageCode": "en",
                  "confidence": 1
                }
              ]
            },
            "width": 313,
            "height": 450,
            "blocks": [
              {
                "property": {
                  "detectedLanguages": [
                    {
                      "languageCode": "en",
                      "confidence": 1
                    }
                  ]
                },
                "boundingBox": {
                  "vertices": [
                    {
                      "x": 66,
                      "y": 349
                    },
                    {
                      "x": 247,
                      "y": 354
                    },
                    {
                      "x": 246,
                      "y": 380
                    },
                    {
                      "x": 65,
                      "y": 375
                    }
                  ]
                },
                "paragraphs": [
                  {
                    "property": {
                      "detectedLanguages": [
                        {
                          "languageCode": "en",
                          "confidence": 1
                        }
                      ]
                    },
                    "boundingBox": {
                      "vertices": [
                        {
                          "x": 66,
                          "y": 349
                        },
                        {
                          "x": 247,
                          "y": 354
                        },
                        {
                          "x": 246,
                          "y": 380
                        },
                        {
                          "x": 65,
                          "y": 375
                        }
                      ]
                    },
                    "words": [
                      {
                        "property": {
                          "detectedLanguages": [
                            {
                              "languageCode": "en"
                            }
                          ]
                        },
                        "boundingBox": {
                          "vertices": [
                            {
                              "x": 66,
                              "y": 349
                            },
                            {
                              "x": 176,
                              "y": 352
                            },
                            {
                              "x": 175,
                              "y": 378
                            },
                            {
                              "x": 65,
                              "y": 375
                            }
                          ]
                        },
                        "symbols": [
                          {
                            "property": {
                              "detectedLanguages": [
                                {
                                  "languageCode": "en"
                                }
                              ]
                            },
                            "boundingBox": {
                              "vertices": [
                                {
                                  "x": 66,
                                  "y": 349
                                },
                                {
                                  "x": 85,
                                  "y": 350
                                },
                                {
                                  "x": 84,
                                  "y": 376
                                },
                                {
                                  "x": 65,
                                  "y": 375
                                }
                              ]
                            },
                            "text": "P"
                          },
                          {
                            "property": {
                              "detectedLanguages": [
                                {
                                  "languageCode": "en"
                                }
                              ]
                            },
                            "boundingBox": {
                              "vertices": [
                                {
                                  "x": 89,
                                  "y": 350
                                },
                                {
                                  "x": 94,
                                  "y": 350
                                },
                                {
                                  "x": 93,
                                  "y": 375
                                },
                                {
                                  "x": 88,
                                  "y": 375
                                }
                              ]
                            },
                            "text": "l"
                          },
                          {
                            "property": {
                              "detectedLanguages": [
                                {
                                  "languageCode": "en"
                                }
                              ]
                            },
                            "boundingBox": {
                              "vertices": [
                                {
                                  "x": 98,
                                  "y": 357
                                },
                                {
                                  "x": 115,
                                  "y": 358
                                },
                                {
                                  "x": 114,
                                  "y": 375
                                },
                                {
                                  "x": 97,
                                  "y": 374
                                }
                              ]
                            },
                            "text": "e"
                          },
                          {
                            "property": {
                              "detectedLanguages": [
                                {
                                  "languageCode": "en"
                                }
                              ]
                            },
                            "boundingBox": {
                              "vertices": [
                                {
                                  "x": 119,
                                  "y": 357
                                },
                                {
                                  "x": 136,
                                  "y": 358
                                },
                                {
                                  "x": 135,
                                  "y": 376
                                },
                                {
                                  "x": 118,
                                  "y": 375
                                }
                              ]
                            },
                            "text": "a"
                          },
                          {
                            "property": {
                              "detectedLanguages": [
                                {
                                  "languageCode": "en"
                                }
                              ]
                            },
                            "boundingBox": {
                              "vertices": [
                                {
                                  "x": 139,
                                  "y": 356
                                },
                                {
                                  "x": 155,
                                  "y": 356
                                },
                                {
                                  "x": 154,
                                  "y": 374
                                },
                                {
                                  "x": 138,
                                  "y": 374
                                }
                              ]
                            },
                            "text": "s"
                          },
                          {
                            "property": {
                              "detectedLanguages": [
                                {
                                  "languageCode": "en"
                                }
                              ],
                              "detectedBreak": {
                                "type": "SPACE"
                              }
                            },
                            "boundingBox": {
                              "vertices": [
                                {
                                  "x": 159,
                                  "y": 357
                                },
                                {
                                  "x": 176,
                                  "y": 358
                                },
                                {
                                  "x": 175,
                                  "y": 376
                                },
                                {
                                  "x": 158,
                                  "y": 375
                                }
                              ]
                            },
                            "text": "e"
                          }
                        ]
                      },
                      {
                        "property": {
                          "detectedLanguages": [
                            {
                              "languageCode": "en"
                            }
                          ]
                        },
                        "boundingBox": {
                          "vertices": [
                            {
                              "x": 189,
                              "y": 356
                            },
                            {
                              "x": 247,
                              "y": 358
                            },
                            {
                              "x": 246,
                              "y": 377
                            },
                            {
                              "x": 188,
                              "y": 375
                            }
                          ]
                        },
                        "symbols": [
                          {
                            "property": {
                              "detectedLanguages": [
                                {
                                  "languageCode": "en"
                                }
                              ]
                            },
                            "boundingBox": {
                              "vertices": [
                                {
                                  "x": 189,
                                  "y": 357
                                },
                                {
                                  "x": 206,
                                  "y": 358
                                },
                                {
                                  "x": 205,
                                  "y": 376
                                },
                                {
                                  "x": 188,
                                  "y": 375
                                }
                              ]
                            },
                            "text": "u"
                          },
                          {
                            "property": {
                              "detectedLanguages": [
                                {
                                  "languageCode": "en"
                                }
                              ]
                            },
                            "boundingBox": {
                              "vertices": [
                                {
                                  "x": 211,
                                  "y": 357
                                },
                                {
                                  "x": 227,
                                  "y": 357
                                },
                                {
                                  "x": 226,
                                  "y": 375
                                },
                                {
                                  "x": 210,
                                  "y": 375
                                }
                              ]
                            },
                            "text": "s"
                          },
                          {
                            "property": {
                              "detectedLanguages": [
                                {
                                  "languageCode": "en"
                                }
                              ],
                              "detectedBreak": {
                                "type": "LINE_BREAK"
                              }
                            },
                            "boundingBox": {
                              "vertices": [
                                {
                                  "x": 230,
                                  "y": 357
                                },
                                {
                                  "x": 247,
                                  "y": 358
                                },
                                {
                                  "x": 246,
                                  "y": 375
                                },
                                {
                                  "x": 229,
                                  "y": 374
                                }
                              ]
                            },
                            "text": "e"
                          }
                        ]
                      }
                    ]
                  }
                ],
                "blockType": "TEXT"
              },
              {
                "property": {
                  "detectedLanguages": [
                    {
                      "languageCode": "en",
                      "confidence": 1
                    }
                  ]
                },
                "boundingBox": {
                  "vertices": [
                    {
                      "x": 32,
                      "y": 393
                    },
                    {
                      "x": 280,
                      "y": 393
                    },
                    {
                      "x": 280,
                      "y": 419
                    },
                    {
                      "x": 32,
                      "y": 419
                    }
                  ]
                },
                "paragraphs": [
                  {
                    "property": {
                      "detectedLanguages": [
                        {
                          "languageCode": "en",
                          "confidence": 1
                        }
                      ]
                    },
                    "boundingBox": {
                      "vertices": [
                        {
                          "x": 32,
                          "y": 393
                        },
                        {
                          "x": 280,
                          "y": 393
                        },
                        {
                          "x": 280,
                          "y": 419
                        },
                        {
                          "x": 32,
                          "y": 419
                        }
                      ]
                    },
                    "words": [
                      {
                        "property": {
                          "detectedLanguages": [
                            {
                              "languageCode": "en"
                            }
                          ]
                        },
                        "boundingBox": {
                          "vertices": [
                            {
                              "x": 32,
                              "y": 393
                            },
                            {
                              "x": 118,
                              "y": 393
                            },
                            {
                              "x": 118,
                              "y": 419
                            },
                            {
                              "x": 32,
                              "y": 419
                            }
                          ]
                        },
                        "symbols": [
                          {
                            "property": {
                              "detectedLanguages": [
                                {
                                  "languageCode": "en"
                                }
                              ]
                            },
                            "boundingBox": {
                              "vertices": [
                                {
                                  "x": 32,
                                  "y": 393
                                },
                                {
                                  "x": 53,
                                  "y": 393
                                },
                                {
                                  "x": 53,
                                  "y": 418
                                },
                                {
                                  "x": 32,
                                  "y": 418
                                }
                              ]
                            },
                            "text": "H"
                          },
                          {
                            "property": {
                              "detectedLanguages": [
                                {
                                  "languageCode": "en"
                                }
                              ]
                            },
                            "boundingBox": {
                              "vertices": [
                                {
                                  "x": 58,
                                  "y": 400
                                },
                                {
                                  "x": 75,
                                  "y": 400
                                },
                                {
                                  "x": 75,
                                  "y": 418
                                },
                                {
                                  "x": 58,
                                  "y": 418
                                }
                              ]
                            },
                            "text": "a"
                          },
                          {
                            "property": {
                              "detectedLanguages": [
                                {
                                  "languageCode": "en"
                                }
                              ]
                            },
                            "boundingBox": {
                              "vertices": [
                                {
                                  "x": 80,
                                  "y": 400
                                },
                                {
                                  "x": 97,
                                  "y": 400
                                },
                                {
                                  "x": 97,
                                  "y": 418
                                },
                                {
                                  "x": 80,
                                  "y": 418
                                }
                              ]
                            },
                            "text": "n"
                          },
                          {
                            "property": {
                              "detectedLanguages": [
                                {
                                  "languageCode": "en"
                                }
                              ],
                              "detectedBreak": {
                                "type": "SPACE"
                              }
                            },
                            "boundingBox": {
                              "vertices": [
                                {
                                  "x": 100,
                                  "y": 393
                                },
                                {
                                  "x": 118,
                                  "y": 393
                                },
                                {
                                  "x": 118,
                                  "y": 419
                                },
                                {
                                  "x": 100,
                                  "y": 419
                                }
                              ]
                            },
                            "text": "d"
                          }
                        ]
                      },
                      {
                        "property": {
                          "detectedLanguages": [
                            {
                              "languageCode": "en"
                            }
                          ]
                        },
                        "boundingBox": {
                          "vertices": [
                            {
                              "x": 132,
                              "y": 393
                            },
                            {
                              "x": 280,
                              "y": 393
                            },
                            {
                              "x": 280,
                              "y": 418
                            },
                            {
                              "x": 132,
                              "y": 418
                            }
                          ]
                        },
                        "symbols": [
                          {
                            "property": {
                              "detectedLanguages": [
                                {
                                  "languageCode": "en"
                                }
                              ]
                            },
                            "boundingBox": {
                              "vertices": [
                                {
                                  "x": 132,
                                  "y": 393
                                },
                                {
                                  "x": 153,
                                  "y": 393
                                },
                                {
                                  "x": 153,
                                  "y": 418
                                },
                                {
                                  "x": 132,
                                  "y": 418
                                }
                              ]
                            },
                            "text": "S"
                          },
                          {
                            "property": {
                              "detectedLanguages": [
                                {
                                  "languageCode": "en"
                                }
                              ]
                            },
                            "boundingBox": {
                              "vertices": [
                                {
                                  "x": 155,
                                  "y": 400
                                },
                                {
                                  "x": 172,
                                  "y": 400
                                },
                                {
                                  "x": 172,
                                  "y": 418
                                },
                                {
                                  "x": 155,
                                  "y": 418
                                }
                              ]
                            },
                            "text": "a"
                          },
                          {
                            "property": {
                              "detectedLanguages": [
                                {
                                  "languageCode": "en"
                                }
                              ]
                            },
                            "boundingBox": {
                              "vertices": [
                                {
                                  "x": 177,
                                  "y": 400
                                },
                                {
                                  "x": 194,
                                  "y": 400
                                },
                                {
                                  "x": 194,
                                  "y": 418
                                },
                                {
                                  "x": 177,
                                  "y": 418
                                }
                              ]
                            },
                            "text": "n"
                          },
                          {
                            "property": {
                              "detectedLanguages": [
                                {
                                  "languageCode": "en"
                                }
                              ]
                            },
                            "boundingBox": {
                              "vertices": [
                                {
                                  "x": 198,
                                  "y": 393
                                },
                                {
                                  "x": 202,
                                  "y": 393
                                },
                                {
                                  "x": 202,
                                  "y": 418
                                },
                                {
                                  "x": 198,
                                  "y": 418
                                }
                              ]
                            },
                            "text": "i"
                          },
                          {
                            "property": {
                              "detectedLanguages": [
                                {
                                  "languageCode": "en"
                                }
                              ]
                            },
                            "boundingBox": {
                              "vertices": [
                                {
                                  "x": 205,
                                  "y": 394
                                },
                                {
                                  "x": 216,
                                  "y": 394
                                },
                                {
                                  "x": 216,
                                  "y": 418
                                },
                                {
                                  "x": 205,
                                  "y": 418
                                }
                              ]
                            },
                            "text": "t"
                          },
                          {
                            "property": {
                              "detectedLanguages": [
                                {
                                  "languageCode": "en"
                                }
                              ]
                            },
                            "boundingBox": {
                              "vertices": [
                                {
                                  "x": 220,
                                  "y": 393
                                },
                                {
                                  "x": 224,
                                  "y": 393
                                },
                                {
                                  "x": 224,
                                  "y": 418
                                },
                                {
                                  "x": 220,
                                  "y": 418
                                }
                              ]
                            },
                            "text": "i"
                          },
                          {
                            "property": {
                              "detectedLanguages": [
                                {
                                  "languageCode": "en"
                                }
                              ]
                            },
                            "boundingBox": {
                              "vertices": [
                                {
                                  "x": 228,
                                  "y": 400
                                },
                                {
                                  "x": 245,
                                  "y": 400
                                },
                                {
                                  "x": 245,
                                  "y": 418
                                },
                                {
                                  "x": 228,
                                  "y": 418
                                }
                              ]
                            },
                            "text": "s"
                          },
                          {
                            "property": {
                              "detectedLanguages": [
                                {
                                  "languageCode": "en"
                                }
                              ]
                            },
                            "boundingBox": {
                              "vertices": [
                                {
                                  "x": 248,
                                  "y": 400
                                },
                                {
                                  "x": 266,
                                  "y": 400
                                },
                                {
                                  "x": 266,
                                  "y": 418
                                },
                                {
                                  "x": 248,
                                  "y": 418
                                }
                              ]
                            },
                            "text": "e"
                          },
                          {
                            "property": {
                              "detectedLanguages": [
                                {
                                  "languageCode": "en"
                                }
                              ],
                              "detectedBreak": {
                                "type": "LINE_BREAK"
                              }
                            },
                            "boundingBox": {
                              "vertices": [
                                {
                                  "x": 269,
                                  "y": 400
                                },
                                {
                                  "x": 280,
                                  "y": 400
                                },
                                {
                                  "x": 280,
                                  "y": 418
                                },
                                {
                                  "x": 269,
                                  "y": 418
                                }
                              ]
                            },
                            "text": "r"
                          }
                        ]
                      }
                    ]
                  }
                ],
                "blockType": "TEXT"
              }
            ]
          }
        ],
        "text": "Please use\nHand Sanitiser\n"
      }
    }
  ]
}
```
