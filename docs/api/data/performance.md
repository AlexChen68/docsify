#### 条件查询时序数据

**接口地址**:`/cm-engine/api/data/performance/query/list`

**请求方式**:`POST`

**请求数据类型**:`application/json`

**响应数据类型**:`*/*`

**接口描述**:条件查询时序数据

**特别说明**: 当查询的属性只有一个时，可指定该属性的条件；当查询的属性为多个时，仅可指定`uuid`和`time`的条件

**请求参数**:

| 参数名称      | 参数说明                     | in    | 是否必须 | 数据类型           |
| ------------- | ---------------------------- | ----- | -------- | ------------------ |
| modelingCode  | 建模编码                     | query | true     | string             |
| wrapper       | 查询条件构造器               | body  | true     | InfluxQueryWrapper |
| isToCamelCase | 属性是否转成驼峰，默认为true | query | false    | boolean            |

**响应状态**:

| 状态码 | 说明         |
| ------ | ------------ |
| 200    | OK           |
| 201    | Created      |
| 401    | Unauthorized |
| 403    | Forbidden    |
| 404    | Not Found    |

**响应参数**:

| 参数名称 | 参数说明                         | 类型           |
| -------- | -------------------------------- | -------------- |
| code     | 返回标记：成功标记=0，失败标记=1 | integer(int32) |
| data     | 数据                             | array          |
| msg      | 返回信息                         | string         |

**请求示例：**

请求接口：`**http://127.0.0.1:9999/cm-engine/api/data/performance/query/list?modelingCode=point_website`

请求BODY：

```
{
    "columns": [
        {
            "key": "website_dnstime_extranet"
        }
    ],
    "condition": [
        {
            "key": "uuid",
            "nested": false,
            "sqlKeyword": "EQ",
            "value": "1394830586829824002"
        },
        "AND",
        {
            "key": "time",
            "nested": false,
            "sqlKeyword": "GE",
            "value": "2021-06-08 00:00:00"
        },
        "AND",
        {
            "key": "time",
            "nested": false,
            "sqlKeyword": "LE",
            "value": "2021-06-09 23:59:59"
        }
    ]
}
```

**响应示例**:

```
{
    "code": 0,
    "msg": "query success",
    "data": [
        {
            "websiteDnstimeExtranet": 0.0,
            "time": "2021-06-08T15:05:00+08:00",
            "uuid": "1394830586829824002"
        },
        {
            "websiteDnstimeExtranet": 0.0,
            "time": "2021-06-08T14:45:00+08:00",
            "uuid": "1394830586829824002"
        }
    ]
}
```



#### 插入单条性能数据



**接口地址**:`/cm-engine/api/data/performance/save`



**请求方式**:`POST`



**请求数据类型**:`application/json`



**响应数据类型**:`*/*`



**接口描述**:插入一条记录，需要携带资源实例的uuid



**请求参数**:

| 参数名称     | 参数说明               | in    | 是否必须 | 数据类型       |
| ------------ | ---------------------- | ----- | -------- | -------------- |
| data         | 插入的数据             | body  | true     | Object         |
| modelingCode | 建模编码               | query | true     | string         |
| time         | 采集时间（13位时间戳） | query | true     | integer(int64) |



**响应状态**:

| 状态码 | 说明         |
| ------ | ------------ |
| 200    | OK           |
| 201    | Created      |
| 401    | Unauthorized |
| 403    | Forbidden    |
| 404    | Not Found    |



**响应参数**:

| 参数名称 | 参数说明                         | 类型           |
| -------- | -------------------------------- | -------------- |
| code     | 返回标记：成功标记=0，失败标记=1 | integer(int32) |
| data     | 数据                             | boolean        |
| msg      | 返回信息                         | string         |



**响应示例**:



```
{
    "code": 0,
    "data": true,
    "msg": ""
}
```



#### 批量插入性能数据



**接口地址**:`/cm-engine/api/data/performance/save/batch`



**请求方式**:`POST`



**请求数据类型**:`application/json`



**响应数据类型**:`*/*`



**接口描述**:保存多条新数据，会返回实例的uuid列表



**请求参数**:

| 参数名称     | 参数说明               | in    | 是否必须 | 数据类型       |
| ------------ | ---------------------- | ----- | -------- | -------------- |
| data         | 插入的数据列表         | body  | true     | Set            |
| modelingCode | 建模编码               | query | true     | string         |
| time         | 采集时间（13位时间戳） | query | true     | integer(int64) |



**响应状态**:

| 状态码 | 说明         |
| ------ | ------------ |
| 200    | OK           |
| 201    | Created      |
| 401    | Unauthorized |
| 403    | Forbidden    |
| 404    | Not Found    |



**响应参数**:

| 参数名称 | 参数说明                         | 类型           |
| -------- | -------------------------------- | -------------- |
| code     | 返回标记：成功标记=0，失败标记=1 | integer(int32) |
| data     | 数据                             | boolean        |
| msg      | 返回信息                         | string         |



**响应示例**:



```
{
    "code": 0,
    "data": true,
    "msg": ""
}
```

