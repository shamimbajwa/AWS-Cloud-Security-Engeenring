# AWS Cloud Security — Class Notes

## 1. Deployment Models

Deployment Models ka matlab hai ke organization apne data, applications aur infrastructure ko kis tarah deploy aur manage karti hai.

Cloud mein commonly 3 deployment models use kiye jate hain:

1. Cloud
2. On-Premises
3. Hybrid Cloud

---

### 1.1 Cloud

Cloud mein organization apne servers aur infrastructure khud purchase karne ke bajaye cloud provider ki services use karti hai.

AWS, Microsoft Azure aur Google Cloud iski examples hain.

**Example:**

Agar koi company apni website AWS par host karti hai, to website ka server company ke office mein nahi hota. Server AWS ke data center mein hota hai aur company internet ke through usay use karti hai.

**Simple Definition:**

Cloud ka matlab hai ke infrastructure aur services cloud provider se use karna.

---

### 1.2 On-Premises

On-Premises ka matlab hai ke organization apne servers, networking devices aur doosra infrastructure apni physical location par rakhti hai.

Is infrastructure ko manage aur maintain karne ki responsibility bhi organization ki hoti hai.

**Example:**

Ek bank apne important customer data aur systems ke liye apne data center mein khud ke servers rakhta hai.

**Simple Definition:**

On-Premises ka matlab hai ke organization apna infrastructure khud own aur manage karti hai.

---

### 1.3 Hybrid Cloud

Hybrid Cloud mein Cloud aur On-Premises dono ko combine karke use kiya jata hai.

Organization apna kuch data aur applications apne servers par rakhti hai aur kuch resources cloud par use karti hai.

**Example:**

Ek hospital sensitive patient data apne servers par rakhta hai, jabke apni website AWS par host karta hai.

**Simple Definition:**

Hybrid Cloud ka matlab hai Cloud aur On-Premises dono ka combination.

---

## 2. Design Principles

Design Principles wo important principles hain jo cloud system ko reliable, available aur scalable banane mein help karte hain.

### 2.1 Scalability

Scalability ka matlab hai ke jab system par workload ya users ki tadaad barh jaye to system apni capacity increase kar sake.

Scalability ki 2 common types hain:

**Horizontal Scaling**

Is mein workload handle karne ke liye additional servers ya instances add kiye jate hain.

**Example:**

Agar website par users zyada ho jayein to ek server ke bajaye multiple servers use kiye ja sakte hain.

**Vertical Scaling**

Is mein existing server ke resources increase kiye jate hain, jaise CPU ya RAM.

**Example:**

Server ki RAM 4 GB se increase karke 16 GB kar dena.

---

### 2.2 Availability

Availability ka matlab hai ke system ya service users ke liye available aur accessible rahe.

System mein downtime jitna kam ho, availability utni behtar hoti hai.

**Example:**

Agar ek server fail ho jaye aur doosra server service provide karta rahe, to system available rehta hai.

**Simple Definition:**

Availability ka matlab hai system ka available aur accessible rehna.

---

### 2.3 Elasticity

Elasticity ka matlab hai ke system demand ke according automatically resources ko increase ya decrease kar sake.

**Example:**

Agar website par achanak bohat zyada users aa jayein to system automatically additional resources add kar sakta hai.

Jab users kam ho jayein to extra resources remove kiye ja sakte hain.

**Simple Definition:**

Elasticity ka matlab hai demand ke according resources ko automatically adjust karna.

---

### 2.4 High Availability

High Availability ka matlab hai system ko is tarah design karna ke failure ki situation mein bhi service available rahe aur downtime minimum ho.

Is ke liye multiple servers aur redundant resources use kiye ja sakte hain.

**Example:**

Agar ek server fail ho jaye to doosra server users ko service provide karta rahe.

**Simple Definition:**

High Availability ka matlab hai minimum downtime ke sath service ko available rakhna.

---

### 2.5 Single Point of Failure

Single Point of Failure yani SPOF system ka aisa single component hota hai jis ke fail hone se poora system ya important service affect ho sakti hai.

**Example:**

Agar website sirf ek server par depend karti hai aur woh server fail ho jaye, to website unavailable ho jayegi.

Is situation mein woh server Single Point of Failure hai.

**Simple Definition:**

Single Point of Failure ka matlab hai ek aisa single component jis ke fail hone se system affect ho sakta hai.

---

### 2.6 Fault Tolerance

Fault Tolerance ka matlab hai ke system kisi component ke fail hone ke bawajood kaam karta rahe.

