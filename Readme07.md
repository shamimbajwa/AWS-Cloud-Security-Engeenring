

# AWS Cloud Security: IAM Users & IAM Policies

## 1. Introduction to AWS IAM

AWS IAM ka full form **Identity and Access Management** hai.

AWS IAM ek security service hai jo humein AWS resources tak access ko securely control aur manage karne ki facility deti hai.

IAM ki madad se hum decide karte hain:

- AWS account ko kaun access kar sakta hai.
- User kin AWS services ko use kar sakta hai.
- User kya actions perform kar sakta hai.
- Kin resources par permissions apply hongi.
- Kis user ko access allow ya deny karna hai.

### Real-World Example

Ek software company AWS par website host karti hai. Company chahti hai ke developer EC2 instances dekh aur manage kar sake, jabke finance employee sirf billing information access kare. IAM in users ke access ko unki responsibilities ke mutabiq control karta hai.

---

# Part 1: IAM Users

## 2. What Is an IAM User?

IAM User AWS account ke andar ek identity hoti hai jise kisi person ya application ke liye create kiya ja sakta hai.

Har IAM user ki apni identity aur assigned permissions hoti hain. Console access ke liye username aur password use ho sakte hain, jabke programmatic access ke liye access keys ya doosre supported authentication methods use kiye ja sakte hain.

### Example

Ek company mein 3 employees hain:

- Developer
- Security Analyst
- Finance Employee

Administrator in employees ke liye alag IAM users create kar sakta hai aur har user ko uski job ke mutabiq permissions de sakta hai.

## 3. Root User vs IAM User

### Root User

Root user woh identity hai jo AWS account create karte waqt account owner ke email address se establish hoti hai.

Root user ke paas account-level administrative capabilities hoti hain aur kuch sensitive account tasks sirf root user perform kar sakta hai.

### IAM User

IAM user root user se separate identity hoti hai. Is ki permissions policies ke through manage ki ja sakti hain.

### Important Differences

| Root User | IAM User |
|---|---|
| AWS account ki original identity | Account ke andar create ki gayi identity |
| Highly privileged account access | Assigned permissions ke mutabiq access |
| Kuch account-level tasks ke liye zaroori | Daily work ke liye use ho sakta hai |
| Routine work ke liye avoid karna chahiye | Specific permissions ke saath use karna behtar hai |

**Security Best Practice:** Root user ko daily tasks ke liye use na karein. Root user par MFA enable karein aur routine AWS work ke liye suitable IAM identities ya IAM Identity Center use karein.

## 4. IAM User Authentication

Authentication ka matlab hai kisi identity ki pehchan verify karna.

AWS mein authentication ke common methods:

### 4.1 Console Password

IAM user AWS Management Console mein username aur password ke through sign in kar sakta hai, agar console access configure kiya gaya ho.

**Example:** `student-read` user console mein login karke EC2 instances ki information dekh sakta hai, agar usay required permissions mili hui hon.

### 4.2 Access Keys

Access keys programmatic access ke liye use hoti hain, jaise AWS CLI, SDKs ya applications.

Access keys mein aam tor par do parts hote hain:

- Access Key ID
- Secret Access Key

**Important:** Secret access key ko password ki tarah confidential rakhein. Isay GitHub repository, screenshots, public files ya chat mein share na karein.

### 4.3 Multi-Factor Authentication (MFA)

MFA security ki additional layer hai. Is mein password ke ilawa ek additional authentication factor use hota hai.

MFA ke examples mein authenticator application ya supported security key shamil ho sakti hai.

**Real-World Example:** Agar kisi attacker ko password mil bhi jaye, to MFA account ko protect karne mein madad de sakta hai.

## 5. IAM User Console Access

IAM user ko AWS Management Console ka access tab milta hai jab us ke liye console sign-in configure kiya gaya ho.

User ko sign-in karne ke liye aam tor par yeh details chahiye hoti hain:

- AWS account ID ya account alias
- IAM username
- Password
- MFA verification, agar enabled ho

**Important:** Console login milne ka matlab yeh nahi ke user automatically har AWS service access kar sakta hai. Us ke actions assigned permissions par depend karte hain.

## 6. IAM User Permissions

IAM user ki permissions policies ke zariye define ki ja sakti hain.

Permissions determine karti hain ke user:

- Kaun si AWS service access kar sakta hai.
- Kaun sa action perform kar sakta hai.
- Kis resource par action perform kar sakta hai.
- Kin conditions mein action allowed hoga.

**Example:** Ek user ko EC2 instances list karne ki permission di ja sakti hai, lekin instances terminate karne ki permission na di jaye.

## 7. IAM Users and Groups

