# Virtual Machine 

### 1. `创建按量主机`

**Path**

`POST`   ``https://stg-client.xuandashi.com/v1/pve/open/createquantity``

**Request paramerter**

| Parameter | Description | Required | Type   | Location |
| --------- | ----------- | -------- | ------ | -------- |
| packageId | 主机模板ID  | yes      | string | body     |
| imageId   | 镜像ID      | yes      | string | body     |

**Response Type**:application/json

**Response Example**

```json
{
    "code":0,
    "data":true,
    "msg":"success"
}
```

**code**

| 错误码 | 错误描述                     |
| ------ | ---------------------------- |
| 1001   | 权限不足                     |
| 7005   | 主机模板类型与镜像类型不一致 |

### 2. `创建包时段主机`

**Path**

`POST`   `https://stg-client.xuandashi.com/v1/pve/open/createRent`

**Request paramerter**

| Parameter    | Description                                      | Required | Type   | Location |
| ------------ | ------------------------------------------------ | -------- | ------ | -------- |
| packageId    | 主机模板ID                                       | yes      | string | body     |
| imageId      | 镜像ID                                           | yes      | string | body     |
| periodNumber | 购买周期                                         | yes      | int    | body     |
| periodType   | 购买周期类型（0小时、1日、2周、3月、4季度、5年） | yes      | int    | body     |

**Response Type**:application/json

**Responses Example**

```json
{
    "code":0,
    "data":true,
    "msg":"success"
}
```

**code**

| 错误码 | 错误描述                 |
| ------ | ------------------------ |
| 1001   | 权限不足                 |
| 1037   | 未进行实名认证           |
| 6002   | 资源不足, 请重新选择配置 |
| 6005   | 创建等待                 |
| 9000   | 钱包异常                 |
| 9001   | 钱包余额不足             |

### 3. `开机/关机`

**Path**

`GET`   `https://stg-client.xuandashi.com/v1/pve/open/operate/{id}`

**Request paramerter**

| Parameter | Description                     | Required | Type   | Location |
| --------- | ------------------------------- | -------- | ------ | -------- |
| id        | 主机ID                          | yes      | string | path     |
| type      | 0：关闭虚拟机     1：开启虚拟机 | yes      | string | query    |

**Response Type**:application/json

**Responses Example**

```json
{
    "code":0,
    "data":true,
    "msg":"success"
}
```

**code**

| 错误码 | 错误描述                 |
| ------ | ------------------------ |
| 1001   | 权限不足                 |
| 6000   | 开机中                   |
| 6001   | 关机中                   |
| 6002   | 资源不足, 请重新选择配置 |
| 6003   | 钱包余额不足             |

### 4. `重启`

**Path**

`GET `   `https://stg-client.xuandashi.com/v1/pve/open/reboot/{id}`

**Request paramerter**

| Parameter | Description | Required | Type   | Location |
| --------- | ----------- | -------- | ------ | -------- |
| id        | 主机ID      | yes      | string | path     |

**Response Type**:application/json

**Responses Example**

```json
{
    "code":0,
    "data":true,
    "msg":"success"
}
```

**code**

| 错误码 | 错误描述               |
| ------ | ---------------------- |
| 7002   | 未启动的主机不能重启   |
| 7003   | 虚拟机不可用，不能重启 |
| 7004   | 主机未运行，不能重启   |

### 5. `查询虚拟机信息` 

**Path**

``GET ``   ``https://stg-client.xuandashi.com/v1/pve/open/one/{id}``

**Request paramerter**

| Parameter | Description | Required | Type   | Location |
| --------- | ----------- | -------- | ------ | -------- |
| id        | 主机ID      | yes      | string | path     |

**Response Type**:application/json

**Responses Example**

```JSON
{
  "code":0,
  "data":{
    "id":"QzyHraLXEr",
    "name":"master_xuan",
    "gpuConfiguration":"GeForce GTX 1660 Ti/S 6G",
    "gpuNumber":2,
    "memory":8,
    "cpu":8,
    "rigidDisk":256,
    "operatingSystem":"Ubuntu Server",
    "hostAccount":"root",
    "hostPw":"***********",
    "address":"xxxx.xxx-xxx.com",
    "port":8080,
    "mac":"*********",
    "ipV4":"*********",
    "pveMachineType" :"0",
    "createTime":1695639270000,
    "expirationTime":1695639850000
  },
  "msg":"success"
}
```

| Responses Parameter | Description                                                 | Type   |
| :------------------ | :---------------------------------------------------------- | ------ |
| id                  | 主机ID                                                      | string |
| name                | 主机名称                                                    | string |
| gpuConfiguration    | GPU配置                                                     | string |
| gpuNumber           | GPU数量                                                     | int    |
| memory              | 内存数                                                      | int    |
| cpu                 | cpu核数                                                     | int    |
| rigidDisk           | 硬盘数                                                      | int    |
| operatingSystem     | 操作系统（Windows,Windows Server,Ubuntu Server,Debian）     | string |
| hostAccount         | 用户名（登录用户名）                                        | string |
| address             | 主机连接地址                                                | string |
| port                | 主机连接端口                                                | int    |
| pveMachineType      | 主机使用范围，用途（0：普通办公、1：图像处理、2：算法区域） | string |
| createTime          | 主机创建时间                                                | long   |
| expirationTime      | 主机到期时间，有可能为空                                    | long   |
| mac                 | MAC地址                                                     | string |
| ipV4                | ip地址                                                      | string |

