**接口描述**

> 根据当前用户权限信息，获取所能查看的资源实例中，各个等级的告警数量，每个实例仅计算一次最高告警等级

**请求URL**

- `/oss-monitor/overview/alarm/summary`

**请求方式**

- Get

**head参数**

| 参数名称     | 必选 | 类型   | 默认值           |
| ------------ | ---- | ------ | ---------------- |
| Content-Type | 是   | string | application/json |

**请求参数**

无

**请求示例**

```http
/oss-monitor/overview/alarm/summary
```

**返回参数说明**

| 节点                      | 类型      | 描述             |
| ------------------------- | --------- | ---------------- |
| msg                       | string    | 操作返回信息     |
| code                      | int       | 成功1 ；失败0    |
| data                      | ArrayList | 返回数据信息结果 |
| &emsp;level         | int       | 告警等级枚举     |
| &emsp;levelName       | string    | 告警名称         |
| &emsp;instanceCount | int       | 告警数量         |



**返回示例**

```json
{
    "msg":"",
    "code": 0,
    "data": [
        {
            "level": 0,
            "levelName": "一般",
            "instanceCount": 99
        },
        {
            "level": 4,
            "levelName": "严重",
            "instanceCount": 99
        }
    ]
}
```
