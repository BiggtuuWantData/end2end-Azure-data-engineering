# Azure End to End Data Engineering Project (Practice)

## Introduction
โปรเจคนี้จะแสดงถึงขั้นตอนการทำ ETL และการ Analytics โดยการใช้ Azure มาเป็นส่วนสำคัญในการทำงานทั้งหมดแบบ end to end เพราะ Microsoft Azure มี services ที่ครอบคลุมทั้งหมดในการจัดการด้าน Data  เช่น Databrick, DataLake/Warehouse, Datafactory และอื่นๆ โดยอีกทั้งยังสามารถกำหนด security ให้กับข้อมูลนั้นๆได้อย่างดี
โดยวัตถุประสงค์ในการทำโปนเจคนี้เพื่อฝึกฝน วิเคราะข้อมูลในขั้นตอนต่างๆที่เป็นพื้นฐานสำคัญในการจัดการข้อมูลไม่ว่าจะเป็น Data ingestion, Data transform, clustering data และไปจนถึงการทำ visualiztaion

## Architecture Diagrams
![image alt](https://github.com/BiggtuuWantData/end2end-Azure-data-engineering/blob/main/data%20factory/workflow%20architecture.png)
**รูปนี้แสดงถึง workflow การทำงานของโปรเจคนี้**
SQLServer On-premise คือ Data source โดย Data factory จะทำ Data ingestion จาก SQLServer หลังจากนัั้นไปเก็บที่ Data lake(Data storage) เพื่อทำข้อมูลไปทำ Data transfrom โดยจะเห็นว่าได้แบ่ง DB ย่อยใน data lale เป็น 3 ระดับ คือ bronze, silver และ gold ซึ่่ง 3 tier นี้จำทำการ transform ข้อมูล จาก bronze -> silver -> gold และจากนั้น Data Synapse จำทำการดึง data จาก DB gold (Data lake) มาทำการ analytics ที่ Power Bi 

## Azure Services
- Azure Data Factory
- Azure Data Lake
- Azure Data Brick
- Azure Synapse Analytics
