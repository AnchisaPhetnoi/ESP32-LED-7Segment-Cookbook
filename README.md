# ESP32-LED-7Segment-Cookbook

ตัวอย่างที่นำมาใช้ คือ การใช้งาน 7 segment โดยการเขียนคำสั่งแสดงผลเป็นตัวเลข นำมาจาก Project  Lab 6-1 ทดสอบ Hardware 7 segment


### ส่วนของการแก้ไข

ทำการแก้ไขใน main.cpp เพื่อให้แสดงผลลัพน์ตามค่าที่ตนเองต้องการโดยแตกต่างจากผลลัพน์ตอนทำ Lab


### ขั้นตอนการทำ project


## 1.สร้าง project และเขียนโปรแกรม

1.1 สร้าง project ใหม่ ชื่อ esp segment

![image](https://github.com/user-attachments/assets/8d85c099-d95d-4f96-9f9e-7dcafcc423be)


1.2 add idf_component.yml ใน Main component

1.3 เพิ่ม dependency ใน yml

![image](https://github.com/user-attachments/assets/145f51fd-8f64-4e92-ac35-c62357448768)

![image](https://github.com/user-attachments/assets/ebafe35a-fbd3-401a-ad74-27609b35c047)

``` cpp
dependencies:
  LED:
    git: https://github.com/AnchisaPhetnoi/ESP32-LED.git
    path: components/LED
```






















Build และทดสอบบนบอร์ด ESP32

ผลลัพน์คือ

วิดิโอประกอบ


สรุปผล: 


ลิงค์ Project ที่ทำบน VS code :


