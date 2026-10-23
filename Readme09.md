# AWS Lambda — Complete Notes

---

## 1. What is AWS Lambda?

### Definition

AWS Lambda Amazon Web Services (AWS) ki ek **serverless computing service** hai. Iski madad se hum apna code run kar sakte hain bina server ko manually create, configure aur maintain kiye.

Lambda mein hum apna code upload karte hain aur define karte hain ke code kis event par execute hona chahiye. Jab woh event hota hai, Lambda automatically code run kar deta hai.

Iska matlab yeh nahi ke servers exist nahi karte. Servers AWS manage karta hai, jabke developer apne code aur function configuration par focus karta hai.

### Simple Example

Suppose hum chahte hain ke jab bhi koi user Amazon S3 bucket mein image upload kare, to Lambda automatically us file ke event ko process kare.

Jab S3 bucket mein image upload hogi, S3 event Lambda function ko invoke karega aur Lambda ka code execute ho jayega.

### Real-World Example

Ek online shopping application mein customer order place karta hai. Lambda function order-related event receive karke order details process karne ya confirmation notification bhejne mein madad kar sakta hai.

### Important Points

* Lambda server infrastructure ko automatically manage karta hai.
* Lambda functions events ke response mein execute ho sakte hain.
* AWS Lambda different AWS services ke saath integrate hota hai.
* Billing requests, execution duration aur configuration jaise factors par depend karti hai.
* Lambda har situation mein EC2 ka replacement nahi hai.

---

## 2. Serverless Computing

### Definition

Serverless Computing ek cloud computing model hai jisme developer ko servers ki provisioning, operating system maintenance aur infrastructure scaling ko manually manage nahi karna parta.

Servers phir bhi exist karte hain, lekin underlying infrastructure manage karne ki zimmedari cloud provider ki hoti hai.

### Simple Example

Traditional server use karte waqt humein server configure karna, application deploy karna aur resources manage karne parte hain.

Lambda mein hum function ka code likhte hain aur event configure karte hain. AWS Lambda required infrastructure manage karta hai.

### Real-World Example

Ek website par user contact form submit karta hai. Lambda function form ka data process karke notification bhejne mein madad kar sakta hai.

### Benefits

* Server management kam ho jati hai.
* Supported workloads ke liye automatic scaling hoti hai.
* Event-based tasks ke liye useful hai.
* Developers application logic par focus kar sakte hain.

---

## 3. Lambda Function

### Definition

Lambda Function code ka ek unit hota hai jo kisi specific task ko perform karta hai. Yeh function kisi event ke response mein execute ho sakta hai.

Function mein hum programming logic likhte hain, jaise file process karna, data validate karna ya notification bhejna.

### Simple Example

```python
def lambda_handler(event, context):
    name = event.get("name", "User")

    return {
        "message": f"Hello, {name}!"
    }
```

Agar event mein `name` ki value `Shamim` ho, to function greeting message return karega.

### Real-World Example

Ek e-commerce website par customer order place karta hai. Lambda function order details receive karke required validation kar sakta hai.

### Important Points

* Har function ka ek specific purpose ho sakta hai.
* Function mein code aur configuration hoti hai.
* Function ko manually test kiya ja sakta hai.
* Function ko events ke zariye automatically invoke bhi kiya ja sakta hai.

---

## 4. How AWS Lambda Works

### Definition

AWS Lambda ka workflow batata hai ke event generate hone se lekar function execute hone aur result ya logs milne tak process kis tarah complete hota hai.

### Working Process

**Step 1: Event Occurs**

Koi activity hoti hai, jaise Amazon S3 bucket mein file upload hona.

**Step 2: Trigger Activates**

S3 event configuration Lambda function ko invoke karne ka process start karti hai.

**Step 3: Lambda Receives Event**

Lambda function ko event data milta hai. Is data mein file ya event ke baare mein relevant information ho sakti hai.

**Step 4: Function Executes**

Lambda function apna code run karta hai aur configured task perform karta hai.

**Step 5: Logs Are Recorded**

