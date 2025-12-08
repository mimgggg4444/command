
# ✅ **1. 프로젝트 초기화**

```bash
npm init -y
```

---

# ✅ **2. 필수 Dependencies 설치 (Express + Prisma Client + pg + cors + dotenv)**

👉 **서버 실행에 필요한 라이브러리들**

```bash
npm install express @prisma/client pg cors dotenv
```

설치되는 것:

* `express` → API 서버
* `@prisma/client` → Prisma ORM 클라이언트
* `pg` → PostgreSQL 드라이버
* `cors` → CORS 허용
* `dotenv` → .env 파일 읽기

---

# ✅ **3. DevDependencies 설치 (Prisma CLI)**

👉 마이그레이션, 스키마 관련 명령어 사용하려면 필요

```bash
npm install -D prisma
```

---

# ✅ **4. Prisma 초기화**

```bash
npx prisma init
```

생성되는 파일들:

```
prisma/
 └── schema.prisma
.env
```

---

# ✅ **5. .env 수정**

```env
DATABASE_URL="postgresql://USER:PASSWORD@localhost:5432/DBNAME"
```

DevPod or Render 사용 시 다른 URL 넣으면 됨.

---

# ✅ **6. Prisma 스키마 push (DB 테이블 생성)**

```bash
npx prisma db push
```

---

# ✅ **7. Prisma Client 생성 (자동 생성)**

보통 `db push`, `migrate` 시 자동 생성되지만 수동으로도 가능:

```bash
npx prisma generate
```

---

# 🎯 **최종 정리된 명령어 FULL Package**

```bash
npm init -y
npm install express @prisma/client pg cors dotenv
npm install -D prisma
npx prisma init
npx prisma db push
npx prisma generate
```

