# PISA2022-Project
เป็น Research Assistance Project ของอาจารย์เศรษฐศาสตร์ธรรมศาสตร์ มธ. เกี่ยวข้องกับการวิเคราะห์ความเหลื่อมล้ำของคะแนน PISA ระหว่างเด็กในเมือง vs ชนบท 

## ข้อมูลที่เกี่ยวข้อง ##
1. Data Dictionary PISA2022 ฉบับ Spreadsheet สำหรับข้อมูลเปิดทั้งหมดที่อ่านง่ายมีทั้งชื่อตัวแปร/คำอธิบาย/ค่าที่เป็นไปได้ สามารถดูข้อมูล Original ได้ที่ link: https://webfs.oecd.org/pisa2022/index.html โดยข้อมูล PISA2022 จริงมีหลายไฟล์จึงทำ Data Dictionary แยกตามนั้น
2. Dataset ที่ใช้ในการวิเคราะห์ (.csv) ซึ่งผ่านการทำ Data Manipulation มาระดับหนึ่งทั้งการคำนวณคะแนน PISA ทั้ง 3 วิชาออกมาให้เหลือเพียงค่าเดียว, การ Grouping ข้อมูลการศึกษาของพ่อแม่ และอาชีพของพ่อแม่ที่ปรับจาก Occupation Code ให้เหลือ 4 กลุ่มตามมาตรฐาน ILO คือ Armed Force, Low Skills, Middle Skills, High Skills

## Code 
- 1_ConvertSPSS_to_CSV คือไฟล์ในการอ่านข้อมูล SPSS ของ PISA จาก Data Lake (Google Drive) เพื่อ Acquire Meta Data กับ Dataset ออกมา
- 2_Create_CSV_File คือไฟล์ในการสร้าง Dataset ตามข้อที่ 2 หัวข้อ 'ข้อมูลที่เกี่ยวข้อง' โดยเริ่มจากการปรับไฟล์ .csv ที่อ่านได้จากไฟล์ SPSS มาสร้าง Database (.db) ด้วย sqlite เพื่อให้ง่ายต่อการดึงข้อมูลรายคอลัมน์ ไม่ต้อง Import Dataset หลายๆ อันที่มีขนาดใหญ่มากเข้า Session ทีเดียว และหลังจากนั้นจึงทำการคัดเลือกเฉพาะตัวแปรที่เกี่ยวข้องกับการวิจัย (หรือทำ Project) เพื่อมารวมกันเป็นไฟล์เดียวและแปลงเป็น .csv ในที่สุด
- 3_Convert_BigCSV_to_PARQUET แต่ขนาดก็ยังใหญ่อยู่ดีเลยทำการแปลงเป็น .parquet และ Optimize file อื่นๆ เช่น ลดขนาด type ตัวเลข
