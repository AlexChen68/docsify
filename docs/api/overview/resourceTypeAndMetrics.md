###  资源类型列表接口（4,10,12）

**简要描述**

- 资源类型列表接口，获取view_resource表存在的资源类型。

**请求URL**

- ` /oss-monitor/overview/resource/type/list`

**请求方式**
- GET

**请求参数**

无

**请求示例**

``` http
/oss-monitor/overview/resource/type/list
```

**返回示例**

```
{
    "code": 0,
    "msg": null,
    "data": [
        {
            "modelCode": "point_ecs",
            "modelName": "云服务器"
        },
       	{
            "modelCode": "point_ebs",
            "modelName": "云硬盘"
        },
        {
            "modelCode": "point_vpc",
            "modelName": "虚拟机"
        },
        {
            "modelCode": "point_eip",
            "modelName": "弹性IP EIP"
        }
    ]
}

```

**返回参数说明**

| 参数名称        | 参数说明                         | 类型           |
| --------------- | -------------------------------- | -------------- |
| code            | 返回标记：成功标记=0，失败标记=1 | integer(int32) |
| msg             | 返回信息                         | string         |
| data            | 资源类型的数据                   | object         |
| &emsp;modelCode | 资源类型编码                     | String         |
| &emsp;modelName | 资源类型名称                     | String         |

### 指标列表接口 （13）

**简要描述**

> 指标列表接口，根据资源类型编码（resourceCode）获取view_target表存在的利用率指标。

**请求URL**

- ` /oss-monitor/overview/resource/column/list`

**请求方式**

- GET

**请求参数**

| 参数名       | 参数位置 | 必选 | 类型   | 说明     |
| ------------ | -------- | ---- | ------ | -------- |
| modelCode | query    | 是   | String | 资源类型编码 |

**请求示例**

``` http
/oss-monitor/overview/resource/column/list?modelCode=point_ecs
```

**返回示例**

```
{
    "code": 0,
    "msg": null,
    "data": [
        {
            "configCode": "oss-overview",
            "configName": "oss概览页视图配置",
            "modelCode": "point_ecs",
            "modelName": "云服务器",
            "columnCode": "cpu_usage",
            "columnName": "CPU利用率"
        },
        {
            "configCode": "oss-overview",
            "configName": "oss概览页视图配置",
            "modelCode": "point_ecs",
            "modelName": "云服务器",
            "columnCode": "mem_usage",
            "columnName": "内存利用率"
        }
    ]
}

```

**返回参数说明**

| 参数名称           | 参数说明                         | 类型           |
| ------------------ | -------------------------------- | -------------- |
| code               | 返回标记：成功标记=0，失败标记=1 | integer(int32) |
| msg                | 返回信息                         | string         |
| data               | 资源类型的数据                   | object         |
| &emsp;configCode |     配置编码                     | String         |
| &emsp;configName |     配置名称                     | String         |
| &emsp;modelCode |     资源类型编码                     | String         |
| &emsp;modelName |     资源类型名称                     | String         |
| &emsp;columnCode |    属性编码                     | String         |
| &emsp;columnName |    利用率名称                     | String         |

