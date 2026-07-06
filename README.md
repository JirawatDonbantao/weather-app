# 🌤️ Weather App

เว็บแอปพยากรณ์อากาศแบบ Full-Stack ที่ผู้ใช้สามารถค้นหาสภาพอากาศปัจจุบันของเมืองใดก็ได้ทั่วโลก ผ่านหน้าเว็บที่เชื่อมต่อกับ Backend API แบบ Real-time

เป็นส่วนหนึ่งของการเรียนรู้ **DevOps และ Cloud Engineering** — โปรเจกต์นี้เน้นการเชื่อมต่อ Frontend และ Backend ที่ Deploy แยกกันคนละ Cloud Platform เข้าด้วยกัน

🔗 **Live Demo:** [weather-jsllbndd5-jirawatdonbantao1.vercel.app](https://weather-jsllbndd5-jirawatdonbantao1.vercel.app)

---

## 📖 เกี่ยวกับโปรเจกต์นี้

Weather App เป็นโปรเจกต์ Full-Stack ตัวแรกที่ฝึกการทำงานร่วมกันระหว่าง:

- **Frontend** ที่ Deploy บน Vercel
- **Backend API** ที่ Deploy บน Railway (คนละ Domain กัน)
- **External API** (WeatherAPI.com) สำหรับดึงข้อมูลอากาศจริง

จุดสำคัญของโปรเจกต์นี้คือการแก้ปัญหา **CORS** ที่เกิดขึ้นเมื่อ Frontend และ Backend อยู่คนละ Domain กัน ซึ่งเป็นปัญหาที่พบบ่อยมากในการทำงานจริง

---

## 🛠️ Tech Stack

| เทคโนโลยี | ใช้ทำอะไร |
|---|---|
| **HTML / CSS / JavaScript** | Frontend UI |
| **Fetch API** | เรียกข้อมูลจาก Backend แบบ Asynchronous |
| **Vercel** | Cloud Platform สำหรับ Deploy Frontend |
| **Node.js + Express** | Backend API (Repo แยก: [myfirstapi](https://github.com/JirawatDonbantao/myfirstapi)) |
| **Railway** | Cloud Platform สำหรับ Deploy Backend |
| **WeatherAPI.com** | แหล่งข้อมูลสภาพอากาศจริง |
| **CORS** | อนุญาตการเรียก API ข้าม Domain |

---

## ✨ Features

- 🔍 ค้นหาสภาพอากาศตามชื่อเมืองได้ทั่วโลก
- 🌡️ แสดงอุณหภูมิจริงและอุณหภูมิที่รู้สึกได้ (Feels Like)
- 💧 แสดงความชื้นในอากาศ
- 🌬️ แสดงความเร็วลม
- 🎨 ไอคอนสภาพอากาศแบบไดนามิกตามสถานการณ์จริง
- ⚡ รองรับการกด Enter เพื่อค้นหา
- 🎯 แสดง Error ที่ชัดเจนเมื่อพิมพ์ชื่อเมืองผิดหรือไม่พบข้อมูล
- 📱 ออกแบบ UI แบบ Responsive และทันสมัย (Glassmorphism style)

---

## 🏗️ Architecture

```
ผู้ใช้ (Browser)
      │
      ▼
Vercel — Frontend (HTML/CSS/JS)
weather-jsllbndd5-jirawatdonbantao1.vercel.app
      │
      │  fetch() ─── CORS enabled
      ▼
Railway — Backend API (Node.js/Express)
myfirstapi-production-40f1.up.railway.app/weather/:city
      │
      ▼
WeatherAPI.com — External Data Source
```

**จุดสำคัญ:** Frontend และ Backend Deploy แยกกันคนละ Platform และคนละ Domain โดยสิ้นเชิง จึงต้องเปิดใช้งาน CORS ฝั่ง Backend เพื่อให้ Browser อนุญาตการเรียกข้ามโดเมนได้

---

## 🚀 Getting Started (รันโปรเจกต์นี้เอง)

### สิ่งที่ต้องมีก่อน
- Backend API ต้องรันอยู่แล้ว (ดูที่ [myfirstapi](https://github.com/JirawatDonbantao/myfirstapi))
- เบราว์เซอร์ทั่วไป (ไม่ต้องติดตั้งอะไรเพิ่มสำหรับ Frontend)

### ขั้นตอน

```bash
# Clone โปรเจกต์
git clone https://github.com/JirawatDonbantao/weather-app.git
cd weather-app
```

เปิดไฟล์ `index.html` แล้วแก้ตัวแปร `API_URL` ให้ชี้ไปที่ Backend ของคุณ:

```javascript
const API_URL = 'https://your-backend-url.up.railway.app'
```

จากนั้นเปิดไฟล์ `index.html` ในเบราว์เซอร์ได้เลย (ดับเบิลคลิก หรือใช้ VS Code Live Server)

---

## 📚 สิ่งที่ได้เรียนรู้จากโปรเจกต์นี้

- ความแตกต่างระหว่างเว็บแบบ Static และ Dynamic
- การแยก Deploy Frontend และ Backend คนละ Cloud Platform (Vercel + Railway)
- ปัญหา CORS คืออะไร เกิดขึ้นเมื่อไหร่ และวิธีแก้ด้วย `cors` middleware
- การใช้ `fetch()` เพื่อเรียก API แบบ Asynchronous พร้อมจัดการ Loading และ Error State
- การออกแบบ UI ที่ตอบสนองต่อสถานะต่าง ๆ (Loading, Success, Error)
- การเชื่อมต่อ Frontend เข้ากับ Backend Service ที่มีอยู่แล้วจากโปรเจกต์ก่อนหน้า

---

## 🔗 โปรเจกต์ที่เกี่ยวข้อง

- **Backend API:** [myfirstapi](https://github.com/JirawatDonbantao/myfirstapi) — REST API ที่ให้บริการข้อมูลสภาพอากาศ พร้อม Route อื่น ๆ สำหรับทดสอบ

---

## 🗺️ โปรเจกต์นี้เป็นส่วนหนึ่งของ

คอร์สเรียน **Cloud Computing & DevOps** — เส้นทางสู่การเป็น Cloud/DevOps Engineer

---

*Built with 💻 by [JirawatDonbantao](https://github.com/JirawatDonbantao)*
