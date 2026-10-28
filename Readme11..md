# AWS CloudWatch & CloudTrail

## 1. Introduction

AWS CloudWatch aur AWS CloudTrail dono AWS ki important services hain jo monitoring, troubleshooting aur security mein help karti hain.

Dono ka purpose different hai:

* **CloudWatch:** AWS resources ki performance aur application logs ko monitor karta hai.
* **CloudTrail:** AWS account mein perform hone wale actions ka record rakhta hai.

---

# 2. Amazon CloudWatch

## Definition

Amazon CloudWatch AWS ki monitoring service hai jo AWS resources aur applications ki performance, metrics aur logs ko monitor karne mein help karti hai. Iski madad se hum errors identify kar sakte hain, performance check kar sakte hain aur specific conditions par alerts configure kar sakte hain.

## Important Components of CloudWatch

### 2.1 Metrics

Metrics numerical data hota hai jo kisi AWS resource ki performance ko represent karta hai.

**Example:**

EC2 instance ka CPU utilization 85% hai. CloudWatch is metric ko monitor kar sakta hai, jis se humein pata chalta hai ke instance kitna CPU use kar raha hai.

### 2.2 Logs

Logs mein applications aur services ki activities, messages aur errors ka record hota hai.

**Example:**

Jab hum AWS Lambda function execute karte hain, to code mein likhe gaye `print()` statements ke messages CloudWatch Logs mein dekhe ja sakte hain.

Agar function mein error aaye, to relevant error details bhi logs mein mil sakti hain.

### 2.3 CloudWatch Alarms

CloudWatch Alarms kisi metric ya supported condition ko monitor karte hain. Jab configured condition meet hoti hai, to alarm notification ya doosra configured action trigger kar sakta hai.

**Example:**

Agar EC2 instance ka CPU utilization 5 minutes tak 80% se zyada rahe, to CloudWatch Alarm ko notification bhejne ke liye configure kiya ja sakta hai.

### 2.4 Dashboards

Dashboards ki madad se hum multiple AWS resources ki important metrics ko ek hi jagah par dekh sakte hain.

**Example:**

Ek dashboard par EC2 CPU utilization, Lambda errors aur doosri relevant metrics display karna.

## Real-World Example: Online Shopping Website

Socho ek company ki online shopping website AWS par host hai.

Sale ke din website par bohat zyada customers visit karte hain aur website slow ho jati hai.

CloudWatch ki madad se company:

1. EC2 instance ka CPU utilization check kar sakti hai.
2. Application ke logs mein errors dekh sakti hai.
3. Lambda function ke execution logs check kar sakti hai.
4. High CPU utilization ke liye alarm configure kar sakti hai.
5. Performance issues investigate kar sakti hai.

**Result:** Company ko website ki performance monitor karne aur problems identify karne mein help milti hai.

---

# 3. AWS CloudTrail

## Definition

AWS CloudTrail AWS ki auditing service hai jo AWS account mein users, roles aur AWS services ke actions ka record rakhti hai. Iski madad se hum investigate kar sakte hain ke kis identity ne kya action perform kiya, action kab hua aur us se related available details kya hain.

## Important Components of CloudTrail

### 3.1 Events

CloudTrail events AWS account mein perform hone wale recorded actions ka record hote hain.

**Example:**

Kisi IAM user ne EC2 instance terminate karne ki request ki. CloudTrail relevant API event record kar sakta hai.

### 3.2 Event History

Event History ki madad se hum AWS account ke recent management events ko search aur review kar sakte hain.

**Example:**

Agar humein pata karna ho ke EC2 instance ko kis waqt terminate kiya gaya tha, to CloudTrail Event History mein relevant event search kar sakte hain.

### 3.3 Trails

Trail configure karne se CloudTrail events ko Amazon S3 bucket mein store karne ke liye deliver karwaya ja sakta hai. Configuration ke mutabiq CloudWatch Logs jaisi destinations bhi use ki ja sakti hain.

Is se account activity ka record maintain karne aur future investigations mein help milti hai.

### 3.4 Security Auditing

CloudTrail security investigations aur auditing mein help karta hai.

**Example:**

Agar kisi S3 bucket ki permissions change ho jayein, to CloudTrail ke relevant events check karke investigate kiya ja sakta hai ke change kis identity ne aur kab kiya.

Yaad rahe ke CloudTrail har unauthorized action ko automatically block nahi karta. Ye recorded activities ki investigation mein help karta hai.

## Real-World Example: Company ka AWS Account

Socho ek company mein multiple employees AWS resources manage karte hain.

Ek din company ki S3 bucket ki permissions change ho jati hain aur security team ko is change ki investigation karni hai.

CloudTrail ki madad se team:

1. Relevant S3 API event search kar sakti hai.
2. Event mein user ya role ki identity check kar sakti hai.
3. Action ka timestamp dekh sakti hai.
4. Available request details investigate kar sakti hai.
5. Security investigation ke liye relevant information collect kar sakti hai.

**Result:** Company ko AWS account ki activities audit karne aur security incidents investigate karne mein help milti hai.

---

# 4. CloudWatch vs CloudTrail

