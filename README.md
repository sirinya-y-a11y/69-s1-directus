# 🏥 Clinic Management System with Directus

## ระบบจัดการคลินิกด้วย Directus

โครงงานระบบจัดการข้อมูลคลินิก (Clinic Management System) พัฒนาด้วย **Directus, PostgreSQL และ Docker** สำหรับจัดการข้อมูลผู้ป่วย แพทย์ การนัดหมาย และการรักษา พร้อมระบบ Authentication, Role-Based Access Control (RBAC), REST API และระบบทดสอบการส่งอีเมลสำหรับการรีเซ็ตรหัสผ่าน

โครงงานนี้เป็นส่วนหนึ่งของการศึกษา

**คณะวิศวกรรมศาสตร์ สาขาวิศวกรรมคอมพิวเตอร์**  
**มหาวิทยาลัยเทคโนโลยีราชมงคลพระนคร ศูนย์พระนครเหนือ**

---

## 📌 Project Overview

ระบบ Clinic Management System ถูกออกแบบมาเพื่อเป็น Backend สำหรับระบบจัดการคลินิก โดยใช้ Directus เป็น Backend Platform และ REST API เชื่อมต่อกับฐานข้อมูล PostgreSQL

ระบบรองรับการจัดการข้อมูลหลัก ได้แก่

- ข้อมูลผู้ป่วย (Patients)
- ข้อมูลแพทย์ (Doctors)
- ข้อมูลการนัดหมาย (Appointments)
- ข้อมูลการรักษา (Treatments)
- การเข้าสู่ระบบ (Authentication)
- การกำหนดสิทธิ์ตาม Role
- การรีเซ็ตรหัสผ่านผ่าน Email
- REST API
- API Testing

---

## 🎯 Objectives

วัตถุประสงค์ของโครงงาน

1. พัฒนาระบบ Backend สำหรับจัดการข้อมูลภายในคลินิก
2. ศึกษาการใช้งาน Directus ร่วมกับ PostgreSQL
3. ออกแบบ Data Model และความสัมพันธ์ของข้อมูล
4. ศึกษาการใช้งาน REST API
5. พัฒนาระบบ Authentication สำหรับผู้ใช้งาน
6. กำหนดสิทธิ์การเข้าถึงข้อมูลด้วย Role และ Policy
7. ศึกษาการใช้งาน Docker และ Docker Compose
8. ทดสอบระบบ Email สำหรับ Forgot Password และ Reset Password
9. ศึกษาการทำงานร่วมกันผ่าน Git และ GitHub
10. ฝึกการพัฒนาโครงการแบบแบ่ง Feature Branch และ Pull Request

---

## ✨ Features

ระบบมีความสามารถหลักดังนี้

- Patient Management
- Doctor Management
- Appointment Management
- Treatment Management
- User Authentication
- Doctor Login
- Receptionist Login
- Forgot Password
- Reset Password
- Role-Based Access Control (RBAC)
- Policy และ Permission Management
- REST API
- CRUD Operations
- API Testing
- Email Testing ผ่าน Mailpit
- PostgreSQL Database Management
- Directus Schema Snapshot
- Docker-based Development Environment

---

## 🛠️ Technology Stack

| Technology | Usage |
|---|---|
| Directus | Backend, REST API และ Admin Panel |
| PostgreSQL | ระบบฐานข้อมูล |
| Docker | Containerization |
| Docker Compose | จัดการ Services ของระบบ |
| pgAdmin | จัดการและตรวจสอบ PostgreSQL |
| Mailpit | ทดสอบการส่ง Email |
| REST Client | ทดสอบ REST API |
| Git | Version Control |
| GitHub | Repository และ Team Collaboration |
| Visual Studio Code | Development Environment |

---

# 🏗️ System Architecture

โครงสร้างโดยรวมของระบบ

```text
            Client / REST Client
                    |
                    | HTTP / REST API
                    v
          +--------------------+
          |      Directus      |
          |     Port 8055      |
          +--------------------+
             |              |
             |              |
             v              v
      +-------------+   +-------------+
      | PostgreSQL  |   |   Mailpit   |
      |  Database   |   | Email Test  |
      +-------------+   +-------------+
             |
             v
        +---------+
        | pgAdmin |
        +---------+
```

