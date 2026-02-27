# Job Order System 📊

ระบบจัดการแผนการผลิต (Plans) และติดตามคำสั่งผลิต (Job Orders) แบบ Real-time สำหรับโรงงานและทีมบริหาร

> **Platform:** Web Application (Next.js + React)  
> **Database:** PostgreSQL  
> **UI Framework:** Tailwind CSS + Shadcn UI  
> **Charts:** Recharts

---

## 🚀 Quick Start

### 1. ติดตั้ง Dependencies

```bash
npm install
```

### 2. ตั้งค่า Environment Variables

สร้างไฟล์ `.env` ที่ Root ของโปรเจกต์:

```env
DATABASE_URL=postgresql://admin:password@localhost:5432/job_order
NEXT_PUBLIC_APP_URL=http://localhost:3000
```

### 3. สร้าง Database Schema & Seed ข้อมูลตัวอย่าง

```bash
npm run db:setup
```

### 4. รัน Development Server

```bash
npm run dev
```

เปิดเบราว์เซอร์ไปที่ **http://localhost:3000** ✨

---

## 📋 Prerequisites (ต้องติดตั้งก่อน)

ดูรายละเอียดทั้งหมดใน [requirements.md](requirements.md)

| โปรแกรม | Version | Status |
|---------|---------|--------|
| Node.js | >= 20 LTS | ✓ Required |
| npm | >= 10 | ✓ Required |
| PostgreSQL | >= 15 | ✓ Required |
| Git | Latest | ✓ Required |
| Antigravity | >= 1.19.5 | ⭐ Recommended |

---

## 📂 Project Structure

```
job-order/
├── app/                          # Next.js App Router
│   ├── page.tsx                  # Root redirect → /dashboard
│   ├── api/
│   │   ├── plan/route.ts         # API จัดการ Plan
│   │   ├── job-order/route.ts    # API จัดการ Job Order
│   │   └── seed/route.ts         # API สร้างข้อมูลตัวอย่าง
│   ├── dashboard/
│   │   └── page.tsx              # แดชบอร์ดสรุปภาพรวม
│   ├── plan/
│   │   └── page.tsx              # หน้าจัดการ Plan
│   └── job-order/
│       └── page.tsx              # หน้าจัดการ Job Order
├── components/
│   ├── layout/
│   │   └── sidebar.tsx           # เมนู Sidebar
│   ├── dashboard/
│   │   ├── summary-cards.tsx     # Card สรุปข้อมูล (4 ใบ)
│   │   ├── charts.tsx            # กราฟ Recharts (4 แบบ)
│   │   └── data-table.tsx        # ตาราง Job Order
│   └── forms/
│       ├── plan-form.tsx         # ฟอร์มสร้าง Plan
│       └── job-order-form.tsx    # ฟอร์มสร้าง Job Order
├── lib/
│   └── validations.ts            # Schema validation (Zod)
├── db/
│   ├── index.ts                  # Database client (Drizzle)
│   ├── schema.ts                 # Table schemas
│   └── seed.ts                   # Mock data seeding
├── drizzle.config.ts             # Drizzle Kit config
├── job-order-system.md           # System Planning Document
├── requirements.md               # Development Requirements
└── package.json
```

---

## 🛠 Tech Stack

| Layer | Technology |
|-------|------------|
| **Frontend** | Next.js 15+, React 19, TypeScript |
| **Styling** | Tailwind CSS, Shadcn UI |
| **Database** | PostgreSQL 15+ |
| **ORM** | Drizzle ORM |
| **Validation** | Zod + React Hook Form |
| **Charts** | Recharts |
| **UI Kit** | Lucide Icons, Radix UI |

---

## 📊 Features

### Dashboard
- 📈 **4 Summary Cards:** ยอดผลิตรวม, เป้าหมาย, จำนวน Job Order, พลังงานรวม
- 📉 **4 Chart Types:**
  - Doughnut Chart: Overall Production Progress
  - Column Chart: Production by Plan
  - Stacked Bar Chart: Job Order Status
  - Line Chart: Energy Consumption Trend
- 📋 **Data Table:** ค้นหา (Search) และกรอง (Filter) ตาม Plan

### Plan Management
- ✏️ สร้างแผนการผลิต (Plan) ใหม่
- 👁️ ดูรายการ Plan ทั้งหมด
- 🔄 อัปเดตสถานะแผน
- 📊 ติดตามความคืบหน้า

