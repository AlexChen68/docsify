#### 根据UUID删除

* **接口地址**:`/cm-engine/api/data/resource/delete`

*  **请求方式**:`POST`

*  **请求数据类型**:`application/json`

*  **响应数据类型**:`*/*`

*  **接口描述**:根据UUID删除

*  **请求参数**:

| 参数名称     | 参数说明 | in    | 是否必须 | 数据类型 |
| ------------ | -------- | ----- | -------- | -------- |
| modelingCode | 建模编码 | query | true     | string   |
| uuid         | uuid     | query | true     | string   |

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

```json
{
    "code": 0,
    "data": true,
    "msg": ""
}
```

------

#### 根据UUID删除（批量）

**接口地址**:`/cm-engine/api/data/resource/delete/batch`

**请求方式**:`POST`

**请求数据类型**:`application/json`

**响应数据类型**:`*/*`

**接口描述**:根据UUID删除（批量）

**请求参数**:

| 参数名称     | 参数说明 | in    | 是否必须 | 数据类型 |
| ------------ | -------- | ----- | -------- | -------- |
| modelingCode | 建模编码 | query | true     | string   |
| uuidSet      | uuid列表 | body  | true     | Set      |



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



#### 条件删除



**接口地址**:`/cm-engine/api/data/resource/delete/condition`



**请求方式**:`POST`



**请求数据类型**:`application/json`



**响应数据类型**:`*/*`



**接口描述**:根据wrapper构造出的条件删除记录



**请求参数**:

| 参数名称     | 参数说明       | in    | 是否必须 | 数据类型          |
| ------------ | -------------- | ----- | -------- | ----------------- |
| modelingCode | 建模编码       | query | true     | string            |
| wrapper      | 查询条件构造器 | body  | true     | MysqlQueryWrapper |



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



#### 根据UUID查询



**接口地址**:`/cm-engine/api/data/resource/query`



**请求方式**:`POST`



**请求数据类型**:`application/json`



**响应数据类型**:`*/*`



**接口描述**:根据UUID查询



**请求参数**:

| 参数名称      | 参数说明                     | in    | 是否必须 | 数据类型 |
| ------------- | ---------------------------- | ----- | -------- | -------- |
| modelingCode  | 建模编码                     | query | true     | string   |
| uuid          | uuid                         | query | true     | string   |
| isToCamelCase | 属性是否转成驼峰，默认为true | query | false    | boolean  |



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
| data     | 数据                             | object         |
| msg      | 返回信息                         | string         |



**响应示例**:



```
{
    "code": 0,
    "data": {},
    "msg": ""
}
```



#### 条件查询



**接口地址**:`/cm-engine/api/data/resource/query/list`



**请求方式**:`POST`



**请求数据类型**:`application/json`



**响应数据类型**:`*/*`



**接口描述**:条件查询



**请求参数**:

| 参数名称      | 参数说明                     | in    | 是否必须 | 数据类型          |
| ------------- | ---------------------------- | ----- | -------- | ----------------- |
| modelingCode  | 建模编码                     | query | true     | string            |
| wrapper       | 查询条件构造器               | body  | true     | MysqlQueryWrapper |
| isToCamelCase | 属性是否转成驼峰，默认为true | query | false    | boolean           |



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



**响应示例**:



```
{
    "code": 0,
    "data": [],
    "msg": ""
}
```



#### 条件查询单条记录



**接口地址**:`/cm-engine/api/data/resource/query/one`



**请求方式**:`POST`



**请求数据类型**:`application/json`



**响应数据类型**:`*/*`



**接口描述**:条件查询单条记录



**请求参数**:

| 参数名称      | 参数说明                     | in    | 是否必须 | 数据类型          |
| ------------- | ---------------------------- | ----- | -------- | ----------------- |
| modelingCode  | 建模编码                     | query | true     | string            |
| wrapper       | 查询条件构造器               | body  | true     | MysqlQueryWrapper |
| isToCamelCase | 属性是否转成驼峰，默认为true | query | false    | boolean           |



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
| data     | 数据                             | object         |
| msg      | 返回信息                         | string         |



**响应示例**:



```
{
    "code": 0,
    "data": {},
    "msg": ""
}
```



#### 分页条件查询



**接口地址**:`/cm-engine/api/data/resource/query/page`



**请求方式**:`POST`



**请求数据类型**:`application/json`



**响应数据类型**:`*/*`



**接口描述**:分页条件查询



**请求参数**:

