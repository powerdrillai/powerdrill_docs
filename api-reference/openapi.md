---
title: 个人项目 copy
language_tabs:
  - shell: Shell
  - http: HTTP
  - javascript: JavaScript
  - ruby: Ruby
  - python: Python
  - php: PHP
  - java: Java
  - go: Go
toc_footers: []
includes: []
search: true
code_clipboard: true
highlight_theme: darkula
headingLevel: 2
generator: "@tarslib/widdershins v4.0.23"

---

# 个人项目 copy

Base URLs:

# Authentication

- HTTP Authentication, scheme: bearer

# session

## POST Create session

POST /v1/sessions

Creates a session. Up to 150 sessions can be created. <br/>
A session refers to the continuous interaction between the user and Powerdrill within a conversation.

> Body 请求参数

```json
{
  "config": {
    "colorIndex": [
      "#FF0000",
      "#ddd"
    ],
    "languageType": "EN",
    "maxMessagesInContext": 10,
    "mediaTtl": 7200
  },
  "title": "测试"
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|Authorization|header|string| 是 ||The API key used for authorization.|
|body|body|object| 否 ||none|
|» title|body|string| 是 ||The session name.|
|» config|body|object| 是 ||The session settings.|
|»» languageType|body|string| 否 | 输出语言类型|Specifies the language in which the output is generated. The value of this parameter is a key-value pair, where the key defines the language, and the value serves as the comment. Possible values are: |
|»» mediaTtl|body|integer| 否 | 媒体生命周期|The valid duration for accessible links generated for media files, such as images in the units of seconds. The value range is 1 to 6000 and defaults to 3600 (1 hour).|
|»» maxMessagesInContext|body|integer| 否 | 上下文的消息数量上限|The maximum number of messages retained per session, with a value range of 1 to 30 and a default of 10.|
|»» colorIndex|body|[string]| 否 | 色卡属性列表|The list of color palette attributes, with values in RGB hexadecimal format such as #FF0000.|
|»» chatMode|body|string| 否 | 对话模式|Chat mode: Possible values are ALL and DATA_ANALYTICS. When set to ALL, Powerdrill will automatically detect your intent and select the appropriate chat mode. When set to DATA_ANALYTICS, Powerdrill will focus specifically on data analysis.|

#### 详细说明

**»» languageType**: Specifies the language in which the output is generated. The value of this parameter is a key-value pair, where the key defines the language, and the value serves as the comment. Possible values are: 
   "AUTO": None,
    "EN": "English",
    "ES": "Spanish",
    "AR": "Arabic",
    "PT": "Portuguese",
    "ID": "Indonesian",
    "JA": "Japanese",
    "RU": "Russian",
    "HI": "Hindi",
    "FR": "French",
    "DE": "German",
    "VI": "Vietnamese",
    "TR": "Turkish",
    "PL": "Polish",
    "IT": "Italian",
    "KO": "Korean",
    "ZH-CN": "Simplified Chinese",
    "ZH-TW": "Traditional Chinese"

> 返回示例

```json
{
  "code": 0,
  "data": "06e29045-cca9-4326-b324-fdff14375ee3"
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none|业务码|Status code. 0 indicates that the session is created. Otherwise, the operation fails. Possible error codes include: <br/><br />100: Bad request. <br/><br />201: Request frequency limit. <br/><br />9999: Internal error. <br/><br />100001: Invalid operation. <br/><br />100105: maxMessageInContext parameter value must be 1 to 30. <br/><br />100106: mediaTtl parameter value must be 1 to 6000. <br/><br />211001: The number of sessions have reached the upper limit of 150.|
|» data|string|true|none||The session ID.|

## GET List sessions

GET /v1/sessions

Lists sessions in your Teamspace.

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|title|query|string| 否 ||The session name.|
|pageNumber|query|integer| 否 ||The number of pages to display.|
|pageSize|query|integer| 否 ||The number of items displayed per page.|
|Authorization|header|string| 是 ||The API key used for authorization.|

> 返回示例

```json
{
  "code": 0,
  "data": {
    "total": 4,
    "pageSize": 10,
    "pageNumber": 1,
    "records": [
      {
        "id": "5534f591-1520-4e74-b753-b87615b2c57a",
        "title": "new title",
        "config": {
          "languageType": "IT",
          "mediaTtl": 10,
          "maxMessagesInContext": 10
        }
      },
      {
        "id": "ebeeec8d-84f8-448e-bb56-6331807e4e7a",
        "title": "测试2",
        "config": {
          "languageType": "EN",
          "mediaTtl": 600,
          "maxMessagesInContext": 10
        }
      },
      {
        "id": "06e29045-cca9-4326-b324-fdff14375ee3",
        "title": "测试",
        "config": {
          "languageType": "EN",
          "mediaTtl": 600,
          "maxMessagesInContext": 10
        }
      },
      {
        "id": "fb0358b2-4280-400d-97f0-f82c4e9edb95",
        "title": "Hello",
        "config": {
          "languageType": "AUTO",
          "mediaTtl": 600,
          "maxMessagesInContext": 10
        }
      }
    ]
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none|业务码|Status code. 0 indicates that the session is created. Otherwise, the operation fails. Possible error codes include: <br/><br />100: Bad request. <br/><br />201: Request frequency limit. <br/><br />9999: Internal error. <br/><br />100001: Invalid operation.|
|» data|object|true|none||The information about each listed session.|
|»» total|integer|true|none||The number of total pages.|
|»» pageNumber|integer|true|none||The page number.|
|»» pageSize|integer|true|none||The number of items displayed per page.|
|»» records|[object]|true|none||The list of records of the session|
|»»» id|string|true|none||none|
|»»» title|string|true|none||none|
|»»» config|[sessionConfig](#schemasessionconfig)|true|none||none|
|»»»» languageType|string|false|none|输出语言类型|枚举如下：取Key作为参数，value是备注<br />"AUTO": None,<br />    "EN": "English",<br />    "ES": "Spanish",<br />    "AR": "Arabic",<br />    "PT": "Portuguese",<br />    "ID": "Indonesian",<br />    "JA": "Japanese",<br />    "RU": "Russian",<br />    "HI": "Hindi",<br />    "FR": "French",<br />    "DE": "German",<br />    "VI": "Vietnamese",<br />    "TR": "Turkish",<br />    "PL": "Polish",<br />    "IT": "Italian",<br />    "KO": "Korean",<br />    "ZH-CN": "Simplified Chinese",<br />    "ZH-TW": "Traditional Chinese"|
|»»»» mediaTtl|integer|false|none|媒体生命周期|单位秒，默认1小时|
|»»»» maxMessagesInContext|integer|false|none|上下文的消息数量上限|默认10|
|»»»» colorIndex|[string]|false|none|色卡属性列表|RGB十六进制值比如：#FF0000|

## PATCH Modify session

PATCH /v1/sessions/{sessionId}

Modifies the configuration of the specified session.

> Body 请求参数

```json
{
  "config": {
    "colorIndex": [
      "#FF0000",
      "#ddd"
    ],
    "languageType": "IT",
    "maxMessagesInContext": 0,
    "mediaTtl": 10
  },
  "title": "new title"
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|sessionId|path|string| 是 ||The ID of the session to modify.|
|Authorization|header|string| 是 ||none|
|body|body|object| 否 ||none|
|» title|body|string| 否 ||The session name. You must set at least one of <b>title<b/> or <b>config<b/>.|
|» config|body|object| 否 ||The configuration of the session. You must set at least one of <b>title<b/> or <b>config<b/>.|
|»» languageType|body|string| 否 | 输出语言类型|Specifies the language in which the output is generated. The value of this parameter is a key-value pair, where the key defines the language, and the value serves as the comment. Possible values are: |
|»» mediaTtl|body|integer| 否 | 媒体生命周期|The valid duration for accessible links generated for media files, such as images in the units of seconds. The value range is 1 to 6000 and defaults to 3600 (1 hour).|
|»» maxMessagesInContext|body|integer| 否 | 上下文的消息数量上限|The maximum number of messages that can be retained in a session. The value range is 1 to 30 and defaults to 10.|
|»» colorIndex|body|[string]| 否 | 色卡属性列表|The list of color palette attributes, with values in RGB hexadecimal format such as #FF0000.|
|»» chatMode|body|string| 否 | 对话模式|The chat mode. Possible values are ALL and DATA_ANALYTICS. If you set it to ALL, Powerdrill will automatically recognize your intention and choose the right chat mode. If you set it to DATA_ANALYTICS, Powerdrill will perform data analysis.|

#### 详细说明

**»» languageType**: Specifies the language in which the output is generated. The value of this parameter is a key-value pair, where the key defines the language, and the value serves as the comment. Possible values are: 
    "AUTO": None,
    "EN": "English",
    "ES": "Spanish",
    "AR": "Arabic",
    "PT": "Portuguese",
    "ID": "Indonesian",
    "JA": "Japanese",
    "RU": "Russian",
    "HI": "Hindi",
    "FR": "French",
    "DE": "German",
    "VI": "Vietnamese",
    "TR": "Turkish",
    "PL": "Polish",
    "IT": "Italian",
    "KO": "Korean",
    "ZH-CN": "Simplified Chinese",
    "ZH-TW": "Traditional Chinese"

> 返回示例

```json
{
  "code": 0
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none|业务码|Status code. 0 indicates that the session is created. Otherwise, the operation fails. Possible error codes include: <br/><br />100: Bad request. <br/><br />201: Request frequency limit. <br/><br />9999: Internal error. <br/><br />100001: Invalid operation. <br/><br />100105: maxMessageInContext parameter value must be 1 to 30. <br/><br />100106: mediaTtl parameter value must be 1 to 6000.|
|» data|string|true|none|业务数据|The session ID.|

## DELETE Delete session

DELETE /v1/sessions/{sessionId}

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|sessionId|path|string| 是 ||none|
|Authorization|header|string| 是 ||none|

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "data": "string"
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none|业务码|正确返回0,<br />错误枚举：<br />100-Bad request;<br />201-Request frequency limit;<br />9999-Internal error;<br />100001-operate.invalid;|
|» data|string|false|none||A null value is returned if the operation is successful.|

## GET Get session

GET /v1/sessions/{sessionId}

Obtains information about the specified session.

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|sessionId|path|string| 是 ||The session ID.|
|Authorization|header|string| 是 ||The API key used for authorization.|

> 返回示例

```json
{
  "code": 0,
  "data": {
    "id": "06e29045-cca9-4326-b324-fdff14375ee3",
    "title": "测试",
    "config": {
      "languageType": "EN",
      "mediaTtl": 600,
      "maxMessagesInContext": 10
    }
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none|业务码|Status code. 0 indicates that the session is created. Otherwise, the operation fails. Possible error codes include: <br/><br />100: Bad request. <br/><br />201: Request frequency limit. <br/><br />9999: Internal error. <br/><br />100001: Invalid operation. <br/><br />211002: The session does not exist.|
|» data|[SessionModelDTO](#schemasessionmodeldto)|true|none||none|
|»» id|string|true|none||none|
|»» title|string|false|none||none|
|»» config|[sessionConfig](#schemasessionconfig)|false|none||none|
|»»» languageType|string|false|none|输出语言类型|枚举如下：取Key作为参数，value是备注<br />"AUTO": None,<br />    "EN": "English",<br />    "ES": "Spanish",<br />    "AR": "Arabic",<br />    "PT": "Portuguese",<br />    "ID": "Indonesian",<br />    "JA": "Japanese",<br />    "RU": "Russian",<br />    "HI": "Hindi",<br />    "FR": "French",<br />    "DE": "German",<br />    "VI": "Vietnamese",<br />    "TR": "Turkish",<br />    "PL": "Polish",<br />    "IT": "Italian",<br />    "KO": "Korean",<br />    "ZH-CN": "Simplified Chinese",<br />    "ZH-TW": "Traditional Chinese"|
|»»» mediaTtl|integer|false|none|媒体生命周期|单位秒，默认1小时|
|»»» maxMessagesInContext|integer|false|none|上下文的消息数量上限|默认10|
|»»» colorIndex|[string]|false|none|色卡属性列表|RGB十六进制值比如：#FF0000|

## GET Get chat history in session

GET /v1/sessions/{sessionId}/history

Obtains the chat history contained in the specified session.

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|sessionId|path|string| 是 ||The session ID.|
|pageNumber|query|integer| 否 ||The number of pages to display.|
|pageSize|query|integer| 否 ||The number of records displayed per page.|
|Authorization|header|string| 是 ||none|

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "data": {
    "total": 0,
    "pageNumber": 0,
    "pageSize": 0,
    "records": [
      {
        "question": {
          "messageId": "string",
          "content": "string"
        },
        "answer": {
          "messageId": "string",
          "content": "string"
        }
      }
    ]
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none|业务码|Status code. 0 indicates that the session is created. Otherwise, the operation fails. Possible error codes include: <br/><br />100: Bad request. <br/><br />201: Request frequency limit. <br/><br />9999: Internal error. <br/><br />100001: Invalid operation.|
|» data|object|true|none||The information about the session.|
|»» total|integer|true|none||The total number of pages displayed.|
|»» pageNumber|integer|true|none||The page number.|
|»» pageSize|integer|true|none||The number of records displayed per page.|
|»» records|[[ConversationDTO](#schemaconversationdto)]|true|none||The list of records displayed.|
|»»» question|[MessageDTO](#schemamessagedto)|true|none||The user's question.|
|»»»» messageId|string|true|none||The message ID.|
|»»»» content|string|true|none||The message content.|
|»»» answer|[MessageDTO](#schemamessagedto)|true|none||The user's question.|
|»»»» messageId|string|true|none||The message ID.|
|»»»» content|string|true|none||The message content.|

# dataset

## POST Create dataset

POST /v1/datasets

A dataset is a collection of data sources. 

You can upload various types of data sources into a single dataset, with each dataset supporting up to 10 data sources.

> Body 请求参数

```json
{
  "description": "mysql的所有文档数据",
  "name": "mysql数据集"
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|Authorization|header|string| 是 ||The API key used for authorization.|
|body|body|object| 否 ||none|
|» name|body|string| 是 ||The dataset name.|
|» description|body|string| 否 ||The dataset description.|

> 返回示例

```json
{
  "code": 0,
  "data": "cm1gikb42001fr3x29gbvxwfa"
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none|业务码|Status code. 0 indicates that the operation is successful. Otherwise, the operation fails. Possible error codes include: <br/><br />100: Bad request. <br/><br />201: Request frequency limit. <br/><br />9999: Internal error. <br/><br />100001: Invalid operation.|
|» data|string|true|none||The dataset ID.|

## GET List datasets

GET /v1/datasets

Lists datasets in your Teamspace or of the specified name.

> Body 请求参数

```json
{}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|pageNumber|query|integer| 否 ||The number of pages to display.|
|pageSize|query|integer| 否 ||The number of records displayed per page.|
|name|query|string| 否 ||The dataset name.|
|Authorization|header|string| 是 ||none|
|body|body|object| 否 ||none|

> 返回示例

```json
{
  "code": 0,
  "data": {
    "total": 31,
    "pageSize": 10,
    "pageNumber": 1,
    "records": [
      {
        "id": "cm1gir4jz0020r3x2qnfb9prx",
        "name": "1mysql数据集",
        "description": "1mysql的所有文档数据"
      },
      {
        "id": "clzm3gsix000hqsx2uw7wvw0p",
        "name": "mysql数据集",
        "description": "joker test"
      },
      {
        "id": "clzm303my0000dvx2u0feu0i3",
        "name": "mysql数据集",
        "description": "joker test"
      },
      {
        "id": "clzm2w8xj0000gnx2w041itzy",
        "name": "mysql数据集",
        "description": "joker test"
      },
      {
        "id": "clzm2t6np000ndpx2bh7ls777",
        "name": "mysql数据集",
        "description": "joker test"
      },
      {
        "id": "clzm2sal6000ldpx2e3tvvmez",
        "name": "mysql数据集",
        "description": "joker test"
      },
      {
        "id": "clzm2s2bm000jdpx2i6f2kowz",
        "name": "mysql数据集",
        "description": "joker test"
      },
      {
        "id": "clzm2rvpp000hdpx2qghug9sg",
        "name": "mysql数据集",
        "description": "joker test"
      },
      {
        "id": "clzm2eey4000hf7x2t51u19o0",
        "name": "mysql数据集",
        "description": "joker test"
      },
      {
        "id": "clzm2b64600004mx25cvu0ngi",
        "name": "mysql数据集",
        "description": "joker test"
      }
    ]
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none|业务码|Status code. 0 indicates that the operation is successful. Otherwise, the operation fails. Possible error codes include: <br/><br />100: Bad request. <br/><br />201: Request frequency limit. <br/><br />9999: Internal error. <br/><br />100001: Invalid operation.|
|» data|object|true|none||The information about the dataset list.|
|»» pageNumber|integer|true|none||The page number.|
|»» pageSize|integer|true|none||The number of items displayed per page.|
|»» total|integer|true|none||The total number of pages displayed.|
|»» records|[[DatasetDTO](#schemadatasetdto)]|true|none||The list of datasets.|
|»»» id|string|true|none||none|
|»»» name|string|true|none||none|
|»»» description|string|true|none||none|

## DELETE Delete dataset

DELETE /v1/datasets/{datasetId}

Deletes the specified dataset. Once deleted, all data sources within the dataset will also be permanently removed and cannot be recovered.

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|datasetId|path|string| 是 ||The dataset ID.|
|Authorization|header|string| 是 ||The API key used for authorization.|

> 返回示例

```json
{
  "code": 0
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none|业务码|Status code. 0 indicates that the operation is successful. Otherwise, the operation fails. Possible error codes include: <br/><br />100: Bad request. <br/><br />201: Request frequency limit. <br/><br />9999: Internal error. <br/><br />100001: Invalid operation.|
|» data|string|false|none||A null value is returned if the operation is successful.|

## PATCH Modify dataset

PATCH /v1/datasets/{datasetId}

Modifies information about the specified dataset.

> Body 请求参数

```json
{
  "name": "dataset"
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|datasetId|path|string| 是 ||The dataset ID.|
|Authorization|header|string| 是 ||The API key used for authorization.|
|body|body|object| 否 ||none|
|» name|body|string| 否 ||The new name of the dataset. <b>name</b> and <b>description</b> cannot be both blank.|
|» description|body|string| 否 ||The new description of the dataset. <b>name</b> and <b>description</b> cannot be both blank.|

> 返回示例

```json
{
  "code": 0
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none|业务码|Status code. 0 indicates that the operation is successful. Otherwise, the operation fails. Possible error codes include: <br/><br />100: Bad request. <br/><br />201: Request frequency limit. <br/><br />9999: Internal error. <br/><br />100001: Invalid operation.|
|» data|string¦null|true|none||Null if the operation is successful.|

## GET Get dataset status

GET /v1/datasets/{datasetId}/status

Obtains the status of the specified dataset.

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|datasetId|path|string| 是 ||The dataset ID.|
|Authorization|header|string| 是 ||The API key used for authorization.|

> 返回示例

```json
{
  "code": 0,
  "data": "synched"
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none|业务码|Status code. 0 indicates that the operation is successful. Otherwise, the operation fails. Possible error codes include: <br/><br />100: Bad request. <br/><br />201: Request frequency limit. <br/><br />9999: Internal error. <br/><br />100001: Invalid operation.|
|» data|string|true|none||Dataset status. Possible values are: <br/><br />synched: All data sources in the dataset are synchronized. <br/><br />processing: At least one data source is currently being synchronized. <br/><br />part_error: Synchronization failed for at least one data source. <br/><br />empty_datasource: The dataset contains no data sources.|

# datasoure

## POST Create datasource in dataset

POST /v1/datasets/{datasetId}/datasources

Creates a data source in the specified dataset. Note that one dataset can contain up to 10 data sources.

> Body 请求参数

```json
{
  "ext": "csv",
  "name": "测试version.csv",
  "type": "FILE",
  "url": "https://s3.amazonaws.com/powerdrilltest/user/clvl4cad2001q01l1m522hxlu/upload/f9773f1e-cd68-489a-8121-d566ca9218b1.csv?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240924T143419Z&X-Amz-SignedHeaders=host&X-Amz-Expires=599&X-Amz-Credential=AKIARLSQLXURHEIDN4OZ%2F20240924%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=9ca0c58d508926a5811818041d557ffb53c64025dae94c0855280d457c7089a2"
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|datasetId|path|string| 是 ||The dataset ID.|
|Authorization|header|string| 是 ||The API key used for authorization.|
|body|body|[SingleDatasourceRequest](#schemasingledatasourcerequest)| 否 ||none|

> 返回示例

```json
{
  "code": 0,
  "data": {
    "id": "cm1gjg1kf0001kcx2puywmzbv",
    "datasetId": "cm1gir4jz0020r3x2qnfb9prx",
    "name": "测试csv",
    "type": "FILE",
    "url": "https://s3.amazonaws.com/powerdrilltest/user/clvl4cad2001q01l1m522hxlu/upload/f9773f1e-cd68-489a-8121-d566ca9218b1.csv?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240924T143419Z&X-Amz-SignedHeaders=host&X-Amz-Expires=599&X-Amz-Credential=AKIARLSQLXURHEIDN4OZ%2F20240924%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=9ca0c58d508926a5811818041d557ffb53c64025dae94c0855280d457c7089a2",
    "ext": "csv",
    "status": "pending"
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none|业务码|Status code. 0 indicates that the operation is successful. Otherwise, the operation fails. Possible error codes include: <br/><br />100: Bad request. <br/><br />201: Request frequency limit. <br/><br />9999: Internal error. <br/><br />100001: Invalid operation.|
|» data|[DatasourceDTO](#schemadatasourcedto)|true|none||none|
|»» id|string|true|none||The data source ID.|
|»» datasetId|string|true|none||The dataset ID.|
|»» name|string|true|none||The data source name.|
|»» type|string|true|none||The type of the data source.|
|»» url|string|true|none||The URL of the data source.|
|»» ext|string|true|none||The file name extension.|
|»» status|string|true|none|文件同步状态|The processing status of the data source, with possible values:<br />- **pending**: Awaiting processing.<br />- **running**: Currently processing.<br />- **synched**: Successfully synchronized.<br />- **error**: Processing failed.<br />- **usage_limit_reached**: Quota limit reached.|

## GET List datasources

GET /v1/datasets/{datasetId}/datasources

Lists data sources contained in the specified dataset.

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|datasetId|path|string| 是 ||The dataset ID.|
|pageNumber|query|integer| 否 ||The number of pages to display.|
|pageSize|query|integer| 否 ||The number of records displayed per page.|
|name|query|string| 否 ||The data source name.|
|expand|query|string| 否 ||An extended field. Set it to preSignUrl to return a presigned URL.|
|Authorization|header|string| 是 ||none|

> 返回示例

```json
{
  "code": 0,
  "data": {
    "total": 1,
    "pageSize": 10,
    "pageNumber": 1,
    "records": [
      {
        "id": "cm1gjmmoo0001h0x24uk1xgu9",
        "datasetId": "cm1gjmg8e0057r3x22v1fdu8m",
        "name": "测试version2csv",
        "type": "FILE",
        "url": "https://s3.amazonaws.com/powerdrilltest/user/clvl4cad2001q01l1m522hxlu/upload/f9773f1e-cd68-489a-8121-d566ca9218b1.csv?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240924T143419Z&X-Amz-SignedHeaders=host&X-Amz-Expires=599&X-Amz-Credential=AKIARLSQLXURHEIDN4OZ%2F20240924%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=9ca0c58d508926a5811818041d557ffb53c64025dae94c0855280d457c7089a2",
        "ext": "csv",
        "status": "pending"
      }
    ]
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none|业务码|Status code. 0 indicates that the operation is successful. Otherwise, the operation fails. Possible error codes include: <br/><br />100: Bad request. <br/><br />201: Request frequency limit. <br/><br />9999: Internal error. <br/><br />100001: Invalid operation.|
|» data|object|true|none||The information about the listed data sources.|
|»» total|integer|true|none||The total number of records displayed.|
|»» pageSize|integer|true|none||The number of records displayed per page.|
|»» pageNumber|integer|true|none||The page number.|
|»» records|[[DatasourceDTO](#schemadatasourcedto)]|true|none||The information about each listed data source.|
|»»» id|string|true|none||The data source ID.|
|»»» datasetId|string|true|none||The dataset ID.|
|»»» name|string|true|none||The data source name.|
|»»» type|string|true|none||The type of the data source.|
|»»» url|string|true|none||The URL of the data source.|
|»»» ext|string|true|none||The file name extension.|
|»»» status|string|true|none|文件同步状态|The processing status of the data source, with possible values:<br />- **pending**: Awaiting processing.<br />- **running**: Currently processing.<br />- **synched**: Successfully synchronized.<br />- **error**: Processing failed.<br />- **usage_limit_reached**: Quota limit reached.|

## DELETE Delete datasource

DELETE /v1/datasets/{datasetId}/datasources/{datasourceId}

Deletes the specified data source from the specified dataset. Once deleted, the data source cannot be recovered.

> Body 请求参数

```json
[
  "string"
]
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|datasetId|path|string| 是 ||The ID of the dataset that contains the data source.|
|datasourceId|path|string| 是 ||The data source ID.|
|Authorization|header|string| 是 ||The API key used for authorization.|
|body|body|array[string]| 否 ||none|

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "data": "string"
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none|业务码|Status code. 0 indicates that the operation is successful. Otherwise, the operation fails. Possible error codes include: <br/><br />100: Bad request. <br/><br />201: Request frequency limit. <br/><br />9999: Internal error. <br/><br />100001: Invalid operation.|
|» data|string¦null|false|none||Null returned if the operation is successful.|

## GET Get datasource

GET /v1/datasets/{datasetId}/datasources/{datasourceId}

Obtains information about the specified data source.

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|datasetId|path|string| 是 ||The ID of the dataset that contains the data source.|
|datasourceId|path|string| 是 ||The data source ID. |
|expand|query|string| 否 ||An extended field. Set it to preSignUrl to return a presigned URL.|
|Authorization|header|string| 是 ||The API key used for authorization.|

> 返回示例

```json
{
  "code": 0,
  "data": {
    "id": "cm1gjmmoo0001h0x24uk1xgu9",
    "datasetId": "cm1gjmg8e0057r3x22v1fdu8m",
    "name": "测试version2.csv",
    "type": "FILE",
    "url": "https://s3.amazonaws.com/powerdrilltest/user/clvl4cad2001q01l1m522hxlu/upload/f9773f1e-cd68-489a-8121-d566ca9218b1.csv?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240924T143419Z&X-Amz-SignedHeaders=host&X-Amz-Expires=599&X-Amz-Credential=AKIARLSQLXURHEIDN4OZ%2F20240924%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=9ca0c58d508926a5811818041d557ffb53c64025dae94c0855280d457c7089a2",
    "ext": "csv",
    "status": "pending"
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none|业务码|Status code. 0 indicates that the operation is successful. Otherwise, the operation fails. Possible error codes include: <br/><br />100: Bad request. <br/><br />201: Request frequency limit. <br/><br />9999: Internal error. <br/><br />100001: Invalid operation.|
|» data|[DatasourceDTO](#schemadatasourcedto)|true|none||none|
|»» id|string|true|none||The data source ID.|
|»» datasetId|string|true|none||The dataset ID.|
|»» name|string|true|none||The data source name.|
|»» type|string|true|none||The type of the data source.|
|»» url|string|true|none||The URL of the data source.|
|»» ext|string|true|none||The file name extension.|
|»» status|string|true|none|文件同步状态|The processing status of the data source, with possible values:<br />- **pending**: Awaiting processing.<br />- **running**: Currently processing.<br />- **synched**: Successfully synchronized.<br />- **error**: Processing failed.<br />- **usage_limit_reached**: Quota limit reached.|

## POST Create datasource

POST /v1/datasources

Creates a data source without specifying a dataset. Powerdrill will automatically generate a dataset for it.

> Body 请求参数

```json
{
  "name": "test.csv",
  "type": "FILE",
  "url": "https://commontestdata-1312904344.cos.ap-shanghai.myqcloud.com/aidata/KIE/s1_pages/train.csv",
  "ext": "csv"
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|Authorization|header|string| 是 ||The API key used for authorization.|
|body|body|object| 否 ||none|
|» name|body|string| 是 ||The name of the data source.|
|» type|body|string| 是 ||The type of the data source, for example, FILE.|
|» url|body|string| 是 ||The URL of the file for public access.|
|» ext|body|string| 是 ||The file name extension. Supported file extensions include: csv, tsv, pdf, md, mdx, json, txt, pptx, docx, xls, and xlsx.|

> 返回示例

```json
{
  "code": 0,
  "data": {
    "id": "cm1zvcymv000101fcluu1htgr",
    "datasetId": "cm0buoeeq02v201l1pp7payr6",
    "name": "jinxi test datasource.csv",
    "type": "FILE",
    "url": "https://commontestdata-1312904344.cos.ap-shanghai.myqcloud.com/aidata/KIE/s1_pages/train.csv",
    "ext": "csv",
    "status": "pending"
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» code|integer|true|none|业务码|Status code. 0 indicates that the operation is successful. Otherwise, the operation fails. Possible error codes include: <br/><br />100: Bad request. <br/><br />201: Request frequency limit. <br/><br />9999: Internal error. <br/><br />100001: Invalid operation.|
|» data|[DatasourceDTO](#schemadatasourcedto)|true|none||none|
|»» id|string|true|none||The data source ID.|
|»» datasetId|string|true|none||The dataset ID.|
|»» name|string|true|none||The data source name.|
|»» type|string|true|none||The type of the data source.|
|»» url|string|true|none||The URL of the data source.|
|»» ext|string|true|none||The file name extension.|
|»» status|string|true|none|文件同步状态|The processing status of the data source, with possible values:<br />- **pending**: Awaiting processing.<br />- **running**: Currently processing.<br />- **synched**: Successfully synchronized.<br />- **error**: Processing failed.<br />- **usage_limit_reached**: Quota limit reached.|

# chat

## POST Query

POST /v1/chat/completions

Chats with your data. You can ask anything you want to know from your data.

> Body 请求参数

```json
{
  "datasetId": "cm1gjmg8e0057r3x22v1fdu8m",
  "datasourceIdList": [
    "cm1gjmmoo0001h0x24uk1xgu9"
  ],
  "history": [
    {
      "answer": "test",
      "question": "test"
    }
  ],
  "languageType": "IT",
  "question": "Hello World",
  "sessionId": "5534f591-1520-4e74-b753-b87615b2c57a",
  "stream": true
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|Authorization|header|string| 是 ||none|
|body|body|object| 否 ||none|
|» sessionId|body|string| 是 ||none|
|» stream|body|boolean| 否 ||none|
|» question|body|string| 是 ||none|
|» datasetId|body|string| 否 ||none|
|» datasourceIdList|body|[string]| 否 ||Specifies the IDs of the data sources to use in the conversation, rather than the entire dataset. You can specify up to 1,000 data sources.|
|» history|body|[[HistoryDTO](#schemahistorydto)]| 否 ||If this parameter is not provided or is empty, the session's historical messages will be used. The maximum of historical messages is determined by the maxMessagesInContext parameter configured for the session.|
|»» question|body|string| 是 | 问题|The user's question.|
|»» answer|body|string| 是 | 回答|The answer to the question.|
|» languageType|body|string| 否 | 输出语言设置|Specifies the language in which the output is generated. The value of this parameter is a key-value pair, where the key defines the language, and the value serves as the comment. Possible values are:|
|» chatMode|body|string| 否 | 对话模式|The chat mode. Possible values are ALL and DATA_ANALYTICS. If you set it to ALL, Powerdrill will automatically recognize your intention and choose the right chat mode. If you set it to DATA_ANALYTICS, Powerdrill will perform data analysis.|
|» answerConfig|body|[answerConfig](#schemaanswerconfig)| 否 ||none|
|»» modelId|body|string| 是 | 模型Id|claude-3-h|
|»» maxTokens|body|integer| 否 | answer的maxTokens|none|
|»» temperature|body|number| 否 ||none|

#### 详细说明

**» languageType**: Specifies the language in which the output is generated. The value of this parameter is a key-value pair, where the key defines the language, and the value serves as the comment. Possible values are:
    "AUTO": None,
    "EN": "English",
    "ES": "Spanish",
    "AR": "Arabic",
    "PT": "Portuguese",
    "ID": "Indonesian",
    "JA": "Japanese",
    "RU": "Russian",
    "HI": "Hindi",
    "FR": "French",
    "DE": "German",
    "VI": "Vietnamese",
    "TR": "Turkish",
    "PL": "Polish",
    "IT": "Italian",
    "KO": "Korean",
    "ZH-CN": "Simplified Chinese",
    "ZH-TW": "Traditional Chinese"

> 返回示例

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### 返回数据结构

# 数据模型

<h2 id="tocS_DatasourceDTO">DatasourceDTO</h2>

<a id="schemadatasourcedto"></a>
<a id="schema_DatasourceDTO"></a>
<a id="tocSdatasourcedto"></a>
<a id="tocsdatasourcedto"></a>

```json
{
  "id": "string",
  "datasetId": "string",
  "name": "string",
  "type": "string",
  "url": "string",
  "ext": "string",
  "status": "string"
}

```

### 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|string|true|none||The data source ID.|
|datasetId|string|true|none||The dataset ID.|
|name|string|true|none||The data source name.|
|type|string|true|none||The type of the data source.|
|url|string|true|none||The URL of the data source.|
|ext|string|true|none||The file name extension.|
|status|string|true|none|文件同步状态|The processing status of the data source, with possible values:<br />- **pending**: Awaiting processing.<br />- **running**: Currently processing.<br />- **synched**: Successfully synchronized.<br />- **error**: Processing failed.<br />- **usage_limit_reached**: Quota limit reached.|

<h2 id="tocS_HistoryDTO">HistoryDTO</h2>

<a id="schemahistorydto"></a>
<a id="schema_HistoryDTO"></a>
<a id="tocShistorydto"></a>
<a id="tocshistorydto"></a>

```json
{
  "question": "string",
  "answer": "string"
}

```

### 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|question|string|true|none|问题|The user's question.|
|answer|string|true|none|回答|The answer to the question.|

<h2 id="tocS_MessageDTO">MessageDTO</h2>

<a id="schemamessagedto"></a>
<a id="schema_MessageDTO"></a>
<a id="tocSmessagedto"></a>
<a id="tocsmessagedto"></a>

```json
{
  "messageId": "string",
  "content": "string"
}

```

### 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|messageId|string|true|none||The message ID.|
|content|string|true|none||The message content.|

<h2 id="tocS_SingleDatasourceRequest">SingleDatasourceRequest</h2>

<a id="schemasingledatasourcerequest"></a>
<a id="schema_SingleDatasourceRequest"></a>
<a id="tocSsingledatasourcerequest"></a>
<a id="tocssingledatasourcerequest"></a>

```json
{
  "name": "string",
  "type": "string",
  "url": "string",
  "ext": "string"
}

```

### 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|name|string|true|none||The name of the data source.|
|type|string|true|none||The type of the data source, for example, FILE.|
|url|string|true|none||The URL of the file for public access.|
|ext|string|true|none||The file name extension. Supported file extensions include: csv, tsv, pdf, md, mdx, json, txt, pptx, docx, xls, and xlsx.|

<h2 id="tocS_SessionModelDTO">SessionModelDTO</h2>

<a id="schemasessionmodeldto"></a>
<a id="schema_SessionModelDTO"></a>
<a id="tocSsessionmodeldto"></a>
<a id="tocssessionmodeldto"></a>

```json
{
  "id": "string",
  "title": "string",
  "config": {
    "languageType": "string",
    "mediaTtl": 0,
    "maxMessagesInContext": 0,
    "colorIndex": [
      "string"
    ]
  }
}

```

### 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|string|true|none||none|
|title|string|true|none||none|
|config|[sessionConfig](#schemasessionconfig)|true|none||none|

<h2 id="tocS_sessionConfig">sessionConfig</h2>

<a id="schemasessionconfig"></a>
<a id="schema_sessionConfig"></a>
<a id="tocSsessionconfig"></a>
<a id="tocssessionconfig"></a>

```json
{
  "languageType": "string",
  "mediaTtl": 0,
  "maxMessagesInContext": 0,
  "colorIndex": [
    "string"
  ]
}

```

### 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|languageType|string|false|none|输出语言类型|枚举如下：取Key作为参数，value是备注<br />"AUTO": None,<br />    "EN": "English",<br />    "ES": "Spanish",<br />    "AR": "Arabic",<br />    "PT": "Portuguese",<br />    "ID": "Indonesian",<br />    "JA": "Japanese",<br />    "RU": "Russian",<br />    "HI": "Hindi",<br />    "FR": "French",<br />    "DE": "German",<br />    "VI": "Vietnamese",<br />    "TR": "Turkish",<br />    "PL": "Polish",<br />    "IT": "Italian",<br />    "KO": "Korean",<br />    "ZH-CN": "Simplified Chinese",<br />    "ZH-TW": "Traditional Chinese"|
|mediaTtl|integer|false|none|媒体生命周期|单位秒，默认1小时|
|maxMessagesInContext|integer|false|none|上下文的消息数量上限|默认10|
|colorIndex|[string]|false|none|色卡属性列表|RGB十六进制值比如：#FF0000|

<h2 id="tocS_DatasetDTO">DatasetDTO</h2>

<a id="schemadatasetdto"></a>
<a id="schema_DatasetDTO"></a>
<a id="tocSdatasetdto"></a>
<a id="tocsdatasetdto"></a>

```json
{
  "id": "string",
  "name": "string",
  "description": "string"
}

```

### 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|string|true|none||none|
|name|string|true|none||none|
|description|string|true|none||none|

<h2 id="tocS_ConversationDTO">ConversationDTO</h2>

<a id="schemaconversationdto"></a>
<a id="schema_ConversationDTO"></a>
<a id="tocSconversationdto"></a>
<a id="tocsconversationdto"></a>

```json
{
  "question": {
    "messageId": "string",
    "content": "string"
  },
  "answer": {
    "messageId": "string",
    "content": "string"
  }
}

```

### 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|question|[MessageDTO](#schemamessagedto)|true|none||The user's question.|
|answer|[MessageDTO](#schemamessagedto)|true|none||The user's question.|

<h2 id="tocS_返回模型">返回模型</h2>

<a id="schema返回模型"></a>
<a id="schema_返回模型"></a>
<a id="tocS返回模型"></a>
<a id="tocs返回模型"></a>

```json
{
  "code": 0
}

```

### 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|code|integer|true|none|业务码|Status code. 0 indicates that the operation is successful. Otherwise, the operation fails. Possible error codes include: <br/><br />100: Bad request. <br/><br />201: Request frequency limit. <br/><br />9999: Internal error. <br/><br />100001: Invalid operation.|

<h2 id="tocS_answerConfig">answerConfig</h2>

<a id="schemaanswerconfig"></a>
<a id="schema_answerConfig"></a>
<a id="tocSanswerconfig"></a>
<a id="tocsanswerconfig"></a>

```json
{
  "modelId": "string",
  "maxTokens": 0,
  "temperature": 0
}

```

### 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|modelId|string|true|none|模型Id|claude-3-h|
|maxTokens|integer|false|none|answer的maxTokens|none|
|temperature|number|false|none||none|