**Example:**

Agar ek server fail ho jaye to doosra server automatically service continue kar de.

**Simple Definition:**

Fault Tolerance ka matlab hai failure ke bawajood system ka kaam karte rehna.

---

### 2.7 Disaster Recovery

Disaster Recovery ka matlab hai kisi major failure ya disaster ke baad systems aur data ko restore karna.

Disaster ki examples:

- Hardware failure
- Cyberattack
- Data loss
- Natural disaster
- Major system failure

**Example:**

Agar company ka main server fail ho jaye to backup se data aur systems ko restore kiya ja sakta hai.

**Simple Definition:**

Disaster Recovery ka matlab hai disaster ke baad systems aur data ko recover karna.

---

# 3. AWS Well-Architected Framework — Six Pillars

AWS Well-Architected Framework mein 6 important pillars hain jo AWS workloads ko secure, reliable, efficient aur cost-effective banane mein help karte hain.

The Six Pillars are:

1. Operational Excellence
2. Security
3. Reliability
4. Performance Efficiency
5. Cost Optimization
6. Sustainability

---

### 3.1 Operational Excellence

Operational Excellence ka matlab hai systems ko effectively operate karna aur continuously improve karna.

Is mein monitoring, automation aur processes ko improve karna shamil hai.

**Example:**

System ko monitor karna aur problems ko identify karke operations ko improve karna.

**Simple Definition:**

Operational Excellence ka matlab hai systems ko efficiently operate aur continuously improve karna.

---

### 3.2 Security

Security ka matlab hai data, applications, systems aur resources ko unauthorized access aur security threats se protect karna.

Is mein access control, data protection, network security aur monitoring important hain.

**Example:**

AWS IAM ka use karke decide karna ke kis user ko kis AWS resource ka access milna chahiye.

**Simple Definition:**

Security ka matlab hai systems aur data ko protect karna.

---

### 3.3 Reliability

Reliability ka matlab hai ke system apna required kaam correctly perform kare aur failure ke baad recover bhi kar sake.

**Example:**

Agar ek Availability Zone unavailable ho jaye to application doosri Availability Zone mein continue kar sake.

**Simple Definition:**

Reliability ka matlab hai system ka correctly work karna aur failure ke baad recover karna.

---

### 3.4 Performance Efficiency

Performance Efficiency ka matlab hai available resources ko efficiently use karna aur workload ke liye suitable resources select karna.

**Example:**

Application ki requirements ke according suitable EC2 instance select karna.

**Simple Definition:**

Performance Efficiency ka matlab hai right resources ko efficiently use karna.

---

### 3.5 Cost Optimization

Cost Optimization ka matlab hai cloud resources ko efficiently use karna aur unnecessary costs ko avoid karna.

**Example:**

Unused EC2 instances ko running rakhne ke bajaye unhein stop kar dena.

**Simple Definition:**

Cost Optimization ka matlab hai unnecessary cloud cost ko reduce karna.

---

### 3.6 Sustainability

Sustainability ka matlab hai cloud resources ko efficiently use karna taake energy consumption aur environmental impact ko reduce kiya ja sake.

**Example:**

Sirf required resources use karna aur unnecessary servers ko run na karna.

**Simple Definition:**

Sustainability ka matlab hai resources ko efficiently use karke environmental impact ko kam karna.

---

# Quick Revision

## Deployment Models

**Cloud** → Cloud provider ki infrastructure use karna.

**On-Premises** → Apni infrastructure ko khud manage karna.

**Hybrid Cloud** → Cloud aur On-Premises dono ko use karna.

---

## Design Principles

**Scalability** → Workload barhne par capacity increase karna.

**Availability** → System ko available rakhna.

**Elasticity** → Demand ke according resources automatically adjust karna.

**High Availability** → Minimum downtime ke sath service available rakhna.

**Single Point of Failure** → Aisa single component jis ke fail hone se system affect ho.

**Fault Tolerance** → Component fail hone ke bawajood system ka kaam karna.

**Disaster Recovery** → Disaster ke baad systems aur data ko restore karna.

---

## AWS Well-Architected Six Pillars

**Operational Excellence** → Efficient operations aur continuous improvement.

**Security** → Data aur systems ko protect karna.

**Reliability** → System ka correctly work aur recover karna.

**Performance Efficiency** → Resources ko efficiently use karna.

**Cost Optimization** → Unnecessary costs ko reduce karna.

**Sustainability** → Resources efficiently use karke environmental impact ko reduce karna.