Directus ทำหน้าที่เป็น Backend หลักของระบบ โดยเชื่อมต่อกับ PostgreSQL สำหรับจัดเก็บข้อมูล และเชื่อมต่อกับ Mailpit สำหรับทดสอบระบบ Email

---

# 🐳 Docker Architecture

ระบบถูกแบ่งออกเป็นหลาย Container ผ่าน Docker Compose

| Service | Container | Description |
|---|---|---|
| Directus | `69-s1-directus-app` | Backend และ REST API |
| PostgreSQL | `69-s1-directus-db` | Database |
| pgAdmin | `69-s1-directus-admin` | Database Administration |
| Mailpit | `69-s1-directus-mailpit` | Email Testing |

การแยก Service ด้วย Docker ช่วยให้สมาชิกในทีมสามารถสร้าง Environment ที่ใกล้เคียงกันในแต่ละเครื่องได้

---

# 🗄️ Database Structure

ระบบประกอบด้วย 4 Collections หลัก

## 1. Patients

ใช้สำหรับจัดเก็บข้อมูลผู้ป่วย

| Field | Description |
|---|---|
| `id` | Primary Key |
| `patient_code` | รหัสผู้ป่วย |
| `first_name` | ชื่อ |
| `last_name` | นามสกุล |
| `gender` | เพศ |
| `phone` | เบอร์โทรศัพท์ |
| `date_of_birth` | วันเกิด |

`patient_code` ควรกำหนดเป็น Unique เพื่อป้องกันรหัสผู้ป่วยซ้ำ

---

## 2. Doctors

ใช้สำหรับจัดเก็บข้อมูลแพทย์

| Field | Description |
|---|---|
| `id` | Primary Key |
| `doctor_code` | รหัสแพทย์ |
| `first_name` | ชื่อ |
| `last_name` | นามสกุล |
| `specialty` | ความเชี่ยวชาญ |
| `phone` | เบอร์โทรศัพท์ |
| `email` | Email |

`doctor_code` ควรกำหนดเป็น Unique เพื่อป้องกันรหัสแพทย์ซ้ำ

---

## 3. Appointments

ใช้สำหรับจัดเก็บข้อมูลการนัดหมาย

| Field | Description |
|---|---|
| `id` | Primary Key |
| `patient_id` | ผู้ป่วย |
| `doctor_id` | แพทย์ |
| `appointment_date` | วันและเวลานัดหมาย |
| `symptom` | อาการ |
| `status` | สถานะการนัดหมาย |

---

## 4. Treatments

ใช้สำหรับจัดเก็บข้อมูลการรักษา

| Field | Description |
|---|---|
| `id` | Primary Key |
| `appointment_id` | Appointment ที่เกี่ยวข้อง |
| `diagnosis` | ผลการวินิจฉัย |
| `treatment_detail` | รายละเอียดการรักษา |
| `medicine` | ยาที่ใช้ |
| `treatment_date` | วันที่รักษา |

---

# 🔗 Database Relationships

ความสัมพันธ์หลักของข้อมูลเป็นดังนี้

```text
Patients
    |
    | patient_id
    v
Appointments --------> Treatments
    ^
    | doctor_id
    |
Doctors
```

หรือสรุปได้ว่า

```text
Patients ----\
              \
               >---- Appointments ----> Treatments
              /
Doctors -----/
```

- Patient สามารถมี Appointment ได้
- Doctor สามารถมี Appointment ได้
- Appointment เชื่อมโยง Patient และ Doctor
- Treatment เชื่อมโยงกับ Appointment

---

# 🔐 Authentication

ระบบใช้ Authentication ของ Directus

ผู้ใช้งานแต่ละ Role ใช้ Authentication Endpoint เดียวกัน แต่ Permission หลังจาก Login จะแตกต่างกันตาม Role และ Policy

## Login

```http
POST /auth/login
```

ตัวอย่าง Request

```json
{
  "email": "user@example.com",
  "password": "your_password"
}
```