### Job Order Management
- ✏️ สร้าง Job Order ใหม่ (ผูกกับ Plan)
- 📝 บันทึกเป้าหมายกับผลิตจริง
- ⚡ บันทึกค่าการใช้พลังงาน (Energy kWh)
- 📏 บันทึกข้อมูลการตรวจสอบ (Inspection: Width, Length, Height, Thickness)
- ✅ Validation ข้อมูลก่อนบันทึก

---

## 🔧 Available Scripts

```bash
# Development
npm run dev              # เริ่มรัน dev server

# Database
npm run db:push         # Push schema ไปยัง DB
npm run db:seed         # Seed ข้อมูลตัวอย่าง
npm run db:setup        # Push + Seed ครั้งเดียว

# Code Quality
npm run lint            # ตรวจสอบ Code (ESLint)
npm run type-check      # Type checking (TypeScript)

# Build & Deploy
npm run build           # Build สำหรับ Production
npm run start           # รัน Production build
```

---

## 🗄️ Database Schema

### Table: `plans`
```sql
- id (UUID, primary key)
- code (VARCHAR, unique) — e.g., "A001"
- name (VARCHAR) — ชื่อแผน
- targetQty (INTEGER) — เป้าหมายรวม
- status (VARCHAR) — PENDING, IN_PROGRESS, COMPLETED
- createdAt (TIMESTAMP)
- updatedAt (TIMESTAMP)
```

### Table: `job_orders`
```sql
- id (UUID, primary key)
- planId (UUID, foreign key → plans.id)
- targetQty (INTEGER) — เป้าหมายผลิต
- actualQty (INTEGER) — ผลิตจริง
- energyKwh (DOUBLE) — พลังงานที่ใช้
- width (DOUBLE) — การตรวจสอบ: กว้าง
- length (DOUBLE) — การตรวจสอบ: ยาว
- thickness (DOUBLE) — การตรวจสอบ: หนา
- height (DOUBLE) — การตรวจสอบ: ความสูง
- status (VARCHAR) — PENDING, IN_PROGRESS, COMPLETED
- createdAt (TIMESTAMP)
- updatedAt (TIMESTAMP)
```

---

## 🎨 UI/UX Design

ระบบออกแบบมาเพื่อผู้บริหารและหัวหน้างาน:

- 🎯 **Professional & Minimalist:** โทนสีขาว-เทา ตัดด้วยสีน้ำเงิน/Slate
- 📱 **Responsive:** ทำงานได้ดีบน Mobile, Tablet, Desktop
- 🔤 **Typography:** ใช้ฟอนต์ K2D (Google Fonts) ทั่วทั้งระบบ
- 🌟 **Premium Look:** Card ขอบมนเล็กน้อย Shadow นุ่มนวล

---

## 📖 Documentation

- **[job-order-system.md](job-order-system.md)** — System Planning Document (Feature, Task Breakdown)
- **[requirements.md](requirements.md)** — Development Environment Requirements

---

## 🚀 Deployment

### Build for Production
```bash
npm run build
npm run start
```

### Deploy to Vercel (แนะนำ)
1. Push โค้ดขึ้น GitHub
2. เชื่อมต่อ Repository กับ [Vercel](https://vercel.com)
3. ตั้งค่า Environment Variables ใน Vercel Dashboard
4. Deploy อัตโนมัติเมื่อ Push ไป `main` branch

---

## 📝 Git Workflow

```bash
# Clone repository
git clone https://github.com/elpmisz/job-order.git
cd job-order

# Create feature branch
git checkout -b feature/your-feature-name

# Commit & Push
git add .
git commit -m "feat: describe your changes"
git push origin feature/your-feature-name

# Create Pull Request บน GitHub
```

---

## 🐛 Troubleshooting

### Database Connection Error
```bash
# ตรวจสอบ DATABASE_URL ใน .env
# ตรวจสอบ PostgreSQL running
psql -U admin -d job_order -c "SELECT 1"
```

### Port 3000 ถูกใช้งาน
```bash
# รัน dev server บน port อื่น
npm run dev -- -p 3001
```

### node_modules Corrupted
```bash
# ลบและติดตั้งใหม่
rm -rf node_modules package-lock.json
npm install
```

---

## 📞 Support

**ติดต่อ / Report Issues:** เปิด Issue บน GitHub Repository

---

## 📄 License

[MIT License](LICENSE) — Free to use

---

**Happy coding! 🎉**
