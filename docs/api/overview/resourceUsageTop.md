**简要描述**

> 根据当前登陆用户的数据权限，根据所选的资源类型和指标，获取按指标排行的前10的资源数量
> 查询可以按照资源类型及时间范围筛选

**请求URL**

```http request
/oss-view/overview/resource/metrics/rank
```

**请求方式**
- `GET`

**请求参数**

| 参数名 | 参数位置 | 必选 | 类型 | 说明 |
| ------ | -------- | ---- | ---- | ---- |
|    resourceCode    |      query    |    是  |   string   |   资源类型编码，例如"point_ecs"   |
|    metricsCode    |      query    |    是  |   string   |   资源指标编码，例如"cpu_usage"   |
|    startTime    |      query    |    是  |   long   |   查询开始时间，格式为13位时间戳，查询的范围为开始时间到结束时间   |
|    endTime    |      query    |    否  |   long   |   查询结束时间，格式为13位时间戳，为空时默认取请求时间  |
|    size    |      query    |    否  |   integer   |   返回数据量限制，默认不限制   |

**请求示例**

```http
http://ip:port/oss-view/overview/resource/metrics/rank?resourceCode=point_ecs&metricsCode=cpu_usage&startTime=1629388800000&size=10
```

**返回示例**

```
{
    "code": 0,
    "msg": "success",
    "data": [
        {
            "uuid": "15678946164815654",
            "objectName": "云服务器1",
            "metricsValue": 0.88 
        },
        {
            "uuid": "15678946135465367",
            "objectName": "云服务器2",
            "metricsValue": 0.81
        }
    ]
}
```

**返回参数说明**

| 参数名称 | 参数说明                          | 类型           |
| -------- | --------------------------------- | -------------- |
| code     | 返回标记：成功标记=0，失败标记非0 | integer(int32) |
| msg      | 返回信息                          | string         |
| data     | 数据        | array         |
| &emsp;uuid     | 实例uuid        | string         |
| &emsp;objectName     | 实例名称       | string         |
| &emsp;metricsValue     | 指标值        | string         |