เมื่อ Login สำเร็จ ระบบจะคืน Access Token สำหรับใช้ในการเรียก API ที่ต้องมีการ Authentication

---

## Current User

สามารถตรวจสอบผู้ใช้งานที่ Login อยู่ผ่าน

```http
GET /users/me
```

พร้อมส่ง Access Token

```http
Authorization: Bearer YOUR_ACCESS_TOKEN
```

Endpoint นี้สามารถใช้ตรวจสอบได้ว่า Token ปัจจุบันเป็นของผู้ใช้งานใด

---

# 👥 Roles and Access Control

ระบบแบ่งผู้ใช้งานออกเป็น Role หลักดังนี้

## Administrator

ใช้สำหรับบริหารจัดการระบบ Directus เช่น

- Database Collections
- Users
- Roles
- Policies
- Permissions
- System Configuration

Administrator มีสิทธิ์ระดับผู้ดูแลระบบ

---

## Doctor

Role สำหรับแพทย์ภายในคลินิก

ใช้สำหรับเข้าถึงข้อมูลที่เกี่ยวข้องกับการทำงานของแพทย์ เช่น

- Patients
- Doctors
- Appointments
- Treatments

สิทธิ์จริงขึ้นอยู่กับ Policy และ Permission ที่กำหนดใน Directus

---

## Receptionist

Role สำหรับเจ้าหน้าที่ Receptionist

ใช้สำหรับงานหน้าคลินิก เช่น

- จัดการข้อมูลผู้ป่วย
- จัดการข้อมูลการนัดหมาย
- ดูข้อมูลแพทย์
- ดูข้อมูลการรักษาตาม Permission ที่กำหนด

---

# 🛡️ Policy and Permissions

ระบบใช้ Directus Policies และ Permissions เพื่อกำหนดสิทธิ์ของแต่ละ Role

Policy หลักของระบบประกอบด้วย

```text
Doctor
    |
    v
Doctor Policy
    |
    v
Permissions

Receptionist
    |
    v
Receptionist Policy
    |
    v
Permissions
```

Permission สามารถควบคุมการทำงานแบบ CRUD ได้แก่

```text
Create
Read
Update
Delete
```

ทำให้สามารถกำหนดได้ว่า Role แต่ละประเภทสามารถดำเนินการใดกับ Collection ใดได้บ้าง

---

# 📧 Forgot Password & Reset Password

ระบบรองรับการขอเปลี่ยนรหัสผ่านผ่าน Directus Authentication API

## Forgot Password

```http
POST /auth/password/request
```

เมื่อ Request สำเร็จ ระบบจะส่ง Email สำหรับ Reset Password

ใน Development Environment Email จะถูกส่งไปยัง Mailpit เพื่อใช้ในการทดสอบ

---

## Reset Password

หลังจากเปิด Email ใน Mailpit จะได้รับ Reset Token

จากนั้นสามารถเรียก

```http
POST /auth/password/reset
```

ตัวอย่าง

```json
{
  "token": "RESET_TOKEN",
  "password": "NEW_PASSWORD"
}
```

Reset Token เป็นข้อมูลสำคัญและไม่ควร Commit หรือเผยแพร่ใน Repository

---

# 📡 REST API

Directus สร้าง REST API สำหรับ Collections ของระบบโดยอัตโนมัติ

ตัวอย่าง API

## Patients

```http
POST   /items/patients
GET    /items/patients
GET    /items/patients/:id
PATCH  /items/patients/:id
DELETE /items/patients/:id
```

## Doctors

```http
POST   /items/doctors
GET    /items/doctors
GET    /items/doctors/:id
PATCH  /items/doctors/:id
DELETE /items/doctors/:id
```

## Appointments

```http
POST   /items/appointments
GET    /items/appointments
GET    /items/appointments/:id
PATCH  /items/appointments/:id
DELETE /items/appointments/:id
```

## Treatments

```http
POST   /items/treatments
GET    /items/treatments
GET    /items/treatments/:id
PATCH  /items/treatments/:id
DELETE /items/treatments/:id
```

การเข้าถึง API แต่ละรายการขึ้นอยู่กับ Authentication และ Permission ของผู้ใช้งาน

