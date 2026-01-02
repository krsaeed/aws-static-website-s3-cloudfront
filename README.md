# 🌐 Static Website Hosting on AWS (S3 + CloudFront)

## 📌 Project Overview
This project demonstrates how to host a static website using **Amazon S3** and deliver it securely and efficiently using **Amazon CloudFront (CDN)**.  
The setup provides global content delivery, HTTPS support, and improved performance compared to using S3 alone.

---

## 🎯 Project Goals
- Host a static website using AWS S3
- Enable public access securely
- Distribute content globally using CloudFront
- Serve the website over HTTPS
- Understand real-world CDN behavior and troubleshooting

---

## 🛠️ Tech Stack
- **Amazon S3** – Static website hosting (origin)
- **Amazon CloudFront** – CDN & HTTPS
- **HTML / CSS**
- **AWS Console**

---

## 🏗️ Architecture

```

User (Browser)
|
v
CloudFront (HTTPS, CDN)
|
v
S3 Static Website Hosting

```

---

## 📁 Project Structure

```

static-site/
├── index.html
├── error.html
└── style.css

````

---

## 🚀 Step-by-Step Implementation

### 1️⃣ Create Static-site Website Files

---

### 2️⃣ Create S3 Bucket

1. Go to **AWS Console → S3**
2. Create a bucket with a unique name

   ```
   <your-bucket-name>
   ```
3. Choose a region
4. Disable **Block all public access**
5. Create the bucket

---

### 3️⃣ Enable Static Website Hosting

1. Open the bucket → **Properties**
2. Enable **Static website hosting**
3. Set:

   ```
   Index document: index.html
   Error document: error.html
   ```
4. Save changes

---

### 4️⃣ Upload Files to S3

Upload all files **at the root level** of the bucket:

* `index.html`
* `error.html`
* `style.css`

---

### 5️⃣ Configure Public Access (Bucket Policy)

Go to **Permissions → Bucket Policy** and add:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::<your-bucket-name>/*"
    }
  ]
}
```

---

### 6️⃣ Verify S3 Website

Open the **S3 Website Endpoint**:

```
http://<your-bucket-name>.s3-website-<region>.amazonaws.com
```

✅ Website should load with CSS applied.

---

## 🌍 CloudFront Integration

### 7️⃣ Create CloudFront Distribution

1. Go to **CloudFront → Create distribution**
2. Origin domain:

   ```
   <your-bucket-name>.s3-website-<region>.amazonaws.com
   ```
3. Origin protocol policy:

   ```
   HTTP only
   ```
4. Default root object:

   ```
   index.html
   ```
5. Viewer protocol policy:

   ```
   Redirect HTTP to HTTPS
   ```
6. Create distribution and wait for deployment

---

### 8️⃣ Access Website via CloudFront

After deployment, open:

```
https://<distribution-id>.cloudfront.net
```

✅ Website loads over HTTPS
✅ CSS and assets served via CDN

---

## 📸 Website Output

![Static Website Output](screenshots/website-output.png)

---

## 🔍 Key Learnings & Troubleshooting

* Use **relative paths** (`style.css`) instead of hardcoding S3 URLs
* CloudFront should serve **all assets**
* S3 Website Endpoints support **HTTP only**
* CloudFront provides **HTTPS termination**
* Correct MIME type (`text/css`) is required
* Cache invalidation may be needed after changes

---

## 📚 Skills Gained

* AWS S3 static website hosting
* CloudFront CDN configuration
* HTTPS enablement
* CDN caching behavior
* Real-world AWS troubleshooting
* Production-style architecture understanding

---

## 📈 Project Status

✔ S3 static website deployed
✔ CloudFront distribution configured
✔ HTTPS enabled
✔ Website accessible globally

---

## 🔜 Future Enhancements

* Custom domain using **Route53**
* Infrastructure as Code using **Terraform**
* CI/CD for static website using **GitHub Actions**
* Private S3 bucket with CloudFront Origin Access Control (OAC)

---

## 👤 Author

**Khalilur Rahman Saeed**
Learning DevOps step-by-step through real projects 🚀