Agar logging configured hai, to execution ke logs Amazon CloudWatch Logs mein dekhe ja sakte hain.

### Example: S3 to Lambda

```text
User Uploads a File
         |
         v
   Amazon S3 Bucket
         |
         v
      S3 Event
         |
         v
   AWS Lambda Function
         |
         v
     Code Execution
         |
         v
  Amazon CloudWatch Logs
```

### Real-World Example

Ek company customer ki uploaded images ko process karna chahti hai. S3 mein image upload hone par Lambda image-processing workflow start kar sakta hai.

---

## 5. Main Components of Lambda

### 5.1 Trigger

**Definition:** Trigger woh event source ya configured mechanism hota hai jo Lambda function ko invoke karne ka process start karta hai.

**Examples:**

* Amazon S3 mein file upload hona.
* Amazon EventBridge ka scheduled event.
* Amazon API Gateway ke through API request.
* Amazon SQS queue mein message receive hona.

**Real-World Example:** Jab user S3 bucket mein PDF upload kare, to S3 event Lambda function ko trigger kar sakta hai.

### 5.2 Event

**Definition:** Event woh data hota hai jo Lambda function ko us activity ke baare mein information deta hai jis ki wajah se function invoke hua.

Event mein operation se related details ho sakti hain, jaise S3 bucket ka naam aur uploaded object ka key.

**Example:** S3 object event mein bucket aur file ka naam diya ja sakta hai. Lambda is information ko use karke uploaded file process kar sakta hai.

**Trigger aur Event mein Difference:**

* **Trigger:** Function ko invoke karne ka process start karta hai.
* **Event:** Function ko process karne ke liye relevant data provide karta hai.

### 5.3 Handler

**Definition:** Handler woh function ya entry point hota hai jahan se AWS Lambda execution ke waqt tumhare code ko call karta hai.

Python mein handler function ko `event` aur `context` parameters mil sakte hain.

```python
def lambda_handler(event, context):
    print("Lambda function executed")
```

Yahan `lambda_handler` Python function ka naam hai. Lambda configuration mein bhi isi handler ko specify karna hota hai.

### 5.4 Runtime

**Definition:** Runtime woh environment hai jo Lambda function ke code ko execute karne ke liye programming language ki required support provide karta hai.

AWS Lambda Python aur Node.js jaisi programming languages ke runtimes support karta hai. Available runtime versions waqt ke saath change ho sakte hain.

**Example:** Agar function Python mein likha gaya hai, to uske liye compatible Python runtime configure karna hoga.

### 5.5 Execution Role

**Definition:** Execution role ek IAM role hota hai jo Lambda function ko AWS services aur resources ke saath interact karne ke liye required permissions provide karta hai.

**Example:** Agar Lambda function ko kisi S3 bucket se file read karni hai, to uski execution role mein required S3 read permissions honi chahiye.

### 5.6 CloudWatch Logs

**Definition:** Amazon CloudWatch Logs ek AWS service hai jo applications aur AWS resources ke logs collect, store aur inspect karne mein madad karti hai.

**Example:** Agar Lambda function mein `print("File uploaded")` likha ho, to yeh message function ke logs mein nazar aa sakta hai, jab logging permissions aur configuration available hon.

---

## 6. Event-Driven Architecture

### Definition

Event-Driven Architecture ek software design approach hai jisme application ke different components events ke response mein kaam karte hain.

Is architecture mein ek service event generate karti hai aur doosri service us event ko receive karke required action perform karti hai.

### Simple Example

```text
S3 File Upload
      |
      v
   S3 Event
      |
      v
 Lambda Function
      |
      v
  Process File
```

### Real-World Example

Ek online store mein order place hone ke baad different tasks perform ho sakte hain:

* Order information process karna.
* Customer ko confirmation bhejna.
* Inventory update karna.
* Reporting system ko event provide karna.

In tasks ko suitable event-driven services ke zariye connect kiya ja sakta hai.

### Benefits

* Application ke components loosely coupled ho sakte hain.
* Events ke response mein automatic processing hoti hai.
* Traffic ke mutabiq services scale kar sakti hain.
* Complex workflows ko smaller tasks mein divide kiya ja sakta hai.