---

# 🧪 API Testing

ไฟล์สำหรับทดสอบ API ของโปรเจกต์

```text
api.http.simple
```

API Testing แบ่งออกเป็นส่วนหลักดังนี้

```text
1. Doctor
   1.1 Login
   1.2 Forgot Password
   1.2.1 Reset Password
   1.3 Profile

2. Receptionist
   2.1 Login
   2.2 Forgot Password
   2.2.1 Reset Password
   2.3 Profile

3. Content
   3.1 Patient
       - Create
       - List All
       - List with ID
       - Update
       - Delete

   3.2 Doctor
       - Create
       - List All
       - List with ID
       - Update
       - Delete

   3.3 Appointment
       - Create
       - List All
       - List with ID
       - Update
       - Delete

   3.4 Treatment
       - Create
       - List All
       - List with ID
       - Update
       - Delete
```

ข้อมูลสำคัญ เช่น Password และ Access Token ไม่ควรเขียนลงในไฟล์ API ที่เผยแพร่สู่ Repository

---

# ⚙️ Environment Variables

โปรเจกต์ใช้ Environment Variables สำหรับจัดเก็บ Configuration

ไฟล์ตัวอย่าง

```text
.env.simple
```

สำหรับการใช้งานจริงในเครื่องให้สร้าง

```text
.env
```

แนวคิดการใช้งาน

```text
.env.simple
     |
     | copy / configure
     v
.env
     |
     v
Docker Compose / API Testing
```

`.env.simple` ควรมีเฉพาะค่าตัวอย่างหรือ Placeholder

ตัวอย่าง

```env
DIRECTUS_ADMIN_EMAIL=admin@example.com
DIRECTUS_ADMIN_PASSWORD=your_admin_password

DOCTOR_EMAIL=doctor@example.com
DOCTOR_PASSWORD=your_doctor_password

RECEPTIONIST_EMAIL=receptionist@example.com
RECEPTIONIST_PASSWORD=your_receptionist_password
```

> ห้ามใส่ Password, Token หรือ Secret จริงลงใน `.env.simple`

---

# 🔒 Sensitive Information

ข้อมูลต่อไปนี้ไม่ควร Commit ขึ้น GitHub

```text
.env
Database Password
Directus Secret
Admin Password
Doctor Password
Receptionist Password
Access Token
Refresh Token
Password Reset Token
```

ควรเก็บข้อมูลสำคัญไว้ใน Environment Variables ของแต่ละเครื่องเท่านั้น

---

# 🚀 Installation

## 1. Clone Repository

```bash
git clone https://github.com/sirinya-y-a11y/69-s1-directus.git
```

เข้าไปยัง Project Directory

```bash
cd 69-s1-directus
```

---

## 2. Configure Environment

ใช้ `.env.simple` เป็นตัวอย่างสำหรับสร้าง `.env`

Windows PowerShell สามารถใช้

```powershell
Copy-Item .env.simple .env
```

จากนั้นแก้ไขค่าภายใน `.env` ให้เหมาะสมกับเครื่องของตนเอง

---

## 3. Start Docker

รัน

```bash
docker compose up -d
```

---

## 4. Check Containers

```bash
docker compose ps
```

ตรวจสอบว่า Services ที่จำเป็นทำงานอยู่

```text
Directus
PostgreSQL
pgAdmin
Mailpit
```

---

## 5. Open Directus

เมื่อ Container ทำงานแล้ว สามารถเข้า Directus ได้ที่

```text
http://localhost:8055
```

---

# 📁 Project Structure

โครงสร้างไฟล์หลักของโปรเจกต์

```text
69-s1-directus/
│
├── .env.simple
├── .gitignore
├── README.md
├── access-control.sql
├── api.http.simple
├── docker-compose.yaml
└── snapshot.yaml
```

รายละเอียดไฟล์

### `.env.simple`

ตัวอย่าง Environment Variables สำหรับการตั้งค่าระบบ

### `docker-compose.yaml`

กำหนด Services และ Docker Containers ของระบบ

### `snapshot.yaml`

