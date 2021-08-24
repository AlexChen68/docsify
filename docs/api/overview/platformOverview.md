### 云平台列表接口（6）

**简要描述**

- 云平台列表接口，获取view_platform表存在的云平台实例。

**请求URL**

- ` /oss-monitor/overview/viewplatform/list`

**请求方式**

- GET

**请求参数**

无

**请求示例**

``` http
/oss-monitor/overview/viewplatform/list
```

**返回示例**

```
{
    "code": 0,
    "msg": null,
    "data": [
        {
            "platformType": "OpenStack",
            "platformList": [
                {
                    "platformUuid": "1429692502677024769",
                    "platformName": "OpenStack平台001"
                },
                {
                    "platformUuid": "1429696427606044673",
                    "platformName": "OpenStack平台002"
                }
            ]
        },
        {
            "platformType": "VMware",
            "platformList": [
                {
                    "platformUuid": "1429692502677029102",
                    "platformName": "VMware平台001"
                }
            ]
        }
    ]
}
```

**返回参数说明**

| 参数名称           | 参数说明                         | 类型           |
| ------------------ | -------------------------------- | -------------- |
| code               | 返回标记：成功标记=0，失败标记=1  | integer(int32) |
| msg                | 返回信息                      | string         |
| data               | 云平台实例的数据                | object         |
| &emsp;platformType | 云平台类型名称                  | string         |
| &emsp;platformList | 类型下的云平台                  | array         |
| &emsp;&emsp;platformUuid | 云平台编码                  | string         |
| &emsp;&emsp;platformName | 云平台名称                  | string         |

### 云平台年度SLA接口（7）

**接口描述**

> 根据平台id获取年度sla，年度故障，月度故障，周度故障。

**请求URL**

-  `/oss-monitor/overview/sla`

**请求方式**

- `Get`

**head参数**

|参数名称|必选|类型|默认值|
|------------|----|------|----------------|
|Content-Type|是|string|application/json|

**请求参数**

|参数名|必选|参数位置|类型|说明|
|---------------------|----|----|-------|--------------------------------------------|
|cloudPlatformId|是|query|string|所属平台|

**请求示例**

```http
/oss-monitor/overview/sla?cloudPlatformId=xxx
```

**返回参数说明**

|节点|父节点|类型|描述|
|----------------------------------|--------|----------------------------------------------------|----------------------------------------------------|
|msg||string|操作返回信息|
|code||int|成功1 ；失败0|
|data||Object|返回数据信息结果|
|&emsp;yearSla| data | float  |年度sla|
|&emsp;yearFault|data|string|年度故障|
|&emsp;monthFault|data| string |月度故障|
|&emsp;weekFault|data| string |周度故障|
|&emsp;cloudPlatformId|data|string|所属平台|

**返回示例**

```json
{
    "code": 1,
    "msg": null,
    "data": {
        "yearSla": "98%",
        "yearFault": "53",
        "monthFault": "23",
        "weekFault": "10",
        "cloudPlatformId": "xxx"
    }
}
```

### [资源统计接口（8）](/api/overview/resourceSummary?id=资源统计接口（5，8）"资源统计接口") 

### 云平台资源分配概览接口(9)
**简要描述**

> 获取所选云平台下，在当前登陆用户数据权限范围内的资源指标信息，包括资源的CPU总核数、CPU利用率、CPU分配率、内存总量、内存利用率、内存分配率、存储总量、存储利用率和存储分配率

**请求URL**

```http
/oss-monitor/overview/metrics
```

**请求方式**
- `GET`

**请求参数**

|参数名|必选|参数位置|类型|说明|
|---------------------|----|----|-------|--------------------------------------------|
|cloudPlatformId|是|query|string|所属平台|

**请求示例**

```http
http://ip:port/oss-monitor/overview/metrics?cloudPlatformId=xxx
```

**返回示例**

```
{
    "code": 0,
    "msg": null,
    "data": {
        "metrics": {
            "cpuTotal": 40,
            "cpuAllocationRate": 0.14,
            "cpuUsage": 0.40,
            "memTotal": 80,
            "memAllocationRate": 0.10,
            "memUsage": 0.20,
            "diskTotal": 1000,
            "diskAllocationRate": 0.25,
            "diskUsage": 0.25
        }
    }
}
```

**返回参数说明**

| 参数名称                       | 参数说明                          | 类型           |
| ------------------------------ | --------------------------------- | -------------- |
| code                           | 返回标记：成功标记=0，失败标记非0 | integer(int32) |
| msg                            | 返回信息                          | string         |
| data                           | 数据                              | object         |
| &emsp;metrics                  | 指标信息                          | object         |
| &emsp;&emsp;cpuTotal           | cpu总核数                         | integer        |
| &emsp;&emsp;cpuUsage           | cpu利用率                         | double         |
| &emsp;&emsp;cpuAllocationRate  | cpu分配率                         | double         |
| &emsp;&emsp;memTotal           | 总内存                            | double         |
| &emsp;&emsp;memUsage           | 内存利用率                        | double         |
| &emsp;&emsp;memAllocationRate  | 内存分配率                        | double         |
| &emsp;&emsp;diskTotal          | 存储总量                          | double         |
| &emsp;&emsp;diskUsage          | 存储利用率                        | double         |
| &emsp;&emsp;diskAllocationRate | 存储分配率                        | double         |

