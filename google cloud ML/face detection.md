# Face detection with Vision API

  * position of face (head & skin)
  * direction & angle of eyes
  * mood (joy, sorrow, anger, and surprise.)
  * head wear

## Face image
![](https://cdn.qwiklabs.com/5%2FxwpTRxehGuIRhCz3exglbWOzueKIPikyYj0Rx82L0%3D)

## Request.json
```json
{
  "requests": [
      {
        "image": {
          "source": {
              "gcsImageUri": "gs://{Bucket}/{Image}"
          }
        },
        "features": [
          {
            "type": "FACE_DETECTION"
          },
          {
            "type": "LANDMARK_DETECTION"
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
      "faceAnnotations": [
        {
          "boundingPoly": {
            "vertices": [
              {
                "x": 81,
                "y": 416
              },
              {
                "x": 464,
                "y": 416
              },
              {
                "x": 464,
                "y": 861
              },
              {
                "x": 81,
                "y": 861
              }
            ]
          },
          "fdBoundingPoly": {
            "vertices": [
              {
                "x": 115,
                "y": 504
              },
              {
                "x": 434,
                "y": 504
              },
              {
                "x": 434,
                "y": 836
              },
              {
                "x": 115,
                "y": 836
              }
            ]
          },
          "landmarks": [
            {
              "type": "LEFT_EYE",
              "position": {
                "x": 212.73776,
                "y": 637.61145,
                "z": 0.00029802322
              }
            },
            {
              "type": "RIGHT_EYE",
              "position": {
                "x": 335.2642,
                "y": 641.00305,
                "z": 5.573952
              }
            },
            {
              "type": "LEFT_OF_LEFT_EYEBROW",
              "position": {
                "x": 177.11182,
                "y": 604.2706,
                "z": 7.009534
              }
            },
            {
              "type": "RIGHT_OF_LEFT_EYEBROW",
              "position": {
                "x": 251.46878,
                "y": 607.5896,
                "z": -21.810808
              }
            },
            {
              "type": "LEFT_OF_RIGHT_EYEBROW",
              "position": {
                "x": 303.50146,
                "y": 611.4801,
                "z": -19.324194
              }
            },
            {
              "type": "RIGHT_OF_RIGHT_EYEBROW",
              "position": {
                "x": 370.41568,
                "y": 615.5546,
                "z": 15.453682
              }
            },
            {
              "type": "MIDPOINT_BETWEEN_EYES",
              "position": {
                "x": 278.60126,
                "y": 635.5503,
                "z": -20.568476
              }
            },
            {
              "type": "NOSE_TIP",
              "position": {
                "x": 275.48404,
                "y": 707.4824,
                "z": -49.34061
              }
            },
            {
              "type": "UPPER_LIP",
              "position": {
                "x": 277.9937,
                "y": 748.0686,
                "z": -20.841455
              }
            },
            {
              "type": "LOWER_LIP",
              "position": {
                "x": 276.43826,
                "y": 789.02386,
                "z": -10.225104
              }
            },
            {
              "type": "MOUTH_LEFT",
              "position": {
                "x": 218.25475,
                "y": 750.4097,
                "z": 8.975543
              }
            },
            {
              "type": "MOUTH_RIGHT",
              "position": {
                "x": 325.76215,
                "y": 754.8611,
                "z": 13.403287
              }
            },
            {
              "type": "MOUTH_CENTER",
              "position": {
                "x": 272.4912,
                "y": 767.07587,
                "z": -11.387869
              }
            },
            {
              "type": "NOSE_BOTTOM_RIGHT",
              "position": {
                "x": 311.55426,
                "y": 712.9132,
                "z": -5.3069224
              }
            },
            {
              "type": "NOSE_BOTTOM_LEFT",
              "position": {
                "x": 243.9779,
                "y": 713.79895,
                "z": -8.261453
              }
            },
            {
              "type": "NOSE_BOTTOM_CENTER",
              "position": {
                "x": 277.9556,
                "y": 725.87946,
                "z": -22.868422
              }
            },
            {
              "type": "LEFT_EYE_TOP_BOUNDARY",
              "position": {
                "x": 211.98752,
                "y": 625.9721,
                "z": -7.005327
              }
            },
            {
              "type": "LEFT_EYE_RIGHT_CORNER",
              "position": {
                "x": 238.52759,
                "y": 639.5389,
                "z": 1.3185911
              }
            },
            {
              "type": "LEFT_EYE_BOTTOM_BOUNDARY",
              "position": {
                "x": 210.61955,
                "y": 647.08545,
                "z": -0.7931818
              }
            },
            {
              "type": "LEFT_EYE_LEFT_CORNER",
              "position": {
                "x": 185.97226,
                "y": 634.2046,
                "z": 9.1281395
              }
            },
            {
              "type": "RIGHT_EYE_TOP_BOUNDARY",
              "position": {
                "x": 335.71545,
                "y": 631.9429,
                "z": -1.5540969
              }
            },
            {
              "type": "RIGHT_EYE_RIGHT_CORNER",
              "position": {
                "x": 355.54373,
                "y": 639.00116,
                "z": 17.079428
              }
            },
            {
              "type": "RIGHT_EYE_BOTTOM_BOUNDARY",
              "position": {
                "x": 335.26404,
                "y": 650.6216,
                "z": 5.031595
              }
            },
            {
              "type": "RIGHT_EYE_LEFT_CORNER",
              "position": {
                "x": 311.13217,
                "y": 643.2319,
                "z": 4.565236
              }
            },
            {
              "type": "LEFT_EYEBROW_UPPER_MIDPOINT",
              "position": {
                "x": 214.00592,
                "y": 594.7385,
                "z": -15.236333
              }
            },
            {
              "type": "RIGHT_EYEBROW_UPPER_MIDPOINT",
              "position": {
                "x": 337.42657,
                "y": 604.12067,
                "z": -9.701122
              }
            },
            {
              "type": "LEFT_EAR_TRAGION",
              "position": {
                "x": 148.29941,
                "y": 668.1025,
                "z": 141.19771
              }
            },
            {
              "type": "RIGHT_EAR_TRAGION",
              "position": {
                "x": 398.31378,
                "y": 666.1978,
                "z": 152.92099
              }
            },
            {
              "type": "FOREHEAD_GLABELLA",
              "position": {
                "x": 279.14954,
                "y": 610.55914,
                "z": -24.45984
              }
            },
            {
              "type": "CHIN_GNATHION",
              "position": {
                "x": 275.09244,
                "y": 843.56964,
                "z": 9.367683
              }
            },
            {
              "type": "CHIN_LEFT_GONION",
              "position": {
                "x": 167.86584,
                "y": 764.0309,
                "z": 101.26094
              }
            },
            {
              "type": "CHIN_RIGHT_GONION",
              "position": {
                "x": 372.63174,
                "y": 765.0617,
                "z": 111.3148
              }
            },
            {
              "type": "LEFT_CHEEK_CENTER",
              "position": {
                "x": 184.56105,
                "y": 708.38934,
                "z": 14.806209
              }
            },
            {
              "type": "RIGHT_CHEEK_CENTER",
              "position": {
                "x": 352.4706,
                "y": 713.5617,
                "z": 22.495564
              }
            }
          ],
          "rollAngle": 1.0361501,
          "panAngle": 2.6743894,
          "tiltAngle": -4.6711164,
          "detectionConfidence": 0.87700474,
          "landmarkingConfidence": 0.69365203,
          "joyLikelihood": "VERY_LIKELY",
          "sorrowLikelihood": "VERY_UNLIKELY",
          "angerLikelihood": "VERY_UNLIKELY",
          "surpriseLikelihood": "VERY_UNLIKELY",
          "underExposedLikelihood": "VERY_UNLIKELY",
          "blurredLikelihood": "VERY_UNLIKELY",
          "headwearLikelihood": "VERY_LIKELY"
        },
        {
          "boundingPoly": {
            "vertices": [
              {
                "x": 744,
                "y": 448
              },
              {
                "x": 893,
                "y": 448
              },
              {
                "x": 893,
                "y": 621
              },
              {
                "x": 744,
                "y": 621
              }
            ]
          },
          "fdBoundingPoly": {
            "vertices": [
              {
                "x": 751,
                "y": 482
              },
              {
                "x": 880,
                "y": 482
              },
              {
                "x": 880,
                "y": 613
              },
              {
                "x": 751,
                "y": 613
              }
            ]
          },
          "landmarks": [
            {
              "type": "LEFT_EYE",
              "position": {
                "x": 793.36646,
                "y": 538.8087,
                "z": -0.00016593933
              }
            },
            {
              "type": "RIGHT_EYE",
              "position": {
                "x": 840.57684,
                "y": 535.4766,
                "z": -1.4707587
              }
            },
            {
              "type": "LEFT_OF_LEFT_EYEBROW",
              "position": {
                "x": 776.07,
                "y": 529.87225,
                "z": 2.9542015
              }
            },
            {
              "type": "RIGHT_OF_LEFT_EYEBROW",
              "position": {
                "x": 804.22174,
                "y": 527.1903,
                "z": -9.582684
              }
            },
            {
              "type": "LEFT_OF_RIGHT_EYEBROW",
              "position": {
                "x": 827.3257,
                "y": 525.94653,
                "z": -10.290566
              }
            },
            {
              "type": "RIGHT_OF_RIGHT_EYEBROW",
              "position": {
                "x": 855.11816,
                "y": 523.2592,
                "z": 0.48041594
              }
            },
            {
              "type": "MIDPOINT_BETWEEN_EYES",
              "position": {
                "x": 816.7482,
                "y": 536.5924,
                "z": -9.402968
              }
            },
            {
              "type": "NOSE_TIP",
              "position": {
                "x": 819.32227,
                "y": 566.0572,
                "z": -18.495546
              }
            },
            {
              "type": "UPPER_LIP",
              "position": {
                "x": 820.58765,
                "y": 576.6085,
                "z": -7.1422668
              }
            },
            {
              "type": "LOWER_LIP",
              "position": {
                "x": 822.50616,
                "y": 592.66376,
                "z": -2.279512
              }
            },
            {
              "type": "MOUTH_LEFT",
              "position": {
                "x": 801.74817,
                "y": 580.04614,
                "z": 5.4872465
              }
            },
            {
              "type": "MOUTH_RIGHT",
              "position": {
                "x": 841.2767,
                "y": 576.1774,
                "z": 4.2747483
              }
            },
            {
              "type": "MOUTH_CENTER",
              "position": {
                "x": 821.5133,
                "y": 584.32837,
                "z": -3.1963942
              }
            },
            {
              "type": "NOSE_BOTTOM_RIGHT",
              "position": {
                "x": 830.8554,
                "y": 563.1985,
                "z": -2.9975238
              }
            },
            {
              "type": "NOSE_BOTTOM_LEFT",
              "position": {
                "x": 806.134,
                "y": 565.17334,
                "z": -2.265707
              }
            },
            {
              "type": "NOSE_BOTTOM_CENTER",
              "position": {
                "x": 819.898,
                "y": 569.88544,
                "z": -8.313124
              }
            },
            {
              "type": "LEFT_EYE_TOP_BOUNDARY",
              "position": {
                "x": 793.3739,
                "y": 534.1215,
                "z": -2.765633
              }
            },
            {
              "type": "LEFT_EYE_RIGHT_CORNER",
              "position": {
                "x": 803.92285,
                "y": 538.83746,
                "z": -0.2039237
              }
            },
            {
              "type": "LEFT_EYE_BOTTOM_BOUNDARY",
              "position": {
                "x": 794.0392,
                "y": 542.12134,
                "z": -0.016411304
              }
            },
            {
              "type": "LEFT_EYE_LEFT_CORNER",
              "position": {
                "x": 784.62085,
                "y": 538.71265,
                "z": 4.0873756
              }
            },
            {
              "type": "RIGHT_EYE_TOP_BOUNDARY",
              "position": {
                "x": 840.34106,
                "y": 531.7333,
                "z": -4.2691064
              }
            },
            {
              "type": "RIGHT_EYE_RIGHT_CORNER",
              "position": {
                "x": 849.7481,
                "y": 534.1355,
                "z": 1.9940851
              }
            },
            {
              "type": "RIGHT_EYE_BOTTOM_BOUNDARY",
              "position": {
                "x": 841.41077,
                "y": 538.6904,
                "z": -1.5322165
              }
            },
            {
              "type": "RIGHT_EYE_LEFT_CORNER",
              "position": {
                "x": 831.70483,
                "y": 537.2582,
                "z": -1.0713434
              }
            },
            {
              "type": "LEFT_EYEBROW_UPPER_MIDPOINT",
              "position": {
                "x": 789.55536,
                "y": 524.84326,
                "z": -6.2166595
              }
            },
            {
              "type": "RIGHT_EYEBROW_UPPER_MIDPOINT",
              "position": {
                "x": 840.9385,
                "y": 520.45306,
                "z": -7.902238
              }
            },
            {
              "type": "LEFT_EAR_TRAGION",
              "position": {
                "x": 767.29706,
                "y": 549.66675,
                "z": 54.13513
              }
            },
            {
              "type": "RIGHT_EAR_TRAGION",
              "position": {
                "x": 870.8414,
                "y": 542.36536,
                "z": 50.876396
              }
            },
            {
              "type": "FOREHEAD_GLABELLA",
              "position": {
                "x": 816.1567,
                "y": 527.6034,
                "z": -11.366033
              }
            },
            {
              "type": "CHIN_GNATHION",
              "position": {
                "x": 825.6964,
                "y": 611.0886,
                "z": 6.0557356
              }
            },
            {
              "type": "CHIN_LEFT_GONION",
              "position": {
                "x": 779.8702,
                "y": 586.0331,
                "z": 41.031227
              }
            },
            {
              "type": "CHIN_RIGHT_GONION",
              "position": {
                "x": 865.6094,
                "y": 578.2519,
                "z": 38.30258
              }
            },
            {
              "type": "LEFT_CHEEK_CENTER",
              "position": {
                "x": 787.9758,
                "y": 565.64526,
                "z": 7.7183447
              }
            },
            {
              "type": "RIGHT_CHEEK_CENTER",
              "position": {
                "x": 851.93646,
                "y": 560.8232,
                "z": 5.6799655
              }
            }
          ],
          "rollAngle": -5.2263813,
          "panAngle": -1.931947,
          "tiltAngle": -8.070016,
          "detectionConfidence": 0.90133977,
          "landmarkingConfidence": 0.68975085,
          "joyLikelihood": "VERY_LIKELY",
          "sorrowLikelihood": "VERY_UNLIKELY",
          "angerLikelihood": "VERY_UNLIKELY",
          "surpriseLikelihood": "VERY_UNLIKELY",
          "underExposedLikelihood": "VERY_UNLIKELY",
          "blurredLikelihood": "VERY_UNLIKELY",
          "headwearLikelihood": "VERY_UNLIKELY"
        },
        {
          "boundingPoly": {
            "vertices": [
              {
                "x": 668,
                "y": 321
              },
              {
                "x": 760,
                "y": 321
              },
              {
                "x": 760,
                "y": 428
              },
              {
                "x": 668,
                "y": 428
              }
            ]
          },
          "fdBoundingPoly": {
            "vertices": [
              {
                "x": 666,
                "y": 339
              },
              {
                "x": 746,
                "y": 339
              },
              {
                "x": 746,
                "y": 420
              },
              {
                "x": 666,
                "y": 420
              }
            ]
          },
          "landmarks": [
            {
              "type": "LEFT_EYE",
              "position": {
                "x": 692.45087,
                "y": 373.57657,
                "z": -0.00028324127
              }
            },
            {
              "type": "RIGHT_EYE",
              "position": {
                "x": 717.3673,
                "y": 372.93967,
                "z": -9.603181
              }
            },
            {
              "type": "LEFT_OF_LEFT_EYEBROW",
              "position": {
                "x": 685.0159,
                "y": 365.9884,
                "z": 5.494735
              }
            },
            {
              "type": "RIGHT_OF_LEFT_EYEBROW",
              "position": {
                "x": 696.334,
                "y": 369.05875,
                "z": -7.116223
              }
            },
            {
              "type": "LEFT_OF_RIGHT_EYEBROW",
              "position": {
                "x": 708.63794,
                "y": 366.8848,
                "z": -11.678239
              }
            },
            {
              "type": "RIGHT_OF_RIGHT_EYEBROW",
              "position": {
                "x": 726.1849,
                "y": 366.89743,
                "z": -10.646131
              }
            },
            {
              "type": "MIDPOINT_BETWEEN_EYES",
              "position": {
                "x": 701.9113,
                "y": 373.83392,
                "z": -9.694357
              }
            },
            {
              "type": "NOSE_TIP",
              "position": {
                "x": 697.0528,
                "y": 388.23816,
                "z": -16.3856
              }
            },
            {
              "type": "UPPER_LIP",
              "position": {
                "x": 702.531,
                "y": 399.09467,
                "z": -11.209531
              }
            },
            {
              "type": "LOWER_LIP",
              "position": {
                "x": 700.0595,
                "y": 405.6434,
                "z": -9.240926
              }
            },
            {
              "type": "MOUTH_LEFT",
              "position": {
                "x": 690.0648,
                "y": 401.05698,
                "z": 0.19131327
              }
            },
            {
              "type": "MOUTH_RIGHT",
              "position": {
                "x": 717.0516,
                "y": 400.62897,
                "z": -8.893454
              }
            },
            {
              "type": "MOUTH_CENTER",
              "position": {
                "x": 701.14716,
                "y": 401.98267,
                "z": -9.228721
              }
            },
            {
              "type": "NOSE_BOTTOM_RIGHT",
              "position": {
                "x": 710.58545,
                "y": 391.29868,
                "z": -10.530836
              }
            },
            {
              "type": "NOSE_BOTTOM_LEFT",
              "position": {
                "x": 696.7625,
                "y": 392.0007,
                "z": -5.2680264
              }
            },
            {
              "type": "NOSE_BOTTOM_CENTER",
              "position": {
                "x": 702.5448,
                "y": 393.18262,
                "z": -11.340342
              }
            },
            {
              "type": "LEFT_EYE_TOP_BOUNDARY",
              "position": {
                "x": 692.0619,
                "y": 370.939,
                "z": -1.3013209
              }
            },
            {
              "type": "LEFT_EYE_RIGHT_CORNER",
              "position": {
                "x": 697.57,
                "y": 374.55267,
                "z": -1.9931557
              }
            },
            {
              "type": "LEFT_EYE_BOTTOM_BOUNDARY",
              "position": {
                "x": 691.7622,
                "y": 375.86197,
                "z": -0.13663864
              }
            },
            {
              "type": "LEFT_EYE_LEFT_CORNER",
              "position": {
                "x": 686.6207,
                "y": 372.97644,
                "z": 4.397163
              }
            },
            {
              "type": "RIGHT_EYE_TOP_BOUNDARY",
              "position": {
                "x": 717.6253,
                "y": 370.34143,
                "z": -11.11541
              }
            },
            {
              "type": "RIGHT_EYE_RIGHT_CORNER",
              "position": {
                "x": 723.4173,
                "y": 373.71735,
                "z": -9.48891
              }
            },
            {
              "type": "RIGHT_EYE_BOTTOM_BOUNDARY",
              "position": {
                "x": 717.42334,
                "y": 374.9754,
                "z": -9.926247
              }
            },
            {
              "type": "RIGHT_EYE_LEFT_CORNER",
              "position": {
                "x": 711.87634,
                "y": 373.0256,
                "z": -7.5685062
              }
            },
            {
              "type": "LEFT_EYEBROW_UPPER_MIDPOINT",
              "position": {
                "x": 689.87897,
                "y": 365.2108,
                "z": -2.3199217
              }
            },
            {
              "type": "RIGHT_EYEBROW_UPPER_MIDPOINT",
              "position": {
                "x": 716.734,
                "y": 364.3164,
                "z": -12.677992
              }
            },
            {
              "type": "LEFT_EAR_TRAGION",
              "position": {
                "x": 685.536,
                "y": 382.1659,
                "z": 36.005737
              }
            },
            {
              "type": "RIGHT_EAR_TRAGION",
              "position": {
                "x": 749.43524,
                "y": 381.69644,
                "z": 13.626722
              }
            },
            {
              "type": "FOREHEAD_GLABELLA",
              "position": {
                "x": 701.9201,
                "y": 368.11392,
                "z": -10.230074
              }
            },
            {
              "type": "CHIN_GNATHION",
              "position": {
                "x": 700.5634,
                "y": 420.96875,
                "z": -5.806553
              }
            },
            {
              "type": "CHIN_LEFT_GONION",
              "position": {
                "x": 687.10834,
                "y": 404.76392,
                "z": 23.944067
              }
            },
            {
              "type": "CHIN_RIGHT_GONION",
              "position": {
                "x": 734.93164,
                "y": 406.25705,
                "z": 6.3688693
              }
            },
            {
              "type": "LEFT_CHEEK_CENTER",
              "position": {
                "x": 685.8955,
                "y": 389.75946,
                "z": 4.68425
              }
            },
            {
              "type": "RIGHT_CHEEK_CENTER",
              "position": {
                "x": 723.4291,
                "y": 390.22375,
                "z": -9.150036
              }
            }
          ],
          "rollAngle": 0.15598953,
          "panAngle": -21.293484,
          "tiltAngle": -1.2292432,
          "detectionConfidence": 0.8967814,
          "landmarkingConfidence": 0.43604028,
          "joyLikelihood": "LIKELY",
          "sorrowLikelihood": "VERY_UNLIKELY",
          "angerLikelihood": "VERY_UNLIKELY",
          "surpriseLikelihood": "VERY_UNLIKELY",
          "underExposedLikelihood": "VERY_UNLIKELY",
          "blurredLikelihood": "VERY_UNLIKELY",
          "headwearLikelihood": "VERY_LIKELY"
        }
      ]
    }
  ]
}
```