เก็บ Schema Snapshot ของ Directus สำหรับ Data Model ของระบบคลินิก

### `access-control.sql`

ใช้สำหรับการตั้งค่า Access Control ที่เกี่ยวข้องกับ Role, Policy และ Permission

### `api.http.simple`

ใช้สำหรับทดสอบ Authentication และ REST API ของระบบ

### `.gitignore`

กำหนดไฟล์ที่ไม่ต้องการให้ Git ติดตาม เช่น Environment Configuration ที่มีข้อมูลสำคัญ

---

# 🔄 Schema Management

Directus สามารถใช้ Snapshot สำหรับจัดการ Schema ระหว่างเครื่องของสมาชิกในทีม

โครงสร้างโดยรวม

```text
Machine A
   |
   | Create / Update Data Model
   v
snapshot.yaml
   |
   | GitHub
   v
Machine B
   |
   | Apply Snapshot
   v
Same Data Model
```

ช่วยให้สมาชิกแต่ละคนสามารถใช้ Data Model ที่สอดคล้องกันได้

---

# 🌿 Git Workflow

โปรเจกต์ใช้ Git และ GitHub สำหรับการพัฒนาร่วมกัน

แนวทางการทำงานคือ

```text
Feature Branch
      |
      | Commit
      v
GitHub Feature Branch
      |
      | Pull Request
      v
     main
```

ตัวอย่าง Feature Branch

```text
feature/data-model
feature/api-testing
```

ขั้นตอนพื้นฐาน

```bash
git switch <feature-branch>
git add <files>
git commit -m "Commit message"
git push origin <feature-branch>
```

จากนั้นสร้าง Pull Request บน GitHub

```text
Feature Branch
      |
      v
Pull Request
      |
      v
Review / Check Conflict
      |
      v
Merge
      |
      v
main
```

การใช้ Pull Request ช่วยลดความเสี่ยงในการแก้ไข `main` โดยตรงและทำให้สามารถตรวจสอบงานก่อน Merge ได้

---

# 🔐 Security Considerations

โครงการมีแนวทางด้านความปลอดภัยดังนี้

### Authentication

ผู้ใช้งานต้อง Login ก่อนเข้าถึง API ที่ต้องมีการยืนยันตัวตน

### Authorization

ใช้ Role, Policy และ Permission เพื่อควบคุมสิทธิ์ของผู้ใช้งาน

### Environment Variables

ข้อมูลสำคัญไม่ควรเขียนลงใน Source Code โดยตรง

### Password Protection

Password จริงไม่ควรถูก Commit ขึ้น Repository

### Token Protection

Access Token, Refresh Token และ Reset Token ถือเป็นข้อมูลสำคัญและไม่ควรเผยแพร่

### Database Integrity

Field ที่ไม่ควรมีข้อมูลซ้ำ เช่น `patient_code` และ `doctor_code` ควรกำหนด Unique Constraint

### Least Privilege

สำหรับการนำระบบไปใช้งานจริง ควรกำหนด Permission ของแต่ละ Role ให้เข้าถึงเฉพาะข้อมูลและ Action ที่จำเป็นต่อหน้าที่

---

# ⚠️ Problems and Solutions

ระหว่างการพัฒนาพบประเด็นสำคัญ เช่น

### Duplicate Data

การเรียก POST ซ้ำสามารถสร้าง Record ใหม่ได้ หาก Database ไม่มี Unique Constraint

**แนวทางแก้ไข:**  
กำหนด Unique Constraint ให้ Field ที่ต้องไม่ซ้ำ เช่น `patient_code` และ `doctor_code`

### Permission Denied

ผู้ใช้งานบาง Role อาจได้รับ HTTP `403 Forbidden` หาก Policy ไม่มี Permission สำหรับ Collection หรือ Action ที่เรียก

**แนวทางแก้ไข:**  
ตรวจสอบ Role, Policy และ CRUD Permissions ใน Directus

### Password Reset Email

ระบบ Forgot Password จำเป็นต้องมี Email Transport

**แนวทางแก้ไข:**  
ใช้ Mailpit สำหรับรับและตรวจสอบ Email ใน Development Environment

### Team Environment