IAM group multiple IAM users ko ek jagah organize karne ka tareeqa hai.

Group ko policy attach karne se us group ke users ko defined permissions mil sakti hain.

### Example

Ek company mein 10 developers hain. Har developer ko alag alag policy attach karne ke bajaye administrator `Developers` naam ka group create kar sakta hai aur us group ko suitable policy attach kar sakta hai.

Group membership ke through milne wali permissions user ki doosri applicable policies ke saath evaluate hoti hain.

**Important:** IAM group ek management facility hai; group khud login karne wali identity nahi hota.

## 8. IAM User Security Best Practices

- Root user ko routine tasks ke liye use na karein.
- Root aur privileged identities par MFA enable karein.
- Har user ko sirf required permissions dein.
- Shared usernames aur passwords se parhez karein.
- Long-term access keys create karne se pehle alternatives consider karein.
- Agar access keys use hon, to unhein securely store aur regularly review karein.
- Unused IAM users aur credentials ko review karke disable ya remove karein.
- IAM policies aur access permissions ko regularly audit karein.

---

# Part 2: IAM Policies

## 9. What Is an IAM Policy?

IAM Policy ek JSON document hota hai jo define karta hai ke AWS mein kaun sa action allow ya deny hai, kis resource par apply hota hai aur kin conditions mein permission effective hogi.

Policies AWS mein access control ka important hissa hain.

### Simple Example

Agar kisi student ko sirf EC2 instances ki list dekhne ki permission deni hai, to ek policy `ec2:DescribeInstances` action allow kar sakti hai.

Is ka matlab yeh nahi ke student automatically instances start, stop ya terminate bhi kar sakta hai.

## 10. Purpose of IAM Policies

IAM policies ka main purpose AWS resources tak access ko control karna hai.

Policies ki madad se hum:

- Required permissions grant karte hain.
- Unnecessary permissions ko avoid karte hain.
- Sensitive resources ko protect karte hain.
- Users aur roles ke access ko manage karte hain.
- Security aur compliance requirements ko support karte hain.

### Real-World Example

Hospital ke AWS environment mein developer ko application resources ka access diya ja sakta hai, jabke patient records ko access karne ki permission sirf authorized identities ko di jaye.

## 11. Types of IAM Policies

### 11.1 Identity-Based Policies

Identity-based policies IAM users, groups ya roles ke saath attach hoti hain.

Yeh define karti hain ke identity kin actions ko perform kar sakti hai.

Identity-based policies ki common categories:

- **Managed Policies:** AWS ya customer ke through manage ki ja sakti hain.
- **Inline Policies:** Kisi ek identity ke saath directly embedded hoti hain.

### 11.2 AWS Managed Policies

AWS managed policies AWS ke through create aur maintain ki jati hain.

In policies ko multiple identities ke saath attach kiya ja sakta hai, agar required permissions hon.

**Example:** `ReadOnlyAccess` ek AWS managed policy hai jo supported AWS services mein read-only access provide karti hai. Is ka exact scope policy document se verify karna chahiye.

### 11.3 Customer Managed Policies

Customer managed policies customer khud create aur maintain karta hai.

Yeh reusable hoti hain aur multiple users ya roles ko attach ki ja sakti hain.

**Example:** Company `EC2-Read-Only-Custom` policy create kar sakti hai jo sirf required EC2 information read karne ki permissions define kare.

### 11.4 Inline Policies

Inline policy kisi specific user, group ya role ke saath directly attach hoti hai.

Yeh tab useful ho sakti hai jab permission set sirf ek identity ke liye ho.

**Important Difference:**

- Managed policy ko multiple identities reuse kar sakti hain.
- Inline policy ek specific identity ke saath directly associated hoti hai.

Policy type ka selection organization ki security aur management requirements par depend karta hai.

### 11.5 Resource-Based Policies

Resource-based policies directly kisi supported AWS resource ke saath attach hoti hain.

Yeh batati hain ke kaun si identity resource ko access kar sakti hai aur kin actions ke liye.

**Example:** Amazon S3 bucket policy define kar sakti hai ke kis AWS principal ko bucket ke objects read karne ki permission ho.

Har AWS service aur resource resource-based policies support nahi karta.

### 11.6 Permissions Boundaries

Permissions boundary ek policy hoti hai jo identity-based policies ke through milne wali maximum permissions ki limit define karti hai.

Yeh khud permissions grant nahi karti; yeh maximum effective permissions ko restrict karne mein madad deti hai.

**Example:** Developer ko policies attach karne ki permission ho, lekin permissions boundary us ke effective access ko defined limits se bahar jaane se roke.

### 11.7 Service Control Policies (SCPs)