### 6. `批量查询虚拟机信息` 

**Path**

`GET`   `https://stg-client.xuandashi.com/v1/pve/open/mypage`

**Request paramerter**

| Parameter | Description                    | Required | Type    | Location |
| --------- | ------------------------------ | -------- | ------- | -------- |
| page      | 起始页                         | yes      | integer | query    |
| pageSize  | 页大小，单次最多只支持查询25条 | yes      | integer | query    |

**Response Type**:application/json

**Responses Example**

```json
{
    "code":0,
    "data":{"data":
    [
       {
           "id":"QzyHraLXEr",
           "name":"master_xuan",
           "gpuConfiguration":"GeForce GTX 1660 Ti/S 6G",
           "gpuNumber":2,
           "memory":8,
           "cpu":8,
           "rigidDisk":256,
           "operatingSystem":"Ubuntu Server",
           "hostAccount":"root",
           "hostPw":"***********",
           "address":"xxxx.xxx-xxx.com", 
           "port":8080,
           "pveMachineType" :"0",
           "createTime":1695639270000,
           "expirationTime":1695639850000
       }
    ],
    "totalCounts":1
 },
    "msg":"success"
}
```

| Responses Parameter | Description                                                 | Type   |
| :------------------ | :---------------------------------------------------------- | ------ |
| id                  | 主机ID                                                      | string |
| name                | 主机名称                                                    | string |
| gpuConfiguration    | GPU配置                                                     | string |
| gpuNumber           | GPU数量                                                     | int    |
| memory              | 内存数                                                      | int    |
| cpu                 | cpu核数                                                     | int    |
| rigidDisk           | 硬盘数                                                      | int    |
| operatingSystem     | 操作系统（Windows,Windows Server,Ubuntu Server,Debian）     | string |
| hostAccount         | 用户名（登录用户名）                                        | string |
| address             | 主机连接地址                                                | string |
| port                | 主机连接端口                                                | int    |
| pveMachineType      | 主机使用范围，用途（0：普通办公、1：图像处理、2：算法区域） | string |
| createTime          | 主机创建时间                                                | long   |
| expirationTime      | 主机到期时间，有可能为空                                    | long   |

### 7. `删除虚拟机`

**Path**

`DELETE`   `https://stg-client.xuandashi.com/v1/pve/open/delete/{id}`

**Response Type**:application/json

**Request paramerter**

| Parameter | Description | Required | Type   | Location |
| --------- | ----------- | -------- | ------ | -------- |
| id        | 主机ID      | yes      | string | path     |

**Responses Example**

```json
{
    "code":0,
    "data":true,
    "msg":"success"
}
```

**code**

| 错误码 | 错误描述 |
| ------ | -------- |
| 1001   | 权限不足 |

### 8. `主机模板信息`

**Path**

`GET`   `https://stg-client.xuandashi.com/v1/pve/open/packAge/{type}`

**Request paramerter**

| Parameter | Description                | Required | Type   | Location |
| --------- | -------------------------- | -------- | ------ | -------- |
| type      | 模板类型（0按量、1包时段） | yes      | string | path     |

**Response Type**:application/json

**Responses Example**

```json
{
    "code":0,
    "data":[
        {
            "packageId":"Pi8tcH1NSd",
            "name":"图像处理-Ubuntu",
            "memoryNumber":16,
            "rigidDiskNumber":512,
            "amount":5.00,
            "cpuNumber":16,
            "bandWidth":8,
            "type":"BZ",
            "pveMachineType":"1",
            "area":"2",
            "useType":"2",
            "discount":0.9
        }
    ],
    "msg":"success"
}
```

| Responses Parameter | Description                                                  | Type   |
| ------------------- | ------------------------------------------------------------ | ------ |
| packageId           | 主机模板ID                                                   | string |
| name                | 主机模板名称                                                 | string |
| gpuNumber           | GPU数                                                        | int    |
| memoryNumber        | 内存数                                                       | int    |
| rigidDiskNumber     | 硬盘数                                                       | int    |
| cpuNumber           | cpu数                                                        | int    |
| bandWidth           | 带宽                                                         | int    |
| amount              | 金额                                                         | string |
| discount            | 折扣                                                         | string |
| type                | 主机模板类型                                                 | string |
| pveMachineType      | 主机用途（0普通办公、1图像处理、2算法区域）                  | string |
| area                | 数据中心（0华南、1华西、国际）                               | string |
| useType             | 主机使用类型（0仅支持按量、1仅支持包时段、2支持按量和包时段） | string |

### 9. `镜像信息`

**Path**

`GET`   `https://stg-client.xuandashi.com/v1/pve/open/image`

**Request paramerter**

`none`

**Response Type**:application/json

**Responses Example**

```json
{
    "code":0,
    "data":[
        {
            "imageId":"8989",
            "type":"BZ",
            "systemImageName":"Windown Server",
            "systemImageVersion":"2022 数据中心中文版 x64"
        }
    ],
    "msg":"success"
}
```

| Responses Parameter | Description  | Type   |
| :------------------ | :----------- | ------ |
| imageId             | 镜像ID       | string |
| type                | 镜像类型     | string |
| systemImageName     | 镜像系统     | string |
| systemImageVersion  | 镜像系统版本 | string |