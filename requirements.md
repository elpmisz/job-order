# System Requirements

สิ่งที่ต้องติดตั้งบนเครื่องก่อนเริ่มพัฒนาหรือรันระบบ Job Order

---

## 1. Runtime & Package Manager

| โปรแกรม | Version แนะนำ | ดาวน์โหลด |
|---------|--------------|-----------|
| **Node.js** | >= 20.x LTS | https://nodejs.org |
| **npm** | >= 10.x (มากับ Node.js) | — |

> ตรวจสอบด้วย: `node -v` และ `npm -v`

---

## 2. Database

| โปรแกรม | Version แนะนำ | หมายเหตุ |
|---------|--------------|----------|
| **PostgreSQL** | >= 15.x | ติดตั้งบนเครื่อง หรือใช้ Docker / Cloud (เช่น Supabase, Neon) |

### ตัวเลือกการติดตั้ง PostgreSQL

**Option A — ติดตั้งตรง (Local)**
- ดาวน์โหลด: https://www.postgresql.org/download/windows/
- ระหว่างติดตั้งให้จำ: `username`, `password`, `port` (default: `5432`)

**Option B — ใช้ Docker (แนะนำสำหรับ Dev)**
```bash
docker run --name job-order-db \
  -e POSTGRES_USER=admin \
  -e POSTGRES_PASSWORD=password \
  -e POSTGRES_DB=job_order \
  -p 5432:5432 \
  -d postgres:15
```

**Option C — Cloud (ไม่ต้องติดตั้งบนเครื่อง)**
- [Supabase](https://supabase.com) — Free tier
- [Neon](https://neon.tech) — Free tier, Serverless PostgreSQL

---

## 3. Code Editor (แนะนำ)

| โปรแกรม | Version | ดาวน์โหลด |
|---------|---------|-----------|
| **Antigravity** | Latest (v1.19.5+) | https://antigravity.google/download |

### ลิงก์ดาวน์โหลดตามระบบปฏิบัติการ

| OS | ลิงก์ |
|----|-------|
| **Windows x64** | https://edgedl.me.gvt1.com/edgedl/release2/j0qc3/antigravity/stable/1.19.5-5117559161880576/windows-x64/Antigravity.exe |
| **Windows ARM64** | https://edgedl.me.gvt1.com/edgedl/release2/j0qc3/antigravity/stable/1.19.5-5117559161880576/windows-arm64/Antigravity.exe |
| **macOS Apple Silicon** | https://edgedl.me.gvt1.com/edgedl/release2/j0qc3/antigravity/stable/1.19.5-5117559161880576/darwin-arm/Antigravity.dmg |
| **macOS Intel** | https://edgedl.me.gvt1.com/edgedl/release2/j0qc3/antigravity/stable/1.19.5-5117559161880576/darwin-x64/Antigravity.dmg |
| **Linux** | https://antigravity.google/download/linux |

### System Requirements

| OS | ข้อกำหนด |
|----|----------|
| **Windows** | Windows 10 (64-bit) ขึ้นไป |
| **macOS** | macOS 12 (Monterey) ขึ้นไป |
| **Linux** | glibc >= 2.28, glibcxx >= 3.4.25 (Ubuntu 20, Debian 10, Fedora 36, RHEL 8) |

---

## 4. Git (สำหรับ Version Control)

| โปรแกรม | ดาวน์โหลด |
|---------|-----------|
| **Git** | https://git-scm.com/download/win |

> ตรวจสอบด้วย: `git --version`

---

## 5. (Optional) Docker

ใช้สำหรับรัน PostgreSQL แบบ Container โดยไม่ต้องติดตั้ง Postgres ตรง

| โปรแกรม | ดาวน์โหลด |
|---------|-----------|
| **Docker Desktop** | https://www.docker.com/products/docker-desktop |

---

## 6. การตั้งค่าหลังติดตั้ง

1. Clone หรือวาง Project ลงในโฟลเดอร์ที่ต้องการ
2. สร้างไฟล์ `.env` ที่ Root ของ Project:
```env
DATABASE_URL=postgresql://admin:password@localhost:5432/job_order
NEXT_PUBLIC_APP_URL=http://localhost:3000
```
3. รันคำสั่งติดตั้ง Dependencies:
```bash
npm install
```
4. สร้าง Database Schema และ Seed ข้อมูลตัวอย่าง:
```bash
npm run db:setup
```
5. เริ่มรัน Development Server:
```bash
npm run dev
```
6. เปิดเบราว์เซอร์ไปที่ `http://localhost:3000`

---

## สรุป Checklist

- [ ] Node.js >= 20 ติดตั้งแล้ว
- [ ] npm >= 10 ติดตั้งแล้ว
- [ ] PostgreSQL พร้อมใช้งาน (Local / Docker / Cloud)
- [ ] VS Code ติดตั้งแล้ว (Optional แต่แนะนำ)
- [ ] Git ติดตั้งแล้ว
- [ ] ไฟล์ `.env` สร้างและกรอกค่าครบแล้ว
