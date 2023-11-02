# 文字识别

### 1.接口描述 
接口请求地址：`POST`   `/v1/ocr/open/gen`

### 2.输入参数

| 参数名称              | 描述    | 是否必选 | 类型     | Location |
|-------------------|-------|------|--------| -------- |
| Finovy-Access-Token | 令牌-口令 | yes  | string | header   |
| imageBase64         | 图片的 Base64 值。 要求图片经Base64编码后不超过 7M，分辨率建议600*800以上，支持PNG、JPG、JPEG、BMP格式。   | yes | string | body |
| t                   | 解析类型 0:通用文本识别模型 1:自然场景文本识别 2:印刷文档文本识别 3:手写文本识别模型 4:车牌  |  no  | int | body |


### 3.输出参数

| 参数名称 | 描述  | 类型   |
| :------------------ | :----------- | ------ |
| page        | 页数，PDF支持会有多页的情况   | int |
| idx        | 索引位置   | int |
| detectedText        | 识别出的文本行内容   | string |
| itemPolygon             | 文本行在旋转纠正之后的图像中的像素坐标，表示为（左上角x, 左上角y）    | json |
| polygon             | 文本行坐标，以四个顶点坐标表示  注意：此字段可能返回 null，表示取不到有效值。    | json |


### 4.示例
示例1:请求成功示例

**输入示例**
```text
POST https://client.xuandashi.com/v1/ocr/open/gen
Finovy-Access-Token: 4vL4rcNGNcgx5v0RLCcFew
<公共请求参数>

{
  "imageBase64":"xxxxx",
  "t": 0
}
```

**输出示例**

```json
{
  "code":0,
  "data":[
    {
        "page":1, 
        "text":
        [
            {
                "idx":1,
                "detectedText":"16:16",
                "itemPolygon":{
                    "X":126,
                    "Y":54
                },
                "polygon":[
                    {
                        "X":126,
                        "Y":54
                    },
                    {
                        "X":251,
                        "Y":54
                    },
                    {
                        "X":251,
                        "Y":96
                    },
                    {
                        "X":126,
                        "Y":96
                    }
                ]
            },
            {
                "idx":2,
                "detectedText":"已完成",
                "itemPolygon":{
                    "X":140,
                    "Y":169
                },
                "polygon":[
                    {
                        "X":140,
                        "Y":169
                    },
                    {
                        "X":279,
                        "Y":168
                    },
                    {
                        "X":279,
                        "Y":215
                    },
                    {
                        "X":140,
                        "Y":215
                    }
                ]
            }
        ]
    }
  ],
  "msg":"success",
  "success":true,
  "traceId":"xxxxxxxxxxxxxx"
}
```

### 5.错误码
详情可查看[通用错误码](https://finovy-open-api.readthedocs.io/zh_CN/latest/api/common/3.%E9%80%9A%E7%94%A8%E9%94%99%E8%AF%AF%E7%A0%81.html#id3)