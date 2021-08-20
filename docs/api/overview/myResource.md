**接口描述**

> 通过当前登陆用户，获取其数据权限范围内的如下信息：
> 1. 云平台纳管实例和告警云平台数量
> 2. 云平台资源池下所有资源的CPU总核数、总内存大小、存储总容量、CPU分配率、内存分配率和存储分配率

**请求URL**

- ` /oss-monitor/overview/my-resource`

**请求方式**

- `GET`

**请求参数**

无

**请求示例**

> http://ip:port/oss-monitor/overview/my-resource

**返回示例**

```
{
    "code": 0,
    "msg": "success",
    "data": {
        "platformInfo": {
            "manageNum": 10,
            "alarmNum": 1
        },
        "metrics": {
            "cpuTotal": 40,
            "cpuAllocationRate": 0.14,
            "memTotal": 80,
            "memAllocationRate": 0.10,
            "diskTotal": 1000,
            "diskAllocationRate": 0.25
        }
    }
}
```

**返回参数说明**

| 参数名称                       | 参数说明                          | 类型    |
| ------------------------------ | --------------------------------- | ------- |
| code                           | 返回标记：成功标记=0，失败标记非0 | integer |
| msg                            | 返回信息                          | string  |
| data                           | 查询数据                          | object  |
| &emsp;platformInfo             | 平台信息                          | object  |
| &emsp;&emsp;manageNum          | 纳管云平台数量                    | integer |
| &emsp;&emsp;alarmNum           | 告警云平台数量                    | integer |
| &emsp;metrics                  | 指标信息                          | object  |
| &emsp;&emsp;cpuTotal           | cpu总核数                         | integer  |
| &emsp;&emsp;cpuAllocationRate  | cpu分配率                         | double  |
| &emsp;&emsp;memTotal           | 总内存                            | double  |
| &emsp;&emsp;memAllocationRate  | 内存分配率                        | double  |
| &emsp;&emsp;diskTotal          | 存储总量                          | double  |
| &emsp;&emsp;diskAllocationRate | 存储分配率                        | double  |