---

## 7. Lambda Invocation Types

### Definition

Invocation ka matlab hai Lambda function ko execute karne ke liye request bhejna.

AWS Lambda mein invocation ka behavior is baat par depend karta hai ke function kis service ya method ke zariye invoke ho raha hai.

### 7.1 Synchronous Invocation

Is method mein caller function ko invoke karta hai aur function ke execution ka response receive karta hai.

**Example:** API Gateway ke through request aati hai aur Lambda response return karta hai.

```text
Client Request
      |
      v
 Lambda Function
      |
      v
Response to Client
```

**Use Cases:**

* API requests.
* Form validation.
* Request ka direct response generate karna.

### 7.2 Asynchronous Invocation

Is method mein event accept hone ke baad caller ko function ke complete hone ka wait karna zaroori nahi hota.

Lambda event ko process karne ke liye schedule karta hai. Failures aur retries ka behavior invocation configuration aur event source par depend karta hai.

**Example:** Amazon S3 mein object upload hone par Lambda ko asynchronous event ke zariye invoke kiya ja sakta hai.

```text
S3 Event
   |
   v
Lambda Accepts Event
   |
   v
Function Processes Event
```

### Important Difference

| Feature        | Synchronous                       | Asynchronous                                               |
| -------------- | --------------------------------- | ---------------------------------------------------------- |
| Response       | Caller response ka wait karta hai | Caller ko execution complete hone ka wait nahi karna parta |
| Common Example | API Gateway request               | S3 object-created event                                    |
| Main Use       | Request ka direct response        | Background event processing                                |

---

## 8. Scaling and Concurrency

### Definition of Scaling

Scaling ka matlab application ki demand ke mutabiq available computing capacity ko adjust karna hai.

AWS Lambda incoming requests aur events ko handle karne ke liye automatically execution environments scale kar sakta hai, subject to service quotas aur configuration limits.

### Definition of Concurrency

Concurrency ka matlab hai ek waqt mein kitne Lambda function executions chal rahe hain.

Agar bohat se events ek saath aate hain, to Lambda ko multiple executions run karne ki zaroorat ho sakti hai.

### Simple Example

Suppose ek application ko normal days par 10 requests milti hain, lekin sale ke din 1,000 requests aa jati hain.

Lambda incoming workload ke mutabiq executions scale kar sakta hai. Lekin concurrency limits ya doosri service limits hit hone par requests throttle bhi ho sakti hain.

### Definition of Throttling

Throttling us situation ko kehte hain jab requests available concurrency ya service limits ki wajah se temporarily restrict ho jati hain.

### Real-World Example

Online shopping sale ke waqt achanak bohat zyada requests aane par Lambda concurrency limits monitor karna zaroori hai.

### Important Points

* Lambda automatic scaling support karta hai.
* Concurrency limits ko samajhna zaroori hai.
* High traffic ke liye monitoring aur testing important hain.
* Automatic scaling ka matlab unlimited capacity nahi hota.

---

## 9. Cold Start

### Definition

Cold start us waqt hota hai jab AWS Lambda ko function execute karne ke liye naya execution environment prepare karna parta hai.

Is initialization process ki wajah se function ki request mein additional delay ho sakta hai.

Har invocation par cold start nahi hota. Agar suitable execution environment reuse ho jaye, to initialization ka extra time bach sakta hai.

### Simple Example

Agar Lambda function kuch der se invoke nahi hua aur uske liye naya execution environment initialize karna pare, to pehli request normal request se thori slow ho sakti hai.

### Cold Start ko Affect Karne Wale Factors

* Programming language runtime.
* Function package ka size.
* Dependencies ki quantity.
* Initialization ke waqt perform hone wala work.
* VPC aur doosri configuration details.

### Possible Improvements

* Unnecessary dependencies kam rakhein.
* Initialization code ko efficient banayein.
* Function package ko unnecessarily large na karein.
* Latency-sensitive applications ke liye suitable configuration consider karein.

---

## 10. Runtime and Handler