| 参数名称      | 参数说明                     | in    | 是否必须 | 数据类型          |
| ------------- | ---------------------------- | ----- | -------- | ----------------- |
| modelingCode  | 建模编码                     | query | true     | string            |
| wrapper       | 查询条件构造器               | body  | true     | MysqlQueryWrapper |
| current       | 分页对象当前页码             | query | false    | integer(int64)    |
| isToCamelCase | 属性是否转成驼峰，默认为true | query | false    | boolean           |
| size          | 分页对象每页大小             | query | false    | integer(int64)    |



**响应状态**:

| 状态码 | 说明         |
| ------ | ------------ |
| 200    | OK           |
| 201    | Created      |
| 401    | Unauthorized |
| 403    | Forbidden    |
| 404    | Not Found    |



**响应参数**:

| 参数名称 | 参数说明                         | 类型             |
| -------- | -------------------------------- | ---------------- |
| code     | 返回标记：成功标记=0，失败标记=1 | integer(int32)   |
| data     | 数据                             | Page«JSONObject» |
| current  | 当前页码                         | integer(int64)   |
| records  | 数据列表                         | array            |
| size     | 单页大小                         | integer(int64)   |
| total    | 总条数                           | integer(int64)   |
| msg      | 返回信息                         | string           |



**响应示例**:



```
{
    "code": 0,
    "data": {
        "current": 0,
        "records": [
            {}
        ],
        "size": 0,
        "total": 0
    },
    "msg": ""
}
```



#### 插入一条记录



**接口地址**:`/cm-engine/api/data/resource/save`



**请求方式**:`POST`



**请求数据类型**:`application/json`



**响应数据类型**:`*/*`



**接口描述**:插入一条记录，无需携带uuid，自动使用雪花算法生成



**请求参数**:

| 参数名称     | 参数说明   | in    | 是否必须 | 数据类型 |
| ------------ | ---------- | ----- | -------- | -------- |
| data         | 插入的数据 | body  | true     | Object   |
| modelingCode | 建模编码   | query | true     | string   |



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



#### 插入（批量）



**接口地址**:`/cm-engine/api/data/resource/save/batch`



**请求方式**:`POST`



**请求数据类型**:`application/json`



**响应数据类型**:`*/*`



**接口描述**:插入（批量），无需携带uuid，自动使用雪花算法生成



**请求参数**:

| 参数名称     | 参数说明       | in    | 是否必须 | 数据类型 |
| ------------ | -------------- | ----- | -------- | -------- |
| dataList     | 插入的数据列表 | body  | true     | List     |
| modelingCode | 建模编码       | query | true     | string   |



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



#### 根据UUID修改



**接口地址**:`/cm-engine/api/data/resource/update`



**请求方式**:`POST`



**请求数据类型**:`application/json`



**响应数据类型**:`*/*`



**接口描述**:根据UUID修改，更新的实体中，uuid为查询条件，其他属性为set条件



**请求参数**:

| 参数名称     | 参数说明                                        | in    | 是否必须 | 数据类型 |
| ------------ | ----------------------------------------------- | ----- | -------- | -------- |
| data         | 更新的实体中，uuid为查询条件，其他属性为set条件 | body  | true     | Object   |
| modelingCode | 建模编码                                        | query | true     | string   |



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



#### 根据UUID修改（批量）



**接口地址**:`/cm-engine/api/data/resource/update/batch`



**请求方式**:`POST`



**请求数据类型**:`application/json`



**响应数据类型**:`*/*`



**接口描述**:根据UUID修改（批量），更新的实体，uuid为查询条件，其他属性为set条件



**请求参数**:

| 参数名称     | 参数说明                                                     | in    | 是否必须 | 数据类型 |
| ------------ | ------------------------------------------------------------ | ----- | -------- | -------- |
| dataList     | 更新的实体列表，每个实体中，uuid为查询条件，其他属性为set条件 | body  | true     | Set      |
| modelingCode | 建模编码                                                     | query | true     | string   |



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



#### 条件修改



**接口地址**:`/cm-engine/api/data/resource/update/condition`



**请求方式**:`POST`



**请求数据类型**:`application/json`



**响应数据类型**:`*/*`



**接口描述**:根据更新条件构造器条件修改



**请求参数**:

| 参数名称     | 参数说明       | in    | 是否必须 | 数据类型           |
| ------------ | -------------- | ----- | -------- | ------------------ |
| modelingCode | 建模编码       | query | true     | string             |
| wrapper      | 更新条件构造器 | body  | true     | MysqlUpdateWrapper |



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

