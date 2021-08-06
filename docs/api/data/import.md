**简要描述**

- 资源数据 `Excel` 导入接口

**请求URL**

- ` /cm-engine/data/excel/import`

**请求方式**

- `POST`

**请求头**

| Key          | Value               |
| ------------ | ------------------- |
| Content-Type | multipart/form-data |

**请求参数**

| 参数名       | 参数位置 | 必选 | 类型   | 说明     |
| ------------ | -------- | ---- | ------ | -------- |
| modelingCode | query    | 是   | string | 模型编码 |
| file         | form     | 是     | binary | 上传的二进制文件 |

**请求示例**

* 请求路径

> http://ip:port/cm-engine/data/excel/import?modelingCode=point_ecs

* Form参数

> --form 'file=@"/C:/Users/admin/Desktop/cmdb_import_point_ecs.xlsx"'

**成功返回示例**

```json
{
    "code": 0,
    "data": true,
    "msg": "导入成功"
}
```

**失败返回示例**

```json
{
    "code": 1,
    "data": false,
    "msg": "导入失败"
}
```

**返回参数说明**

| 参数名称 | 参数说明                          | 类型           |
| -------- | --------------------------------- | -------------- |
| code     | 返回标记：成功标记=0，失败标记非0 | integer(int32) |
| msg      | 返回信息                          | string         |
| data     | true：成功；false：失败           | boolean        |

