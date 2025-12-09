
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







---

## 📂 명령어 실행에 따른 파일/폴더 변동 설명

### 1. `npm init -y`

| 파일/폴더 | 설명 |
| :--- | :--- |
| **`package.json`** | Node.js 프로젝트의 **메인 설정 파일**입니다. 프로젝트의 이름, 버전, 스크립트 명령어, 그리고 다음 단계에서 설치할 의존성 목록(dependencies)이 정의됩니다. |

### 2. `npm install express @prisma/client pg cors dotenv`

| 파일/폴더 | 설명 |
| :--- | :--- |
| **`package.json`** | 파일 내의 **`"dependencies"`** 섹션에 위 5개 패키지 (`express`, `@prisma/client`, `pg`, `cors`, `dotenv`)와 그 버전 정보가 추가됩니다. |
| **`package-lock.json`** | 설치된 모든 패키지와 그 하위 의존성(sub-dependencies)들의 **정확한 버전 및 구조**가 기록됩니다. 재현 가능한 설치를 보장합니다. |
| **`node_modules/`** | 설치된 모든 패키지(수백 개의 파일)가 저장되는 폴더입니다. 이 폴더는 Git 관리 대상에서 제외됩니다. |

### 3. `npm install -D prisma`

| 파일/폴더 | 설명 |
| :--- | :--- |
| **`package.json`** | 파일 내의 **`"devDependencies"`** 섹션에 `prisma` 패키지와 버전 정보가 추가됩니다. (`-D` 플래그로 인해 개발용 의존성으로 분류됨) |
| **`package-lock.json`** | `prisma` 패키지 관련 정보가 업데이트됩니다. |
| **`node_modules/`** | `prisma` CLI 도구가 설치됩니다. |

### 4. `npx prisma init`

| 파일/폴더 | 설명 |
| :--- | :--- |
| **`prisma/`** (새 폴더) | Prisma 관련 설정 파일들을 모아두는 폴더가 생성됩니다. |
| **`prisma/schema.prisma`** | **Prisma의 핵심 파일**입니다. 데이터베이스 연결 정보(`datasource`), Prisma가 사용할 데이터베이스 클라이언트 설정, 그리고 **데이터베이스 테이블 구조(모델)**를 정의합니다. |
| **`.env`** (새 파일) | **환경 변수 파일**입니다. 기본적으로 `DATABASE_URL` 변수가 정의되어 있으며, 데이터베이스 연결 문자열(5단계에서 수정할 내용)을 저장하는 데 사용됩니다. 보안상 Git 관리 대상에서 제외됩니다. |

### 5. `npx prisma db push`

이 명령어는 **DB에 실제로 테이블을 생성**합니다. 만약 `schema.prisma`에 데이터 모델이 정의되어 있다면, 해당 모델에 따라 DB 서버에 테이블이 생성/변경됩니다.

| 파일/폴더 | 설명 |
| :--- | :--- |
| **`prisma/schema.prisma`** | 만약 `db push` 실행 시 `schema.prisma` 파일이 변경되었다면, 자동 생성된 메타데이터가 업데이트될 수 있습니다. |
| **`@prisma/client`** | 다음 단계인 `npx prisma generate`를 포함하여 **Prisma Client가 자동 생성/업데이트**됩니다. (6단계와 7단계는 대부분 동시에 작동함) |

### 6. `npx prisma generate`

이 명령은 `@prisma/client`를 생성하고 TypeScript/JavaScript 코드에서 사용할 수 있도록 준비합니다.

| 파일/폴더 | 설명 |
| :--- | :--- |
| **`node_modules/@prisma/client/`** | Prisma가 `schema.prisma` 파일을 읽어들여, 정의된 데이터 모델에 접근하고 쿼리를 보낼 수 있도록 **Node.js 코드를 자동으로 생성**합니다. `import prisma from '../prismaClient.js';` 처럼 코드에서 임포트하여 사용하는 객체가 바로 이 단계에서 생성됩니다. |

---

### 📋 요약: 초기화 후 최종 생성되는 주요 파일

프로젝트 초기화가 완료되면, 코드를 작성하기 위해 준비된 환경은 다음과 같은 핵심 파일 구조를 갖게 됩니다.

| 파일/폴더 | 역할 |
| :--- | :--- |
| `package.json` | 프로젝트 정보 및 의존성 목록 |
| `node_modules/` | 설치된 모든 라이브러리 파일 |
| `.env` | 데이터베이스 연결 비밀 정보 저장 |
| `prisma/schema.prisma` | DB 모델(테이블) 정의 및 Prisma 설정 |




