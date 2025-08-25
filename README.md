# Azure End to End Data Engineering Project (Practice)

## Introduction
โปรเจคนี้จะแสดงถึงขั้นตอนการทำ ETL และการ Analytics โดยการใช้ Azure มาเป็นส่วนสำคัญในการทำงานทั้งหมดแบบ end to end เพราะ Microsoft Azure มี services ที่ครอบคลุมทั้งหมดในการจัดการด้าน Data  เช่น Databrick, Datalake/Warehouse, Datafactory และอื่นๆ โดยอีกทั้งยังสามารถกำหนด security(key-vault) ให้กับข้อมูลนั้นๆได้อย่างดี โดยวัตถุประสงค์ในการทำโปรเจคนี้เพื่อฝึกฝน วิเคราะห์ข้อมูลในขั้นตอนต่างๆที่เป็นพื้นฐานสำคัญในการจัดการข้อมูลไม่ว่าจะเป็น Data ingestion, Data transform, clustering data และไปจนถึงการทำ visualizataion

## Architecture Diagram
![image alt](https://github.com/BiggtuuWantData/end2end-Azure-data-engineering/blob/main/data%20factory/workflow%20architecture.png)
**รูปนี้แสดงถึง workflow การทำงานของโปรเจคนี้**

SQLServer On-premise คือ Data source โดย Data factory จะทำ ingestion จาก SQLServer หลังจากนัั้นไปเก็บที่ Data lake(Data storage) เพื่อนำข้อมูลไปทำการ transfromation โดยจะเห็นว่าได้แบ่ง DB ย่อยใน data lake เป็น 3 ระดับ คือ bronze, silver และ gold ซึ่่ง 3 tier นี้จำทำการ transform ข้อมูล จาก bronze -> silver -> gold และจากนั้น Data Synapse จำทำการดึง data จาก DB gold (Data lake) มาทำการ analytics ที่ Power Bi เพื่อทำ visualization
## Azure Services
- Azure Data Factory
- Azure Data Storage Gen2
- Azure Data Brick
- Azure Synapse Analytics
## Data Source (SQLServer On-prem)
![image alt](https://github.com/BiggtuuWantData/end2end-Azure-data-engineering/blob/main/data%20factory/dataset.png)
จากรูป คือข้อมูลใน SQLServer ที่จะนำมาทำการ ETL 
## Setup Services
- setup key-vault เพื่อกำหนด permission ในการเข้าถึงโดยเลือกที่ access control -> add -> เลือก key-vault secret user
- activies ต่างๆจะมีให้ linked service เข้ากับ sqlserver on-prem เลือก server name, data base name ให้ตรงกับ sql local และเลือก AKV linked service -> เลือก key-vault ที่เราทำการ setup ไว้ก่อนหน้านี้
- setup data storage gen 2 ไปที่ service data storage ที่เราสร้างไว้ -> storage -> container ทำการ add container 3 tier คือ bronze, silver, gold
## Data Ingestion Using Data Factory
![image alt](https://github.com/BiggtuuWantData/end2end-Azure-data-engineering/blob/main/data%20factory/workflow%20datafactory.png)
ทำการสร้าง pipeline
- Lookup : ดึงข้อมูลจากแหล่งข้อมูล (SQLServer) มาเก็บใน pipeline เพื่อนำค่าไปใช้ต่อใน Activities อื่น ๆ
- ForEach : ทำการ iterate table เพื่อเรียก table ที่อยู๋ schema นั้นๆมา ซึ่งใน ForEach จะที copydata
- Copy data : เปรียบเหมือน data lake ทำการ store data มาเก็บไว้เพื่อไปทำ data transform ต่อไป
- Databrick Notebook : transform data โดยในภาพเป็นการแบ่ง notebook เป็น 2 ส่วน คือ bronze to silver และ silver to gold 
## Data Transform Using Data Brick
รูป
1. Create Cluster
   - setting cluster เลือก compute
   - set node
2. Create Notebook
   - storagemount : ทำการ mount กับที่อยู่ไฟล์ใน data storage gen2 เ
   - transform : using pyspark ในการ transform data โดย notebook(bronze to silver) คือการเปลี่ยนแบบ fromat date, notebook(silver to gold) คือการเปลี่ยน column name ให้อยู่ในรูปแบบที่อ่านง่ายขึ้น
## Synapse Analytics
![image alt](https://github.com/BiggtuuWantData/end2end-Azure-data-engineering/blob/main/data%20factory/pipeline%20synapse.png)
- สร้าง db_gold เพื่อทำการ store data 


