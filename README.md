# 🖼️ Serverless Image Preprocessing with AWS

This repository contains the final project report for **Cloud Computing (2024/2025)** at **Sapienza Università di Roma**.

---

## 📘 Project Summary

The goal of this project is to implement a fully serverless, cloud-based image preprocessing pipeline using AWS services. The pipeline automatically triggers an image processing function whenever a new image is uploaded to Amazon S3. The images are converted to grayscale and resized using the Pillow library in Python, with the processed outputs stored in a separate S3 bucket.

This system is optimized for scalability, cost-efficiency, and real-time operation using a completely serverless architecture.

---

## 🚀 Key Features

- **📥 Automatic Triggering**: Uploading an image to the input S3 bucket triggers processing automatically.
- **🖼️ Image Processing**: Grayscale conversion and resizing to 256×256 using the Pillow library.
- **📤 Processed Output**: Results are saved to a separate S3 bucket.
- **⚙️ Serverless Design**: No servers or containers required—powered entirely by AWS Lambda.
- **📊 Monitoring**: CloudWatch tracks metrics like function duration, error rate, and concurrency.
- **🔐 Secure Access**: Managed through AWS IAM roles and permissions.

---

## 🧰 Technologies Used

| Technology        | Purpose                                                    |
|-------------------|------------------------------------------------------------|
| **AWS Lambda**     | Executes the image processing logic in response to uploads |
| **Amazon S3**      | Stores input and output images and triggers Lambda         |
| **Amazon CloudWatch** | Observability, metrics, and debugging                    |
| **AWS IAM**        | Secures access to S3 and Lambda                            |
| **Python + Pillow**| Performs image transformations                             |

---

## 🏗️ Architecture Diagram

```text
  [User Uploads Image]
           │
           ▼
┌────────────────────┐
│  Amazon S3 (Input) │
└────────────────────┘
           │
           ▼ (S3:ObjectCreated trigger)
┌────────────────────┐
│   AWS Lambda       │
│ - Convert to Gray  │
│ - Resize to 256x256│
└────────────────────┘
           │
           ▼
┌────────────────────┐
│ Amazon S3 (Output) │
└────────────────────┘
```


---

## ⚙️ Lambda Configuration

- **Runtime**: Python 3.12
- **Memory**: 128 MB
- **Timeout**: 3 seconds
- **Trigger**: `s3:ObjectCreated:*` event
- **Environment Variable**: `OUTPUT_BUCKET` specifies the output S3 bucket
- **Pillow Library**: Included via a Lambda Layer

---

## 📈 Performance Testing & Evaluation

Performance was evaluated under two scenarios:

### 1. Manual Upload Trigger

Images were uploaded manually via CLI or browser in batches of:
- 10
- 50
- 100
- 500
- 1000

### 2. High Rate Trigger

Simulated high-throughput uploads using a Python script to rapidly copy images into S3.

### Metrics Collected

- **Invocation Count**
- **Execution Duration**
- **Success Rate & Error Count**
- **Throttling Events**
- **Concurrent Executions**
- **Async Event Age**
- **Events Received/Dropped**

### Key Insights

- The system scaled efficiently with image volume and resolution.
- No throttling occurred, even under high-rate uploads.
- Execution duration increased with resolution but remained within acceptable limits.
- Brief cold start delays were observed and recovered quickly.
- Both trigger types demonstrated resilience and reliability.

---

## 🖼️ Sample Input & Output

| Resolution | Input (RGB)        | Output (Grayscale) |
|------------|--------------------|--------------------|
| Low        | 1200 x 800 pixels  | 256 x 256 pixels   |
| Mid        | 1500 x 997 pixels  | 256 x 256 pixels   |
| High       | 2040 x 1536 pixels | 256 x 256 pixels   |

---

## 📁 Supporting Materials

All graphs and performance metrics collected from CloudWatch are organized and available here:

📦 **[Google Drive – Metrics & Graphs](https://drive.google.com/drive/folders/190IXUecx4ZmLunxUyIfHdl-hzswfxg6B?usp=sharing)**

Includes:
- Manual Trigger graphs
- High-Rate Trigger graphs
- All image resolutions (Low, Mid, High)
- All batch sizes (10–1000)

---

## 🧾 Conclusion

This project successfully demonstrates the use of AWS services to build a serverless image preprocessing pipeline. The system is lightweight, scalable, and designed for real-time event-driven workloads. It offers:

- **No server management**
- **Automatic scaling**
- **Minimal cost (pay-per-use)**
- **Consistent performance across workloads**

This architecture can be extended to:
- Support additional image formats
- Integrate ML-based image classification
- Build a front-end with API Gateway for end users

---

## 👨‍💻 Authors

- **Beyza Nur Elaslan** (2180876)  
- **Marthe Elgawly** (2170201)  
- **Murad Hüseynov** (2181584)

📅 Final Project – Cloud Computing (2024/2025)  
🏛️ Sapienza Università di Roma

---

## 📬 Feedback & Contributions

This repository is academic, but feedback and forks are welcome for educational or extension purposes.
