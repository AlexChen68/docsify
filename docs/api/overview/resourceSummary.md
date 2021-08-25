**接口描述**

> 根据当前用户权限信息，获取所能查看的资源实例中，各个资源的告警实例数量及纳管数量。

**请求URL**

- `/oss-monitor/overview/resource/summary`

**请求方式**

- `Get`

**head参数**

| 参数名称     | 必选 | 类型   | 默认值           |
| ------------ | ---- | ------ | ---------------- |
| Content-Type | 是   | string | application/json |

**请求参数**

| 参数名          | 必选 | in    | 类型   | 说明     |
| --------------- | ---- | ----- | ------ | -------- |
| cloudPlatformId | 否   | query | string | 所属平台 |
| modelCodeList | 是   | body | array | 请求查询的模型列表，不可为空 |

**请求示例**

**url**

```http
/oss-monitor/overview/resource/summary?cloudPlatformId=xxx
```


**body**

```json
{
  "modelCodeList":[
    "point_ecs",
    "point_ebs"
  ]
}
```

**返回参数说明**

| 节点                     | 类型      | 描述             |
| ------------------------ | --------- | -------------- |
| msg                      | string    | 操作返回信息     |
| code                     | int       | 成功1 ；失败0    |
| data                     | Object    | 返回数据信息结果  |
| &emsp;modelCode          | String    | 资源类型编码     |
| &emsp;manageNum          | int       | 纳管实例数       |
| &emsp;alarmNum           | int       | 告警实例数       |

**返回示例**

```json
{
    "code": 0,
    "msg": null,
    "data": [
        {
            "modelCode": "point_ecs",
            "manageNum": "20",
            "alarmNum": "10"
        },
        {
            "modelCode": "point_ebs",
            "manageNum": "18",
            "alarmNum": "12"
        }
    ]
}
```
