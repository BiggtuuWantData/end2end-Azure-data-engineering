# Azure End to End Data Engineering Project (Practice)

## Introduction
โปรเจคนี้จะแสดงถึงขั้นตอนการทำ ETL และการ Analytics โดยการใช้ Azure มาเป็นส่วนสำคัญในการทำงานทั้งหมดแบบ end to end เพราะ Microsoft Azure มี services ที่ครอบคลุมทั้งหมดในการจัดการด้าน Data  เช่น Databrick, Datalake/Warehouse, Datafactory และอื่นๆ โดยอีกทั้งยังสามารถกำหนด security(key-vault) ให้กับข้อมูลนั้นๆได้อย่างดี โดยวัตถุประสงค์ในการทำโปรเจคนี้เพื่อฝึกฝน วิเคราะห์ข้อมูลในขั้นตอนต่างๆที่เป็นพื้นฐานสำคัญในการจัดการข้อมูลไม่ว่าจะเป็น Data ingestion, Data transform, clustering data และไปจนถึงการทำ visualizataion

## Architecture Diagram
![image alt](https://github.com/BiggtuuWantData/end2end-Azure-data-engineering/blob/main/data%20factory/workflow%20architecture.png)
**รูปนี้แสดงถึง workflow การทำงานของโปรเจคนี้**

SQLServer On-premise คือ Data source โดย Data factory จะทำ ingestion จาก SQLServer หลังจากนัั้นไปเก็บที่ Data lake(Data storage) เพื่อนำข้อมูลไปทำการ transfromation โดยจะเห็นว่าได้แบ่ง DB ย่อยใน data lake เป็น 3 ระดับ คือ bronze, silver และ gold ซึ่่ง 3 tier นี้จำทำการ transform ข้อมูล จาก bronze -> silver -> gold และจากนั้น Data Synapse จำทำการดึง data จาก DB gold (Data lake) มาทำการ analytics ที่ Power Bi เพื่อทำ visualization
## Azure Services
- Azure Data Factory
- Azure Data Lake
- Azure Data Brick
- Azure Synapse Analytics
## Data Source (SQLServer On-prem)
รูป
จากรูป คือข้อมูลใน SQLServer ที่จะนำมาทำการ ETL 
## Data Factory
![image alt](https://github.com/BiggtuuWantData/end2end-Azure-data-engineering/blob/main/data%20factory/workflow%20datafactory.png)
ทำการสร้าง pipeline
- Lookup : ดึงข้อมูลจากแหล่งข้อมูล (SQLServer) มาเก็บใน pipeline เพื่อนำค่าไปใช้ต่อใน Activities อื่น ๆ
- ForEach : ทำการ iterate table เพื่อเรียก table ที่อยู๋ schema นั้นๆมา ซึ่งใน ForEach จะที copydata
## Data Lake
## Data Brick
## Snynapse Analytics
## Power Bi