### Runtime

Runtime code execute karne ke liye required programming language environment provide karta hai.

**Example:** Python runtime Python code ko execute karne mein madad karta hai.

### Handler

Handler function ka entry point hota hai jahan se Lambda execution start karta hai.

### Python Example

```python
def lambda_handler(event, context):
    name = event.get("name", "User")

    print(f"Processing request for {name}")

    return {
        "statusCode": 200,
        "body": f"Hello, {name}!"
    }
```

### Code Explanation

* `lambda_handler`: Handler function ka naam hai.
* `event`: Request ya event se milne wala data hai.
* `context`: Current invocation aur execution environment ke baare mein information provide karta hai.
* `event.get("name", "User")`: Event mein `name` available ho to woh use karta hai; warna `"User"` use hota hai.
* `print()`: Message ko logs mein record karne mein madad karta hai.
* `return`: Function ka response return karta hai.

### Important Point

Agar Python file ka naam `lambda_function.py` hai aur handler ka naam `lambda_handler` hai, to handler setting aam tor par yeh hogi:

```text
lambda_function.lambda_handler
```

---

## 11. Memory and Timeout

### Memory

**Definition:** Lambda memory woh configured memory amount hai jo function ke execution environment ko allocate ki jati hai.

Memory configuration CPU resources aur doosre available resources par bhi asar dalti hai. Is liye memory barhane se kuch workloads ki processing speed improve ho sakti hai.

**Example:** Agar image processing function ko zyada computation ki zaroorat hai, to suitable memory configuration uski performance improve kar sakti hai.

### Timeout

**Definition:** Timeout woh maximum duration hai jitni der Lambda function ek invocation ke liye run kar sakta hai. Agar function configured duration ke andar complete nahi hota, to invocation timeout ho sakti hai.

AWS Lambda function ka maximum timeout **900 seconds, yani 15 minutes** hai.

**Example:** Agar timeout 30 seconds configure hai aur function us waqt tak complete nahi hota, to invocation timeout ho sakti hai.

### Important Points

* Memory ko workload ke mutabiq configure karein.
* Timeout task ki expected duration ke mutabiq set karein.
* Bohat kam timeout legitimate task ko fail karwa sakta hai.
* Bohat zyada timeout unnecessarily long-running invocations ko allow kar sakta hai.

---

## 12. Lambda Layers

### Definition

Lambda Layer ek package hota hai jisme reusable libraries, dependencies ya doosra supporting content rakha ja sakta hai.

Iska purpose common dependencies ko multiple Lambda functions ke darmiyan reuse karna hai, taake har function mein same dependencies ko separately package karne ki zaroorat kam ho.

### Simple Example

Suppose 5 Lambda functions ek hi Python library use karte hain. Hum compatible Lambda Layer mein woh library package karke functions ke saath attach kar sakte hain.

### Real-World Example

Ek company ke multiple Lambda functions data processing ke liye common library use karte hain. Layer un functions ke liye dependency management ko asaan bana sakti hai.

### Benefits

* Common dependencies reuse hoti hain.
* Code organization improve hoti hai.
* Multiple functions mein dependency duplication kam ho sakti hai.

### Important Point

Layer mein maujood libraries function ke runtime aur architecture ke saath compatible honi chahiye.

---

## 13. Environment Variables

### Definition

Environment variables configuration values hoti hain jo function ke code se separate store ki ja sakti hain.

Inka use settings ko code mein hard-code kiye baghair configure karne ke liye hota hai.

### Simple Example

Suppose Lambda function ko S3 bucket ka naam chahiye. Hum bucket name ko environment variable mein store kar sakte hain.

### Python Example

```python
import os

def lambda_handler(event, context):
    bucket_name = os.environ.get("BUCKET_NAME")

    print(f"Configured bucket: {bucket_name}")

    return {
        "statusCode": 200,
        "body": "Configuration loaded"
    }
```

AWS Lambda configuration mein `BUCKET_NAME` environment variable define karna hoga.

### Benefits

