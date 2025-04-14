# AI作品分析模块接口文档

## 2.图片分析

### 2.1 基本信息

请求路径：/ai-analysis  
请求方式：POST  
接口描述：上传图片并获取AI色彩情感分析结果（支持动态字数控制）  

---

### 2.2 请求参数

参数格式：multipart/form-data  

| 参数名    | 类型   | 是否必须 | 备注                             |
| --------- | ------ | -------- | -------------------------------- |
| image     | file   | 必须     | 支持格式：PNG/JPG/JPEG，最大10MB |
| wordCount | number | 必须     | 生成字数（50/100/150/200）       |

请求示例：
```http
POST /ai-analysis HTTP/1.1
Content-Type: multipart/form-data

{
  "image": "<FILE>",
  "wordCount": 100
}
```

### 2.1.3 响应数据

参数格式：application/json

| 参数名    | 类型   | 是否必须 | 备注                            |
| :-------- | :----- | :------- | :------------------------------ |
| code      | number | 必须     | 1=成功，0=失败，-1=图片格式错误 |
| msg       | string | 非必须   | 错误详情                        |
| data      | object | 非必须   | 分析结果（仅成功时返回）        |
| !-colors  | array  | 必须     | 主要色彩及占比（HEX格式）       |
| !-emotion | string | 必须     | 情感分析文本                    |

响应示例：

```json
{
  "code": 1,
  "msg": "success",
  "data": {
    "colors": [
      {"hex": "#FFD700", "percentage": 45},
      {"hex": "#87CEEB", "percentage": 30}
    ],
    "emotion": "明亮的金黄色占比45%，传递出温暖与活力；淡蓝色占比30%，带来宁静感。整体画面洋溢着乐观积极的情绪。"
  }
}
```