Dono services AWS security aur monitoring mein useful hain, lekin inka main purpose different hai.

| Feature        | CloudWatch                                           | CloudTrail                                                          |
| -------------- | ---------------------------------------------------- | ------------------------------------------------------------------- |
| Main Purpose   | Monitoring                                           | Auditing                                                            |
| Focus          | Resource performance aur application activity        | AWS account mein perform hone wale actions                          |
| Main Question  | System mein kya ho raha hai?                         | Kis ne kya action perform kiya?                                     |
| Data           | Metrics, logs aur alarms                             | API events aur account activity records                             |
| EC2 Example    | CPU utilization monitor karna                        | Kis identity ne EC2 instance terminate kiya                         |
| Lambda Example | Execution logs aur errors check karna                | Lambda se related recorded API activity check karna                 |
| S3 Example     | Application logs aur supported metrics monitor karna | S3 bucket ki settings change karne wala event investigate karna     |
| Alerts         | Metrics aur logs par alarms configure karna          | Events ko doosri services ke saath use karke alerts configure karna |
| Security Use   | Operational issues identify karna                    | Account activity audit aur investigate karna                        |
| Main Benefit   | Performance monitoring aur troubleshooting           | Activity tracking aur security auditing                             |

**Important Note:** S3 objects ke upload, download aur delete operations ko CloudTrail mein record karne ke liye relevant S3 data events configure karne ki zaroorat ho sakti hai.

---

# 5. Real-World Scenario: CloudWatch and CloudTrail Together

Socho ek company ki website EC2 instance par host hai aur important files S3 bucket mein store hoti hain.

Ek din website slow ho jati hai aur S3 bucket ki permissions bhi change ho jati hain.

## CloudWatch ka Role

1. EC2 ka CPU utilization check karna.
2. Application ke logs mein errors identify karna.
3. Configured metrics aur alarms ke zariye performance issues ka alert dena.
4. Troubleshooting ke liye relevant logs aur metrics analyze karna.

## CloudTrail ka Role

1. S3 bucket ki permissions change karne wala relevant event search karna.
2. Event mein identity information check karna.
3. Action ka timestamp dekhna.
4. Available request details investigate karna.

**Conclusion:** CloudWatch performance issues ko monitor aur troubleshoot karne mein help karta hai, jabke CloudTrail AWS account mein perform hone wale recorded actions ki investigation mein help karta hai.

---

# 6. AWS Lambda Example

Hum CloudWatch aur CloudTrail ke difference ko AWS Lambda aur S3 trigger ki example se bhi samajh sakte hain.

## CloudWatch

Jab S3 bucket mein file upload hoti hai aur configured trigger Lambda function ko invoke karta hai, to:

* Lambda function execute hota hai.
* Code ke `print()` statements se generate hone wale messages CloudWatch Logs mein dekhe ja sakte hain.
* Function mein error aaye to relevant logs check kiye ja sakte hain.
* CloudWatch metrics se function ke executions, errors aur duration monitor kiye ja sakte hain.

## CloudTrail

CloudTrail ki madad se Lambda aur S3 se related recorded API activities investigate ki ja sakti hain.

**Example:**

Agar kisi ne Lambda function ki configuration change ki ya S3 bucket ki settings modify ki, to relevant recorded events search kiye ja sakte hain.

**Important Difference:**

CloudWatch Logs mein Lambda ke execution messages dekhna aur CloudTrail mein AWS API activities dekhna do different cheezein hain.

---

# 7. Important Points for Quick Revision

## CloudWatch

* AWS monitoring service hai.
* Metrics collect aur monitor karta hai.
* Application aur service logs provide karta hai.
* Configured conditions par alarms generate kar sakta hai.
* Dashboards ke zariye metrics display kar sakta hai.
* Performance monitoring aur troubleshooting mein help karta hai.

## CloudTrail

* AWS auditing service hai.
* AWS account ki recorded activities ka record rakhta hai.
* API events ke zariye actions investigate karne mein help karta hai.
* User aur role ki identity se related available information provide karta hai.
* Security investigations aur compliance mein help karta hai.
* Trails ke zariye events ko Amazon S3 mein deliver kiya ja sakta hai.

---

# 8. Quick Revision Trick

**CloudWatch = What is happening?**

System ki performance kaisi hai? CPU kitna use ho raha hai? Lambda mein errors aa rahe hain?

**CloudTrail = Who did what?**

Kis identity ne EC2 instance terminate kiya? Kis ne IAM policy modify ki? S3 bucket ki settings kis ne change ki?

---

# 9. Final Summary

Amazon CloudWatch aur AWS CloudTrail dono AWS environment ko manage karne mein important role perform karte hain.

CloudWatch resources ki performance aur operational activity ko monitor karne mein help karta hai. Iski madad se hum metrics, logs aur alarms use karke performance issues identify kar sakte hain.

CloudTrail AWS account mein perform hone wale recorded actions ka audit trail provide karta hai. Iski madad se hum investigate kar sakte hain ke kis identity ne kya action perform kiya aur woh action kab hua.

**Final Difference:**

* **CloudWatch:** Performance Monitoring and Troubleshooting
* **CloudTrail:** Activity Tracking and Auditing
