# ESP32-LED-7Segment-Cookbook

ตัวอย่างที่นำมาใช้ คือ การใช้งาน 7 segment โดยการเขียนคำสั่งแสดงผลเป็นตัวเลข นำมาจาก Project  Lab 6-1 ทดสอบ Hardware 7 segment


### ส่วนของการแก้ไข

ทำการแก้ไขใน main.cpp เพื่อให้แสดงผลลัพน์ตามค่าที่ตนเองต้องการโดยแตกต่างจากผลลัพน์ตอนทำ Lab


### ขั้นตอนการทำ project


## 1.สร้าง project และเขียนโปรแกรม

1.1 สร้าง project ใหม่ ชื่อ esp segment

![image](https://github.com/user-attachments/assets/8d85c099-d95d-4f96-9f9e-7dcafcc423be)

![image](https://github.com/user-attachments/assets/9d0c907d-00cf-4af0-8b97-06b01f91cb0e)


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


1.4 เปลี่ยนชื่อ main.c เป็น main.cpp

![image](https://github.com/user-attachments/assets/12a46869-e0ef-4e63-9975-b31e56a6af4e)


1.5 ใน CMakeLists.txt เปลี่ยนชื่อ main.c เป็น main.cpp

![image](https://github.com/user-attachments/assets/44646eaf-22f7-4269-94e3-eb72791b0a9d)

``` cpp
idf_component_register(SRCS "LED.cpp"
                    INCLUDE_DIRS "include"
                    REQUIRES driver) 
```

1.7 ใน main.cpp เปลี่ยน code เป็นดังนี้

![image](https://github.com/user-attachments/assets/f2a04ce0-82d2-4b71-9cb3-9bfacfdf40ef)

![image](https://github.com/user-attachments/assets/73db2af1-9b5f-4bf7-9966-11cc7cd2345e)

![image](https://github.com/user-attachments/assets/3e4e75dc-52f3-4eb1-bdb2-daed855355ad)


``` cpp
#include <stdio.h>
#include "LED.h"
#include "freertos/FreeRTOS.h"
#include "freertos/task.h"

LED seg_a(16);
LED seg_b(17);
LED seg_c(5);
LED seg_d(18);
LED seg_e(19);
LED seg_f(21);
LED seg_g(22);
LED digit_1(0);  // สำหรับหลักสิบ
LED digit_2(4);  // สำหรับหลักหน่วย

void DisplayDigit(int digit, int number) {
    if (digit == 1) {
        digit_1.ON();
        digit_2.OFF();
    } else if (digit == 2) {
        digit_1.OFF();
        digit_2.ON();
    }

    seg_a.OFF();
    seg_b.OFF();
    seg_c.OFF();
    seg_d.OFF();
    seg_e.OFF();
    seg_f.OFF();
    seg_g.OFF();

    switch (number) {
        case 0: seg_a.ON(); seg_b.ON(); seg_c.ON(); seg_d.ON(); seg_e.ON(); seg_f.ON(); break;
        case 1: seg_b.ON(); seg_c.ON(); break;
        case 2: seg_a.ON(); seg_b.ON(); seg_d.ON(); seg_e.ON(); seg_g.ON(); break;
        case 3: seg_a.ON(); seg_b.ON(); seg_c.ON(); seg_d.ON(); seg_g.ON(); break;
        case 4: seg_b.ON(); seg_c.ON(); seg_f.ON(); seg_g.ON(); break;
        case 5: seg_a.ON(); seg_c.ON(); seg_d.ON(); seg_f.ON(); seg_g.ON(); break;
        case 6: seg_a.ON(); seg_c.ON(); seg_d.ON(); seg_e.ON(); seg_f.ON(); seg_g.ON(); break;
        case 7: seg_a.ON(); seg_b.ON(); seg_c.ON(); break;
        case 8: seg_a.ON(); seg_b.ON(); seg_c.ON(); seg_d.ON(); seg_e.ON(); seg_f.ON(); seg_g.ON(); break;
        case 9: seg_a.ON(); seg_b.ON(); seg_c.ON(); seg_d.ON(); seg_f.ON(); seg_g.ON(); break;
    }
}

void DisplayNumber(int tens, int units) {
    for (int i = 0; i < 200; i++) {  // ทำซ้ำเพื่อแสดงผลได้นานขึ้น
        DisplayDigit(1, tens);
        vTaskDelay(10 / portTICK_PERIOD_MS);  // เพิ่มดีเลย์เพื่อให้ตัวเลขติดนานขึ้น

        DisplayDigit(2, units);
        vTaskDelay(10 / portTICK_PERIOD_MS);

        digit_1.OFF();
        digit_2.OFF();
    }
}

void DisplaySequence() {
    int sequence[][2] = {{6, 5}, {2, 0}, {3, 0}, {2, 8}, {0, 9}};
    int numPairs = sizeof(sequence) / sizeof(sequence[0]);

    for (int i = 0; i < numPairs; i++) {
        DisplayNumber(sequence[i][0], sequence[i][1]);
        vTaskDelay(1000 / portTICK_PERIOD_MS);  // ดีเลย์ระหว่างคู่ตัวเลขแต่ละคู่
    }
}

extern "C" void app_main(void) {
    while (1) {
        DisplaySequence();
        vTaskDelay(2000 / portTICK_PERIOD_MS);  // รอระหว่างรอบการแสดงลำดับทั้งหมด
    }
}

```

Build และทดสอบบนบอร์ด ESP32


ผลลัพน์คือ

วิดิโอประกอบ


สรุปผล: 


ลิงค์ Project ที่ทำบน VS code :