* Configuration code se separate rehti hai.
* Different environments ke liye different values use ki ja sakti hain.
* Code ko baar baar edit kiye baghair settings change ki ja sakti hain.

### Security Note

Passwords, API keys aur doosre sensitive secrets ko plain-text environment variables mein rakhne se bachna chahiye. Sensitive information ke liye AWS Secrets Manager ya AWS Systems Manager Parameter Store jaisi services suitable configuration ke saath use ki ja sakti hain.

---

## 14. IAM Execution Role

### Definition

IAM Execution Role ek IAM role hai jo Lambda function ko AWS resources par specific actions perform karne ki permission deta hai.

Jab Lambda ko kisi AWS service se interact karna hota hai, to execution role ki permissions decide karti hain ke function kin actions ko perform kar sakta hai.

### Simple Example

Agar Lambda function ko S3 bucket se object read karna hai, to uski execution role mein required S3 read permission honi chahiye.

Agar required permission nahi hogi, to request access-denied error de sakti hai.

### Real-World Example

Ek company ka Lambda function uploaded files ko process karta hai. Function ko sirf required S3 bucket se files read karne ki permission di ja sakti hai.

Usay tamam S3 buckets access karne ki permission dena zaroori nahi.

### Least Privilege Principle

Least Privilege ka matlab hai user, role ya service ko sirf utni permissions dena jitni uske task ke liye zaroori hon.

### Best Practices

* Har function ko suitable execution role dein.
* Unnecessary permissions attach na karein.
* Resource-specific policies use karein jahan possible ho.
* Function ke access ko regular review karein.
* IAM permissions ko test aur monitor karein.

---

## 15. CloudWatch Logs and Monitoring

### Definition

Amazon CloudWatch AWS ki monitoring service hai jo supported AWS resources aur applications ke metrics, logs aur alarms ko monitor karne mein madad karti hai.

Lambda function ki execution details aur application ke log messages ko CloudWatch Logs mein inspect kiya ja sakta hai, jab required permissions aur logging setup available ho.

### Simple Example

```python
def lambda_handler(event, context):
    print("Lambda function started")

    return {
        "statusCode": 200,
        "body": "Success"
    }
```

Execution ke baad `Lambda function started` message ko CloudWatch Logs mein dekha ja sakta hai.

### CloudWatch se Kya Monitor Kar Sakte Hain?

* Function invocations.
* Function errors.
* Execution duration.
* Throttles.
* Logs aur configured alarms.

### Real-World Example

Agar S3-triggered Lambda function file upload ke baad error de raha hai, to CloudWatch Logs mein error message inspect karke troubleshooting start ki ja sakti hai.

### Important Note

CloudWatch Logs mein sensitive data, passwords, secret keys ya personal information unnecessarily log nahi karni chahiye.

---

## 16. Security Best Practices

AWS Lambda ko secure rakhne ke liye following practices important hain.

### 16.1 Least Privilege

Lambda execution role ko sirf required permissions dein.

### 16.2 Secure Secrets

Sensitive values ko securely manage karein. Secrets ko code mein hard-code na karein.

### 16.3 Input Validation

Event ya request se milne wale data ko process karne se pehle validate karein.

### 16.4 Logging

Errors aur useful execution details log karein, lekin secrets aur sensitive data log na karein.

### 16.5 Monitoring

Errors, duration aur throttling ko monitor karein. Zaroorat ke mutabiq CloudWatch alarms configure karein.

### 16.6 Resource Permissions

S3 aur doosri services ke resource policies ko review karein taake unnecessary access na mile.

### 16.7 Dependency Management

Libraries aur packages ko updated aur trusted sources se maintain karein.

### Real-World Example

Agar Lambda ko sirf ek specific S3 bucket se files read karni hain, to usay tamam S3 resources ke liye unrestricted access dene ke bajaye specific bucket aur required actions tak permissions limit karni chahiye.

---

## 17. AWS Lambda vs Amazon EC2

### What is Amazon EC2?

Amazon EC2 ka full form **Amazon Elastic Compute Cloud** hai.

EC2 AWS ki service hai jo virtual servers provide karti hai. User in servers par operating system aur applications configure aur run kar sakta hai.