Service Control Policies AWS Organizations mein organization ke member accounts ke liye available maximum permissions define karne mein madad karti hain.

SCP khud kisi user ko permission grant nahi karti.

**Example:** Organization apne member accounts mein certain services ke use ko restrict kar sakti hai.

SCP ka effect organization ke account structure aur applicable rules par depend karta hai. Management account aur doosre special cases ke rules alag ho sakte hain.

---

## 12. IAM Policy Structure

IAM policies aam tor par JSON format mein likhi jati hain.

### Example: EC2 Instances Read Permission

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "ViewEC2Instances",
      "Effect": "Allow",
      "Action": "ec2:DescribeInstances",
      "Resource": "*"
    }
  ]
}
```

Yeh example EC2 instances ki information dekhne ki permission allow karta hai. Is ka scope sirf is statement mein specified action hai; yeh EC2 ko start, stop ya terminate karne ki permission nahi deta.

### 12.1 Version

`Version` policy language ka version specify karta hai.

Common value:

`2012-10-17`

Yeh policy language version hai, policy banane ki date nahi.

### 12.2 Statement

`Statement` policy ke permission rules contain karta hai.

Ek policy mein ek ya multiple statements ho sakte hain.

Har statement kisi action ko allow ya deny kar sakta hai aur resource aur conditions define kar sakta hai.

### 12.3 Sid

`Sid` ka full form Statement ID hai.

Yeh statement ko identify karne ke liye optional label hota hai.

**Example:** `ViewEC2Instances`

### 12.4 Effect

`Effect` batata hai ke policy statement permission ko allow karta hai ya deny.

Is ki do main values hain:

- `Allow` — specified action ko allow karta hai.
- `Deny` — specified action ko deny karta hai.

Explicit `Deny` applicable `Allow` ko override karta hai.

### 12.5 Action

`Action` define karta hai ke kaun sa AWS operation allow ya deny hai.

**Examples:**

- `ec2:DescribeInstances` — EC2 instances ki information dekhna.
- `ec2:StartInstances` — EC2 instances start karna.
- `ec2:StopInstances` — EC2 instances stop karna.
- `s3:ListBucket` — S3 bucket ke objects ki listing karna.
- `s3:GetObject` — S3 object read karna, subject to applicable permissions.

Har action ki permission us service ke authorization rules ke mutabiq evaluate hoti hai.

### 12.6 Resource

`Resource` specify karta hai ke policy kis AWS resource par apply hoti hai.

Kuch actions resource-level permissions support karte hain, jabke kuch actions ke liye `"Resource": "*"` required hota hai.

**Example:**

`"Resource": "*"`

Is ka matlab specified action ke liye all applicable resources hain. Is ka matlab yeh nahi ke policy automatically har AWS action allow karti hai.

Production environment mein jahan mumkin ho, required resources tak scope limit karna behtar hota hai.

### 12.7 Condition

`Condition` additional rules define karta hai jin ke true hone par policy statement apply hota hai.

Conditions ke through permissions ko specific circumstances tak limit kiya ja sakta hai.

**Possible Examples:**

- Specific IP address range.
- Specific request attributes.
- Required tags.
- Supported services mein encryption ya transport-related requirements.

Condition keys aur operators service aur action ke mutabiq select karne chahiye.

---

## 13. Authentication vs Authorization

### Authentication

Authentication ka matlab identity verify karna hai.

**Example:** IAM username aur password ke through AWS Console mein sign in karna.

### Authorization

Authorization ka matlab decide karna hai ke authenticated identity ko kaun se actions perform karne ki permission hai.

**Example:** Login ke baad user EC2 instances dekh sakta hai, lekin terminate nahi kar sakta.

**Yaad Rakhein:** Authentication batata hai ke aap kaun hain; authorization batata hai ke aap kya kar sakte hain.

## 14. Allow vs Deny

### Allow

Allow statement kisi specified action ko permission de sakta hai.

### Deny

Deny statement specified action ko restrict karta hai.

AWS policy evaluation mein applicable explicit Deny, applicable Allow par priority rakhta hai.

Agar koi applicable Allow na ho aur kisi aur rule se access grant na ho, to request aam tor par implicit deny hoti hai.

**Example:**

Agar user ko EC2 instances dekhne ki Allow permission hai, lekin kisi applicable policy mein unhein terminate karne ki Explicit Deny hai, to user instances terminate nahi kar sakega.

## 15. Principle of Least Privilege

Principle of Least Privilege ka matlab user ya application ko sirf utni permissions dena hai jitni usay apna kaam karne ke liye required hon.

**Example:**

Agar employee ka kaam EC2 instances ki information dekhna hai, to usay sirf required read permissions di jani chahiye. Start, stop aur terminate permissions bina zaroorat grant nahi karni chahiye.

Least privilege se accidental mistakes aur unauthorized actions ka risk kam ho sakta hai.

## 16. IAM Policy Evaluation

AWS request ko evaluate karte waqt applicable policies aur permissions boundaries, organization policies, resource policies aur doosre relevant authorization rules ko consider kar sakta hai.

**General Concepts:**

1. Request ki identity aur target resource identify hote hain.
2. Applicable policies evaluate hoti hain.
3. Explicit Deny milne par request deny hoti hai.
4. Applicable Allow aur baqi required authorization conditions satisfy honi chahiye.
5. Agar required permission grant nahi hoti, to request aam tor par deny hoti hai.

Actual evaluation identity type, resource type, AWS service aur policy combination par depend karti hai.

## 17. Practical Lab: Three IAM Users

Is practical task mein 3 IAM users create kiye ja sakte hain:

1. `student-read`
2. `student-write`
3. `student-denied`

Maqsad yeh samajhna hai ke different policies different users ke access ko kaise affect karti hain.

### 17.1 student-read

Is user ko selected resources ki read-only permissions di jati hain.

**Possible Actions:**

- EC2 instances ki listing.
- Supported resource information dekhna.

**Expected Learning:** User allowed read actions perform kar sakta hai, lekin sirf read permission ki wajah se write actions automatically allowed nahi hote.

### 17.2 student-write

Is user ko selected resources par required write permissions di jati hain.

Write permission ka exact scope policy par depend karta hai. Misal ke taur par, kisi specific resource ko create ya update karne ki permission di ja sakti hai.

**Expected Learning:** User ko sirf un actions ka access milna chahiye jo policy explicitly allow karti hai aur jin ke liye baqi authorization requirements bhi satisfy hon.

### 17.3 student-denied

Is user ke liye ek relevant action par Explicit Deny configure ki ja sakti hai.

**Expected Learning:** Applicable Explicit Deny, doosri applicable Allow permission ke bawajood us action ko block kar sakti hai.

**Important:** User ka exact access test ki gayi policy, resource aur AWS service par depend karta hai. Is liye practical test ke results ko actual policy ke saath verify karna chahiye.

## 18. IAM Users and Policies: Real-World Scenario

Ek organization AWS par online shopping website host karti hai.

- **Developer:** Application ke required resources par development permissions rakhta hai.
- **Security Analyst:** Security configuration aur logs ki required information read karta hai.
- **Administrator:** Approved administrative tasks perform karta hai.
- **Finance Employee:** Billing information ke liye required access rakhta hai.

IAM users ya suitable identities ke saath policies attach karke organization har role ka access manage kar sakti hai.

Is approach se access control behtar hota hai aur unnecessary permissions ko reduce kiya ja sakta hai.

## 19. Common IAM Mistakes

- Har user ko `AdministratorAccess` de dena.
- Root user ko daily tasks ke liye use karna.
- Access keys ko public GitHub repository mein upload karna.
- `"Resource": "*"` ko bina samjhe use karna.
- `Allow` aur `Deny` ka difference na samajhna.
- Console access aur AWS permissions ko ek hi cheez samajhna.
- Policy changes ke baad access test na karna.
- Unused users aur credentials ko review na karna.

---

## 20. Quick Revision

### IAM Users

- IAM = Identity and Access Management.
- IAM user AWS account ke andar ek identity hoti hai.
- Authentication identity ko verify karta hai.
- Authorization actions aur permissions ko determine karta hai.
- Console access aur programmatic access alag methods hain.
- IAM groups users ko organize karne aur permissions manage karne mein madad karte hain.
- Root user ko secure rakhein aur routine tasks ke liye avoid karein.

### IAM Policies

- IAM policy JSON document hota hai.
- `Version` policy language version batata hai.
- `Statement` permission rules contain karta hai.
- `Sid` optional statement identifier hai.
- `Effect` Allow ya Deny specify karta hai.
- `Action` AWS operation specify karta hai.
- `Resource` target resource define karta hai.
- `Condition` additional requirements define karti hai.
- Explicit Deny applicable Allow ko override karta hai.
- Least Privilege ka matlab minimum required permissions dena hai.
- AWS managed, customer managed aur inline policies identity-based policy management ke common types hain.
- Resource-based policies resources ke saath attach hoti hain.
- Permissions boundaries maximum permissions ko limit karti hain.
- SCPs AWS Organizations mein member accounts ke maximum available permissions ko control karne mein madad karti hain.

### Final Security Principle

**Har identity ko sirf required access dein, permissions ko regularly review karein aur AWS resources ko least privilege ke principle ke mutabiq secure karein.**
