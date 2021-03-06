# Reid-backend API

## Data Sensor

#### 后端获取sensor捕捉到的包信息，存入数据库
  - URL: http://222.201.137.47:12346/sensor/wifi
  - Type: POST
  - Content-type: x-www-form-urlencoded
  - 参数: 
    - captureTime: 捕获时间，为yyyy-MM-dd hh:mm:ss格式
    - fromSensorId: 传感器id，一个整数，范围[0,2^32)
    - macAddress: 捕捉到的包的mac地址，格式为70:85:c2:3d:c8:eb
    - intensity： 捕捉到的包的信号强度， 范围[-150,150]
  - 返回值:
    - 写入成功
    ```json
    {
        "code": 0,
        "msg": "成功",
        "data": {
            "captureTime": "2017-12-11 07:00:05",
            "fromSensorId": 0,
            "macAddress": "00:11:22:33:44:55:66",
            "intensity": "80"
        }
    }
    ```
    
    - 写入出错(其他接口同理）
    ```json
    {
        "code": -1,
        "msg": "未知错误",
        "data": null
    }
    ```
    
#### 后端获取sensor捕捉到的图片信息，存入数据库(deprecated, see sensor/visionMac)
  - URL: http://222.201.137.47:12346/sensor/vision
  - Type: POST
  - Content-type: application/json
  - 参数: json格式
  
  ```json
  {
	"captureTime": "2017-12-17 16:21:00",
	"fromSensorId": "1",
	"imgPath": "http://222.201.137.47:12347/img/rasp-wifi.png",
	"boxes": [[0, 1, 2, 3], [2, 3,3,4]]
}
  ```
    - captureTime: 捕获时间，为yyyy-MM-dd hh:mm:ss格式
    - fromSensorId: 传感器id，一个整数，范围[0,2^32)
    - imgPath: 图片的URL，需要先调用[接口](#前端上传图片文件，后端返回一个URL)来获取，注意同步
    - boxes: 图片中行人的坐标
  - 返回值:
    - 写入成功
    
    ```json
    {
        "code": 0,
        "msg": "成功",
        "data": {
            "captureTime": "2017-12-11 07:00:00",
            "fromSensorId": 0,
            "imgPath": "http://222.201.145.237:8888/img/rasp-wifi.png"
        }
    }
    ```

#### 后端获取sensor捕捉到的图片信息，存入数据库, 并执行匹配mac地址的逻辑
  - URL: http://222.201.137.47:12346/sensor/visionMac
  - Type: POST
  - Content-type: application/json
  - 参数: json格式
  
  ```json
  {
	"captureTime": "2017-12-17 16:21:00",
	"fromSensorId": "1",
	"imgPath": "http://222.201.137.47:12347/img/rasp-wifi.png",
	"boxes": [[0, 1, 2, 3], [2, 3,3,4]]
}
  ```
    - captureTime: 捕获时间，为yyyy-MM-dd hh:mm:ss格式
    - fromSensorId: 传感器id，一个整数，范围[0,2^32)
    - imgPath: 图片的URL，需要先调用[接口](#前端上传图片文件，后端返回一个URL)来获取，注意同步
    - boxes: 图片中行人的坐标
  - 返回值:
    - 写入成功
    
    ```json
    {
        "code": 0,
        "msg": "成功",
        "data": {
            "captureTime": "2017-12-11 07:00:00",
            "fromSensorId": 0,
            "imgPath": "http://222.201.145.237:8888/img/rasp-wifi.png"
        }
    }
    ```    
    
#### 后端获取sensor捕捉到的音频信息，存入数据库
  - URL: http://222.201.137.47:12346/sensor/audio
  - Type: POST
  - Content-type: x-www-form-urlencoded
  - 参数: 
    - captureTime: 捕获时间，为yyyy-MM-dd hh:mm:ss格式
    - fromSensorId: 传感器id，一个整数，范围[0,2^32)
    - audioPath: 音频的URL，需要先调用接口#前端上传音频文件，后端返回一个URL 来获取，注意同步
  - 返回值:
    - 写入成功
    
    ```json
    {
        "code": 0,
        "msg": "成功",
        "data": {
            "captureTime": "2017-12-11 07:00:00",
            "fromSensorId": 0,
            "audioPath": "http://222.201.145.237:8888/img/rasp-wifi.mp3"
        }
    }
    ```

#### 前端上传图片文件，后端返回一个URL
  - URL: http://222.201.137.47:12346/file/img
  - Type: POST
  - Content-type: multipart/form-data
  - 参数: 
    - file: 文件二进制流 
  - 返回值：
    - 成功：
    
    ```json
    {
      "code":0,
      "msg":"成功",
      "data":"http://222.201.145.237:8888/img/rasp-wifi.png"
    }
    ```
    

#### 新增单个传感器信息(deprecated, see sensorArea/setting)
 - URL: http://222.201.137.47:12346/sensor/setting
  - Type: POST
  - Content-type: application/json
  - 参数: json格式
  
  ```json
  {
	"id": "1",
	"macAddress": "00:11:22:33:44:66",
	"latitude": 40.0,
	"longitude": 110.0 
  }
  ```
    - macAddress: 传感器上一个无线网卡的mac地址
    - id: 传感器id，一个整数，范围[0,2^32)
    - latitude: 传感器所在纬度
    - longitude: 传感器所在经度
  - 返回值:
    - 写入成功
    
    ```json
    {
        "code": 0,
        "msg": "成功",
        "data": {
            "id": 1,
            "latitude": 40,
            "longitude": 110,
            "macAddress": "00:11:22:33:44:66"
        }
    }
    ```


#### 新增单个传感器信息
 - URL: http://222.201.137.47:12346/sensorArea/setting
  - Type: POST
  - Content-type: application/json
  - 参数: json格式
  
  ```json
  {
    "id": "2",
    "macAddress": "00:11:22:33:44:02",
    "latitude": 40.0000002,
    "longitude": 110.000002,
    "x0": 0,
    "y0": 7,
    "x1": 10,
    "y1": 10
  }
  ```
    - macAddress: 传感器上一个无线网卡的mac地址
    - id: 传感器id，一个整数，范围[0,2^32)
    - latitude: 传感器所在纬度
    - longitude: 传感器所在经度
    - x0: 监控对应区域左下角横坐标
    - y0: 监控对应区域左下角纵坐标
    - x1: 监控对应区域右下角横坐标
    - y1: 监控对应区域右下角纵坐标
  - 返回值:
    - 写入成功
    
    ```json
    {
        "code": 0,
        "msg": "成功",
        "data": {
            "id": "2",
            "macAddress": "00:11:22:33:44:02",
            "latitude": 40.0000002,
            "longitude": 110.000002,
            "x0": 0,
            "y0": 7,
            "x1": 10,
            "y1": 10
        }
    }
    ``` 
    
#### 批量新增传感器信息

## Web 检索
#### 前端获取后端的传感器列表(deprecated, see sensorArea/list)
- URL: http://222.201.137.47:12346/sensor/list
  - Type: GET
  - Content-type: multipart/form-data
  - 参数: 
    无
- 返回值：
    - 成功：
    
    ```json
    {
    "code": 0,
    "msg": "成功",
    "data": [
        {
            "id": 0,
            "latitude": 40.5,
            "longitude": 110.7,
            "macAddress": "00:11:22:33:44:66"
        },
        {
            "id": 1,
            "latitude": 39.3,
            "longitude": 110.5,
            "macAddress": "02:11:22:33:44:66"
        },
        {
            "id": 2,
            "latitude": 40.2,
            "longitude": 110.1,
            "macAddress": "03:11:22:33:44:66"
        },
        {
            "id": 3,
            "latitude": 41.2,
            "longitude": 111.1,
            "macAddress": "04:11:22:33:44:66"
        }
    ]
    }
    ```

#### 前端获取后端的传感器列表
- URL: http://222.201.137.47:12346/sensorArea/list
  - Type: GET
  - Content-type: multipart/form-data
  - 参数: 
    无
- 返回值：
    - 成功：
    
    ```json
    {
        "code": 0,
        "msg": "成功",
        "data": [
            {
                "id": 0,
                "latitude": 6,
                "longitude": 2,
                "macAddress": "00:11:22:33:44:60",
                "x0": 0,
                "y0": 0,
                "x1": 4,
                "y1": 10
            },
            {
                "id": 1,
                "latitude": 4,
                "longitude": 2,
                "macAddress": "00:11:22:33:44:61",
                "x0": 6,
                "y0": 0,
                "x1": 10,
                "y1": 10
            },
            {
                "id": 2,
                "latitude": 6,
                "longitude": 10,
                "macAddress": "00:11:22:33:44:62",
                "x0": 0,
                "y0": 7,
                "x1": 10,
                "y1": 10
            }
        ]
    }
    ```

#### 前端给出传感器id和时间范围，后端返回符合条件的图片列表，以及图片中行人的位置
  - URL: http://222.201.137.47:12346/sensor/visionMac/list?id=1&startTime=2018-1-5 00:00:00&endTime=2018-1-8 00:00:00
  - Type: GET
  - Content-type: multipart/form-data
  - 参数: 
    - id: 传感器id
    - startTime: 起始时间
    - endTime: 终止时间 
  - 返回值：
    - 成功：
    
    ```json
    {
    "code": 0,
    "msg": "成功",
    "data": [
        {
            "captureTime": "2018-01-05 08:32:52",
            "fromSensorId": 1,
            "imgPath": "http://222.201.137.47:12347//img/68b1b470-1c8b-4edb-aa73-dddbf5252b74.jpg",
            "boxes": [
                [
                    79,
                    108,
                    273,
                    267
                ],
                [
                    328,
                    0,
                    172,
                    375
                ]
            ]
        },
        {
            "captureTime": "2018-01-05 08:32:57",
            "fromSensorId": 1,
            "imgPath": "http://222.201.137.47:12347//img/31eddf0f-d6ab-49bb-88af-2977d9898dfd.jpg",
            "boxes": [
                [
                    194,
                    30,
                    165,
                    274
                ]
            ]
        },
        {
            "captureTime": "2018-01-05 08:33:01",
            "fromSensorId": 1,
            "imgPath": "http://222.201.137.47:12347//img/166f1cb7-7358-48ac-af07-0c4b25fccd23.jpg",
            "boxes": [
                [
                    0,
                    302,
                    221,
                    73
                ],
                [
                    361,
                    0,
                    139,
                    375
                ]
            ]
        }
    ]
    }
    ```
    
#### 前端给出传感器id和时间范围，后端返回符合条件的音频列表

#### 前端给出传感器id和时间范围，后端返回符合条件的mac地址列表
  - URL: http://222.201.137.47:12346/sensor/wifi/list
  - Type: GET
  - Content-type: multipart/form-data
  - 参数: 
    - id: 传感器id
    - startTime: 起始时间,格式类似： 2017-12-11 07:00:00
    - endTime: 终止时间,格式类似 2017-12-11 07:00:00
  - 返回值：
    - 成功：
    
    ```json
    {
    "code": 0,
    "msg": "成功",
    "data": [
        {
            "captureTime": "2017-12-11 07:00:05",
            "fromSensorId": 0,
            "macAddress": "00:11:22:33:44:55:66",
            "intensity": 0
        },
        {
            "captureTime": "2017-12-11 07:00:05",
            "fromSensorId": 0,
            "macAddress": "00:11:22:33:44:55:66",
            "intensity": 0
        },
        {
            "captureTime": "2017-12-11 07:00:00",
            "fromSensorId": 0,
            "macAddress": "00:11:22:33:44:55:66",
            "intensity": 0
        },
        {
            "captureTime": "2017-12-11 07:00:05",
            "fromSensorId": 0,
            "macAddress": "00:11:22:33:44:55:66",
            "intensity": 0
        }
    ]
    }
    ```


#### 前端给出mac地址和时间段，后端返回mac被检索到时所在的传感器id列表

  - URL: http://222.201.137.47:12346/multi/mac2sensor
  - Type: GET
  - Content-type: multipart/form-data
  - 参数: 
    - macAddress: 被捕捉到的手机的MAC地址
    - startTime: 起始时间,格式类似： 2017-03-01 00:00:00
    - endTime: 终止时间,格式类似 2018-04-04 00:00:00
  - 返回值：
    - 成功：
    
    ```json
    {
        "code": 0,
        "msg": "成功",
        "data": [
            {
                "captureTime": "2017-12-11 07:00:05",
                "fromSensorId": 0,
                "macAddress": "00:11:22:33:44:55:66",
                "intensity": 0
            },
            {
                "captureTime": "2017-12-11 07:00:05",
                "fromSensorId": 0,
                "macAddress": "00:11:22:33:44:55:66",
                "intensity": 0
            },
            {
                "captureTime": "2017-12-11 07:00:00",
                "fromSensorId": 0,
                "macAddress": "00:11:22:33:44:55:66",
                "intensity": 0
            },
            {
                "captureTime": "2017-12-11 07:00:05",
                "fromSensorId": 0,
                "macAddress": "00:11:22:33:44:55:66",
                "intensity": 0
            },
            {
                "captureTime": "2018-03-01 07:00:05",
                "fromSensorId": 1,
                "macAddress": "00:11:22:33:44:55:66",
                "intensity": 0
            }
        ]
    }
    ```


#### 前端给出mac地址和时间段，后端返回相关图片列表，以及捕捉时间，对应的传感器id

  - URL: http://222.201.137.47:12346/multi/mac2vision
  - Type: GET
  - Content-type: multipart/form-data
  - 参数: 
    - macAddress: 被捕捉到的手机的MAC地址
    - startTime: 起始时间,格式类似： 2017-03-01 00:00:00
    - endTime: 终止时间,格式类似 2018-04-04 00:00:00
  - 返回值：
    - 成功：
    
    ```json
    {
        "code": 0,
        "msg": "成功",
        "data": [
            {
                "captureTime": "2017-12-11 07:00:00",
                "fromSensorId": 0,
                "imgPath": "http://222.201.145.237:8888//img/rasp-wifi.png",
                "boxes": [
                    [
                        0,
                        302,
                        221,
                        73
                    ],
                    [
                        361,
                        0,
                        139,
                        375
                    ]
                ]
            },
            {
                "captureTime": "2017-12-11 07:00:00",
                "fromSensorId": 0,
                "imgPath": "http://222.201.145.237:8888//img/rasp-wifi.png",
                "boxes": [
                    [
                        0,
                        302,
                        221,
                        73
                    ],
                    [
                        361,
                        0,
                        139,
                        375
                    ]
                ]
            },
            {
                "captureTime": "2017-12-11 07:00:00",
                "fromSensorId": 0,
                "imgPath": "http://222.201.145.237:8888//img/rasp-wifi.png",
                "boxes": null
            }
        ]
    }
    ```
    
#### 前端给出时间段，传感器id和mac地址，后端返回可定位到的位置信息
 - URL: http://222.201.137.47:12346/position/list
  - Type: POST
  - Content-type: multipart/form-data
  - 参数: 
    - startTime: 起始时间,格式类似： 2017-03-01 00:00:00
    - endTime: 终止时间,格式类似 2018-04-04 00:00:00
    - id:可选，可传多个，传感器id列表，不传表示查询所有传感器
    - macAddress: 可选，需定位的手机的MAC地址，不传表示查询所有mac地址
  - 返回值：
    - 成功：
    ```json
    {
        "code": 0,
        "msg": "成功",
        "data": [
            {
                "captureTime": "2017-12-11 07:00:00",
                "positionList": []
            },
            {
                "captureTime": "2017-12-11 07:00:01",
                "positionList": []
            },
            {
                "captureTime": "2017-12-11 07:00:02",
                "positionList": []
            },
            {
                "captureTime": "2017-12-11 07:00:03",
                "positionList": [
                    {
                        "captureTime": "2017-12-11 07:00:03",
                        "macAddress": "00:11:22:33:44:55:66",
                        "x": 775.5322851455759,
                        "y": 1090.6716909691856
                    }
                ]
            },
            {
                "captureTime": "2017-12-11 07:00:04",
                "positionList": []
            },
            {
                "captureTime": "2017-12-11 07:00:05",
                "positionList": []
            },
            {
                "captureTime": "2017-12-11 07:00:06",
                "positionList": []
            },
            {
                "captureTime": "2017-12-11 07:00:07",
                "positionList": []
            },
            {
                "captureTime": "2017-12-11 07:00:08",
                "positionList": [
                    {
                        "captureTime": "2017-12-11 07:00:08",
                        "macAddress": "00:11:22:33:44:55:69",
                        "x": 330,
                        "y": 880
                    }
                ]
            },
            {
                "captureTime": "2017-12-11 07:00:09",
                "positionList": []
            },
            {
                "captureTime": "2017-12-11 07:00:10",
                "positionList": []
            }
        ]
    }
    ```

#### 前端给出mac地址和时间范围，后端返回符合条件的图片列表，以及图片中行人的位置
  - URL: http://222.201.137.47:12346/vision/list?startTime=2017-12-11 07:00:01&endTime=2017-12-11 07:00:10&macAddress=00:11:22:33:44:55:66
  - Type: GET
  - Content-type: multipart/form-data
  - 参数: 
    - macAddress: mac地址
    - startTime: 起始时间
    - endTime: 终止时间 
  - 返回值：
    - 成功：
    
    ```json
    {
        "code": 0,
        "msg": "成功",
        "data": [
            {
                "captureTime": "2017-12-11 07:00:03",
                "fromSensorId": 1,
                "imgPath": "http://222.201.137.47:12347/img/rasp-wifi.png",
                "boxes": [
                    [
                        0,
                        1,
                        2,
                        3
                    ],
                    [
                        2,
                        3,
                        3,
                        4
                    ]
                ],
                "macAddress": "00:11:22:33:44:55:66"
            },
            {
                "captureTime": "2017-12-11 07:00:04",
                "fromSensorId": 1,
                "imgPath": "http://222.201.137.47:12347/img/rasp-wifi.png",
                "boxes": [
                    [
                        0,
                        1,
                        2,
                        3
                    ],
                    [
                        2,
                        3,
                        3,
                        4
                    ]
                ],
                "macAddress": "00:11:22:33:44:55:66"
            },
            {
                "captureTime": "2017-12-11 07:00:03",
                "fromSensorId": 1,
                "imgPath": "http://222.201.137.47:12347/img/rasp-wifi.png",
                "boxes": [
                    [
                        0,
                        1,
                        2,
                        3
                    ],
                    [
                        2,
                        3,
                        3,
                        4
                    ]
                ],
                "macAddress": "00:11:22:33:44:55:66"
            }
        ]
    }
    ```

#### 前端给出mac地址，后端返回mac检索到的相关图片列表，以及捕捉时间，对应的传感器id，音频列表


## Machine Learning Reid

#### 前端给出图片文件，后端返回图像检索到的相似图片列表，以及捕捉时间，对应的传感器id，音频列表，mac地址列表

#### 前端给出图片url，后端返回图像检索到的相似图片列表，以及捕捉时间，对应的传感器id，音频列表，mac地址列表
 
