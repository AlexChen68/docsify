**简要描述**

- 资源数据 `Excel` 导入模版下载接口

**请求URL**

- ` /cm-engine/data/excel/import/template`

**请求方式**

- `GET`

**请求参数**

| 参数名       | 参数位置 | 必选 | 类型   | 说明     |
| ------------ | -------- | ---- | ------ | -------- |
| modelingCode | query    | 是   | string | 模型编码 |

**请求示例**

* 请求路径

> http://ip:port/cm-engine/data/excel/import/template?modelingCode=point_ecs

**返回参数说明**

> 返回的为导出模版的二进制文件，保存为本地文件即可

