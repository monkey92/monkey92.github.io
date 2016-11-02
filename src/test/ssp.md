
# 2016-09-12

## 用户角色
1. 管理员（添加处理人员/处理反馈/任务分配）
2. 处理人员（App的使用者）


## 基础数据
1. 本地区域列表
2. 地区与设备之间的关联

## 接口数据
1. 国控数据接口
2. 检测数据接口

### 国控数据接口示例
暂无

### 检测数据接口示例

1. 按时间点获得设备采集的数据(根据设备查询)
   
   ```
   get: http://host/fetch_by_machine/  
   args: machine_id,time

   example: http://host/fetch_by_machine?machine_id=1&time=201609121600
   return:  
   {
       "machine_name":"设备检测的具体地方(工地名称/街道名称)",
       "machine_position":["经度","纬度"],
       "PM10"："2.29",
       "PM25":"1.43",
       "db":"61.4",
       "time":"09-12 16:00",
       "pic":"http://host/images/machine_id/201609121630.jpg"
   }

   ```

2. 按时间段获得设备采集的数据(根据设备查询)  
   
   ```
   get: http://host/fefetch_by_machinetch/  
   args: machine_id,start_time,end_time
   
   example: http://host/fetch_by_machine?machine_id=1&start_time=201609120800&end_time=201609121500
   return:  
    {
        "0800":{
            "machine_name":"设备检测的具体地方(工地名称/街道名称)",
            "machine_position":["经度","纬度"],
            "PM10"："2.29",
            "PM25":"1.43",
            "db":"61.4",
            "time":"09-12 08:00",
            "pic":"http://host/images/machine_id/201609121630.jpg"
        },
        "0900":{
            "machine_name":"设备检测的具体地方(工地名称/街道名称)",
            "machine_position":["经度","纬度"]
            "PM10"："2.29",
            "PM25":"1.43",
            "db":"61.4",
            "time":"09-12 09:00",
            "pic":"http://host/images/machine_id/201609121630.jpg"
        }
        "1000":{
            "machine_name":"设备检测的具体地方(工地名称/街道名称)",
            "machine_position":["经度","纬度"],
            "PM10"："2.29",
            "PM25":"1.43",
            "db":"61.4",
            "time":"09-12 10:00",
            "pic":"http://host/images/machine_id/201609121630.jpg"
        }
        // ...
        "1500":{
            "machine_name":"设备检测的具体地方(工地名称/街道名称)",
            "machine_position":["经度","纬度"],
            "PM10"："2.29",
            "PM25":"1.43",
            "db":"61.4",
            "time":"09-12 15:00",
            "pic":"http://host/images/machine_id/201609121630.jpg"
        }

    }

   ```
3. 按地区查找设备

   ```
   get: http://host/machine_list/  
   args: region_id

   example: http://host/machine_list?region_id=1
   return:  
   [
       {    
            "machine_id":1,
            "machine_name":"设备检测的具体地方(工地名称/街道名称)",
            "machine_position":["经度","纬度"],
        },
        {
            "machine_id":2,
            "machine_name":"设备检测的具体地方(工地名称/街道名称)",
            "machine_position":["经度","纬度"],
        },
        {
            "machine_id":3,
            "machine_name":"设备检测的具体地方(工地名称/街道名称)",
            "machine_position":["经度","纬度"],
        }
   ]

   ```

4. 按区域查询检测参数

   ```
   get: http://host/fetch_by_region/  
   args: region_id,time

   example: http://host/fetch_by_region?region_id=1&time=201609121600
   return:  
   {
       "region_name":"区域名称",
       "region_position":["经度","纬度"],
       "PM10"："2.29",
       "PM25":"1.43",
       "db":"61.4",
       "time":"09-12 16:00",
   }

   ```
5. 按区域查询检测参数

   ```
   get: http://host/fetch_by_region/  
   args: region_id,start_time,end_time

   example: http://host/fetch_by_region?region_id=1&start_time=201609120800&end_time=201609121500
   return:  
   {
        "0800":{
            "region_name":"区域名称",
            "region_position":["经度","纬度"],
            "PM10"："2.29",
            "PM25":"1.43",
            "db":"61.4",
            "time":"09-12 08:00",
        },
        "0900":{
            "region_name":"区域名称",
            "region_position":["经度","纬度"]
            "PM10"："2.29",
            "PM25":"1.43",
            "db":"61.4",
            "time":"09-12 09:00",
        }
        "1000":{
            "region_name":"区域名称",
            "region_position":["经度","纬度"],
            "PM10"："2.29",
            "PM25":"1.43",
            "db":"61.4",
            "time":"09-12 10:00",
        }
        // ...
        "1500":{
            "region_name":"区域名称",
            "region_position":["经度","纬度"],
            "PM10"："2.29",
            "PM25":"1.43",
            "db":"61.4",
            "time":"09-12 15:00",
        }
   }

   ```
    