EC2 mein user ko operating system updates, server configuration aur security settings jaise tasks ki responsibility leni par sakti hai.

### What is AWS Lambda?

AWS Lambda ek serverless compute service hai jo code ko events ke response mein execute karti hai. AWS underlying infrastructure ko manage karta hai, jabke user function code aur configuration par focus karta hai.

### Detailed Comparison

| Feature                   | AWS Lambda                                                  | Amazon EC2                                                                   |
| ------------------------- | ----------------------------------------------------------- | ---------------------------------------------------------------------------- |
| Service Type              | Serverless compute service                                  | Virtual server service                                                       |
| Infrastructure Management | AWS underlying infrastructure manage karta hai              | User ko operating system aur server configuration manage karni par sakti hai |
| Execution                 | Function invoke hone par code execute hota hai              | Application configured server par run kar sakti hai                          |
| Scaling                   | Supported workloads ke liye automatic scaling               | Manual ya configured automatic scaling                                       |
| Runtime Duration          | Har invocation ka maximum timeout 15 minutes hai            | Application server par longer-running processes chala sakti hai              |
| Operating System Access   | Traditional server jaisa full OS administration access nahi | Instance ke operating system ko manage kar sakte hain                        |
| Maintenance               | Infrastructure maintenance comparatively kam                | OS updates aur server maintenance ki responsibility ho sakti hai             |
| Billing Model             | Requests aur execution duration jaise factors par based     | Instance ke running time aur selected resources par based                    |
| Best For                  | Event-driven tasks, APIs aur background processing          | Websites, custom applications aur long-running workloads                     |
| Example                   | S3 file upload par function execute karna                   | Nginx ke zariye website host karna                                           |

### Example 1: AWS Lambda

Suppose user S3 bucket mein file upload karta hai.

S3 event Lambda function ko invoke karta hai. Function file ki information process karta hai aur logs generate karta hai.

Is task ke liye dedicated server ko manually maintain karna zaroori nahi.

### Example 2: Amazon EC2

Suppose hum ek website ko Nginx web server par host karna chahte hain.

Hum EC2 instance launch karte hain, Nginx install aur configure karte hain, website files upload karte hain aur security settings manage karte hain.

Website EC2 instance par host hoti hai.

### Real-World Scenario

Ek company apni main website EC2 par host kar sakti hai aur S3 par file upload hone ke baad automatic processing ke liye Lambda use kar sakti hai.

Is tarah dono services ek hi application mein mil kar kaam kar sakti hain.

### Which One Should We Choose?

**AWS Lambda choose karein jab:**

* Task event ke response mein execute hona ho.
* Server management kam rakhni ho.
* Workload ko function-based processing mein divide kiya ja sakta ho.
* Task Lambda ki execution limits ke andar complete ho sakta ho.

**Amazon EC2 choose karein jab:**

* Operating system par zyada control chahiye.
* Long-running application ya process run karna ho.
* Custom server configuration ki zaroorat ho.
* Application ko aise runtime ya workload ki zaroorat ho jo Lambda ki limits mein fit na hota ho.

---

## 18. Real-World Applications

### 18.1 File Processing

S3 bucket mein file upload hone par Lambda us file ke metadata ko process kar sakta hai ya doosra processing workflow start kar sakta hai.

### 18.2 API Backends

Amazon API Gateway ke saath Lambda use karke serverless APIs banayi ja sakti hain.

### 18.3 Notifications

Kisi event ke response mein Lambda notification bhejne ya notification workflow start karne mein madad kar sakta hai.

### 18.4 Scheduled Tasks

Amazon EventBridge ke scheduled events ke zariye Lambda function ko specified schedule par invoke kiya ja sakta hai.

### 18.5 Data Processing

Lambda incoming records ya events ko process karne aur unhein doosri services tak pohanchane mein madad kar sakta hai.

### 18.6 Security Automation

Security-related event receive hone par Lambda automated response workflow start kar sakta hai, jaise alert generate karna ya approved remediation process initiate karna.