สมาชิกแต่ละเครื่องอาจมี Schema หรือ Configuration ไม่ตรงกัน

**แนวทางแก้ไข:**  
ใช้ Docker Compose, Environment Configuration และ Directus Snapshot เพื่อช่วยให้ Environment สอดคล้องกัน

---

# 🔮 Future Improvements

ระบบสามารถพัฒนาต่อได้ในอนาคต เช่น

- เพิ่ม Item-Level Permissions
- จำกัดข้อมูลตาม Doctor ที่รับผิดชอบ
- เพิ่ม Field-Level Permissions
- เพิ่ม Validation Rules
- เพิ่ม Automated API Testing
- เพิ่ม Audit และ Activity Monitoring
- เพิ่มระบบ Frontend
- เพิ่ม Dashboard สำหรับแพทย์
- เพิ่ม Dashboard สำหรับ Receptionist
- เพิ่มระบบค้นหาประวัติผู้ป่วย
- เพิ่มระบบแจ้งเตือนการนัดหมาย
- เพิ่ม Production Email Service
- เพิ่ม HTTPS
- เพิ่ม Backup Strategy
- ปรับ Permission ตามหลัก Least Privilege

---

# 👨‍💻 Team Responsibilities

การพัฒนาโครงการแบ่งงานออกเป็นส่วนหลัก ได้แก่

| ส่วนงาน | รายละเอียด |
|---|---|
| Project Setup | การตั้งค่าโปรเจกต์และ Environment |
| Data Model | ออกแบบ Collections, Fields และ Relationships |
| Access Control | จัดการ Roles, Policies และ Permissions |
| API Testing | ทดสอบ Authentication และ CRUD API |
| Integration | รวมการทำงานของแต่ละส่วน |
| Docker | จัดการ Development Services |
| Mailpit | ทดสอบระบบ Email และ Password Reset |
| Git/GitHub | Version Control, Feature Branch และ Pull Request |

สมาชิกในทีมพัฒนาแต่ละส่วนผ่าน Git และรวมงานเข้าสู่ `main` ผ่าน Pull Request

---

# 👥 คณะผู้จัดทำ

โครงงาน **Clinic Management System with Directus** จัดทำโดย

| ลำดับ | ชื่อ-นามสกุล | รหัสนักศึกษา |
|:---:|---|:---:|
| 1 | นางสาวแพรทิพย์ หนะราช | 056860405015-9 |
| 2 | นางสาวสุพรรษา งามอักษร | 056860405031-6 |
| 3 | นางสาวสิรินยา ยืนชีวิต | 056860405063-9 |
| 4 | นายอินทัช เวนานนท์ | 056960405159-3 |

### ข้อมูลสถาบัน

**คณะ:** คณะวิศวกรรมศาสตร์  
**สาขา:** วิศวกรรมคอมพิวเตอร์  
**มหาวิทยาลัย:** มหาวิทยาลัยเทคโนโลยีราชมงคลพระนคร  
**ศูนย์:** พระนครเหนือ

---

# 📚 Project Summary

Clinic Management System เป็นโครงงานสำหรับศึกษาการพัฒนา Backend ด้วย Directus และ PostgreSQL โดยครอบคลุมตั้งแต่การออกแบบ Data Model การสร้าง REST API การ Authentication การกำหนด Role และ Permission การทดสอบ Password Reset ผ่าน Email ตลอดจนการจัดการ Development Environment ด้วย Docker

นอกจากนี้โครงงานยังประยุกต์ใช้ Git และ GitHub สำหรับการทำงานร่วมกันเป็นทีม โดยแยกการพัฒนาเป็น Feature Branch และใช้ Pull Request ก่อนรวมงานเข้าสู่ `main`

แนวทางดังกล่าวช่วยให้เข้าใจกระบวนการพัฒนาระบบ Backend ตั้งแต่ระดับ Database, API, Authentication, Authorization, Security ไปจนถึงการทำงานร่วมกันผ่าน Version Control

---

## 🎓 Faculty of Engineering

**Computer Engineering**  
**Rajamangala University of Technology Phra Nakhon**  
**North Bangkok Campus**