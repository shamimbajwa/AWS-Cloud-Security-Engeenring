# 🔐 Class 3 — Migration, Shared Responsibility & IAM Basics

## ☁️ 1. Cloud Migration

**Cloud Migration** ka matlab hai kisi application, website, database ya IT system ko **on-premises environment se Cloud** par move karna.

Misal ke taur par agar kisi company ka application apne physical server par chal raha ho aur company usay AWS par move karti hai, to is process ko **Cloud Migration** kehte hain.

---

# 🔄 2. The 6 R's of Cloud Migration

Cloud Migration ke common **6 R's** yeh hain:

### 1. Rehost

Isay **Lift and Shift** bhi kaha jata hai.

Is mein application ko zyada changes kiye baghair existing environment se Cloud par move kar diya jata hai.

**Example:**  
`Existing Server → AWS EC2`

---

### 2. Replatform

Is mein application ko Cloud par move karte waqt kuch **minor changes ya optimization** ki jati hai, lekin application ka basic architecture same rehta hai.

**Example:**  
Application ko AWS par move karke managed database service use karna.

---

### 3. Repurchase

Is mein existing software ko migrate karne ke bajaye usay **new Cloud-based solution** se replace kiya jata hai.

**Example:**  
`Existing Software → SaaS Solution`

---

### 4. Refactor / Re-architect

Is mein application ko **dobara design ya modify** kiya jata hai taa-ke woh Cloud ki capabilities ka behtar faida utha sake.

**Example:**  
Traditional application ko microservices ya serverless architecture mein convert karna.

---

### 5. Retire

Jo applications ya services ab **useful nahi hain**, unko completely band ya remove kar dena.

**Example:**  
Old application jo company ab use nahi karti → **Retire**

---

### 6. Retain

Is mein application ko abhi Cloud par move nahi kiya jata aur usay **existing environment mein hi rakha jata hai**.

**Example:**  
Aisi legacy application jise abhi migrate karna practical nahi.

---

# 🔐 3. Shared Responsibility Model

**Shared Responsibility Model** ka matlab hai ke AWS Cloud ki security ki responsibility **AWS aur Customer ke darmiyan share hoti hai**.

Is model ko do main parts mein samjha jata hai:

## Security OF the Cloud

Iski responsibility **AWS** ki hoti hai.

AWS apni Cloud infrastructure ko secure karta hai, jismein:

- Physical Data Centers
- Hardware
- Networking Infrastructure
- Physical Security
- AWS Infrastructure

shamil hain.

---

## Security IN the Cloud

Iski responsibility **Customer** ki hoti hai.

Customer ko apne:

- Data
- Users
- Passwords
- IAM Permissions
- Applications
- Security Configurations

ko secure karna hota hai.

### Simple Example

AWS **building aur uski physical security** ko protect karta hai, jabke customer building ke andar apne **data aur resources** ko secure karta hai.

---

# ⚙️ 4. Responsibility Shifts by Service

AWS ki different services mein AWS aur customer ki responsibilities different hoti hain.

Jitni service zyada **managed** hoti jati hai, customer ki infrastructure management ki responsibility utni kam hoti jati hai.

| Service | AWS Responsibility | Customer Responsibility |
|---|---|---|
| **EC2** | Physical infrastructure | OS, Applications, Data & Security Configuration |
| **RDS** | Infrastructure & Database Platform | Data, Users, Access & Configuration |
| **Lambda** | Infrastructure & Runtime | Code, Data & Permissions |

### EC2

EC2 mein customer ko zyada cheezen manage karni hoti hain, jaise:

- Operating System
- Applications
- Data
- Security Configuration

### RDS

RDS mein AWS database infrastructure aur platform ko manage karta hai, is liye customer ki responsibility EC2 ke comparison mein kam hoti hai.

### Lambda

Lambda mein AWS underlying servers aur infrastructure ko manage karta hai. Customer mainly **code, data aur permissions** par focus karta hai.

### Key Concept

`EC2 → More Customer Responsibility`

`RDS → Less Customer Responsibility`

`Lambda → More Managed by AWS`

---

# 🔑 5. IAM — Identity and Access Management

**IAM** ka full form **Identity and Access Management** hai.

IAM AWS mein identities aur permissions ko manage karne ke liye use hota hai.

Iska basic purpose yeh decide karna hai:

> **Kaun AWS resources ko access kar sakta hai aur woh kya actions perform kar sakta hai?**

### Example

Aik employee ko S3 files **read** karne ki permission di ja sakti hai, lekin un files ko **delete** karne ki permission nahi di jati.

---

# 🔐 6. Authentication vs Authorization

## Authentication

**Authentication** ka matlab hai identity verify karna.

Simple words mein:

> **"Aap kaun hain?"**

### Example

Username aur password se AWS account mein login karna.

---

## Authorization

**Authorization** ka matlab hai user ko allowed actions ki permission dena.

Simple words mein:

> **"Aap kya kar sakte hain?"**

### Example

User S3 files ko **read** kar sakta hai, lekin **delete** nahi kar sakta.

### Easy Difference

| Concept | Meaning |
|---|---|
| **Authentication** | Who are you? |
| **Authorization** | What are you allowed to do? |

---

# 👤 7. IAM Building Blocks — User & Group

## IAM User

**IAM User** AWS account ke andar aik individual identity hoti hai.

Ye kisi person ya specific requirement ko represent kar sakti hai.

### Example

- Developer
- Security Engineer
- Administrator

Har IAM User ko uski requirement ke according permissions di ja sakti hain.

---

## IAM Group

**IAM Group** multiple IAM Users ka collection hota hai.

Iska faida yeh hai ke permissions ko har user ke liye separately manage karne ke bajaye **group level par manage** kiya ja sakta hai.

### Example

**Developers Group**

Is group mein:

- Ali
- Ahmed
- Sara

Agar Developers Group ko specific permissions di jati hain, to group ke users ko woh permissions mil sakti hain.

### Simple Concept

`User = Individual Identity`

`Group = Multiple Users ka Collection`

---

# 📝 Quick Revision

| Topic | Simple Meaning |
|---|---|
| **Cloud Migration** | System ko Cloud par move karna |
| **Rehost** | Directly Cloud par move karna |
| **Replatform** | Minor changes ke saath move karna |
| **Repurchase** | Existing solution ko replace karna |
| **Refactor / Re-architect** | Application ko dobara design karna |
| **Retire** | Unused system ko remove karna |
| **Retain** | System ko existing environment mein rakhna |
| **Shared Responsibility** | AWS aur Customer dono security ke responsible hain |
| **Security OF the Cloud** | AWS ki responsibility |
| **Security IN the Cloud** | Customer ki responsibility |
| **Authentication** | Aap kaun hain? |
| **Authorization** | Aap kya kar sakte hain? |
| **IAM User** | Individual identity |
| **IAM Group** | Multiple users ka collection |
| **EC2** | Customer ki zyada responsibility |
| **RDS** | AWS zyada management karta hai |
| **Lambda** | AWS underlying infrastructure manage karta hai |