**Important:** Security automation ke liye permissions aur actions ko carefully test karna chahiye, kyunki incorrect configuration legitimate resources ko affect kar sakti hai.

---

## 19. Advantages of AWS Lambda

### 19.1 Less Server Management

AWS infrastructure manage karta hai, is liye developer ko server maintenance par comparatively kam focus karna parta hai.

### 19.2 Automatic Scaling

Supported workloads ke liye Lambda incoming events aur requests ke mutabiq execution capacity scale kar sakta hai.

### 19.3 Event Integration

Lambda S3, API Gateway, EventBridge aur doosri supported services ke saath integrate ho sakta hai.

### 19.4 Usage-Based Billing

Billing requests, execution duration aur configured resources jaise factors par depend karti hai.

### 19.5 Faster Development

Developers infrastructure manage karne ke bajaye application logic aur business requirements par zyada focus kar sakte hain.

---

## 20. Limitations of AWS Lambda

### 20.1 Execution Timeout

Lambda invocation ka maximum duration 15 minutes hai. Is se zyada time lene wale tasks ke liye doosri architecture ya services consider karni chahiye.

### 20.2 Cold Starts

Kuch situations mein execution environment initialize karne ki wajah se additional latency aa sakti hai.

### 20.3 Limited Server Control

Lambda traditional virtual server jaisa full operating system administration access provide nahi karta.

### 20.4 Concurrency Limits

Account ya function ki concurrency limits hit hone par requests throttle ho sakti hain.

### 20.5 Dependency and Runtime Compatibility

Code, libraries aur runtime versions ko compatible rakhna zaroori hai.

### 20.6 Cost Depends on Usage

Lambda har workload ke liye automatically sab se cheap option nahi hota. High-volume ya continuously running workloads ke liye alternative compute services ka cost comparison karna chahiye.

---

## 21. Quick Revision

| Term                      | Roman Urdu Explanation                                                                 |
| ------------------------- | -------------------------------------------------------------------------------------- |
| AWS Lambda                | Serverless service jo code ko events ke response mein execute karti hai.               |
| Serverless Computing      | Aisa model jisme cloud provider underlying servers ko manage karta hai.                |
| Lambda Function           | Code ka unit jo ek specific task perform karta hai.                                    |
| Trigger                   | Event source ya mechanism jo function ko invoke karne ka process start karta hai.      |
| Event                     | Woh data jo function ko activity ke baare mein information deta hai.                   |
| Handler                   | Function ka entry point jahan se Lambda code ko call karta hai.                        |
| Runtime                   | Programming language code execute karne ka environment.                                |
| Execution Role            | IAM role jo Lambda ko required AWS permissions deta hai.                               |
| CloudWatch Logs           | Function execution ke log messages dekhne aur troubleshoot karne ka zariya.            |
| Event-Driven Architecture | Design jisme application components events ke response mein kaam karte hain.           |
| Synchronous Invocation    | Invocation jisme caller function ke response ka wait karta hai.                        |
| Asynchronous Invocation   | Invocation jisme caller ko function ke complete hone ka wait nahi karna parta.         |
| Concurrency               | Ek waqt mein chalne wali Lambda executions ki quantity.                                |
| Throttling                | Limits ki wajah se requests ka temporarily restrict hona.                              |
| Cold Start                | Naya execution environment initialize hone ki wajah se aane wala additional delay.     |
| Timeout                   | Function invocation ke liye configured maximum execution duration.                     |
| Lambda Layer              | Reusable dependencies ya libraries ka package.                                         |
| Environment Variables     | Code se separate rakhi gayi configuration values.                                      |
| Amazon EC2                | Virtual server service jo operating system aur application par zyada control deti hai. |

### Main Workflow

```text
Event Occurs
     |
     v
Trigger Invokes Lambda
     |
     v
Lambda Receives Event
     |
     v
Function Executes
     |
     v
Result / CloudWatch Logs
```

**Key Concept:** AWS Lambda event-driven code execution ke liye useful hai, jabke Amazon EC2 virtual server par applications run karne aur server configuration par zyada control ke liye useful hai.
