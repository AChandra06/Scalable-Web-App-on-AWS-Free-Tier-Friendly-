# Scalable-Web-App-on-AWS-Free-Tier-Friendly-
Project Overview

This project demonstrates the design and deployment of a **highly available and scalable web application** on AWS using core cloud services. The system automatically distributes incoming traffic and scales resources based on demand.

---

Architecture

```
User → Application Load Balancer → Auto Scaling Group → EC2 Instances
```

---

Technologies & Services Used

* Amazon EC2 (Virtual Servers)
* Application Load Balancer (ALB)
* Auto Scaling Group (ASG)
* Target Groups
* Amazon Linux
* Apache Web Server

---

Implementation Steps
1️⃣ EC2 Setup

* Launched an EC2 instance using Amazon Linux (t2.micro)
* Configured security group to allow:

  * SSH (22)
  * HTTP (80)
* Connected via SSH using `.pem` key
* Installed Apache web server
* Deployed a simple web page displaying instance hostname

---

2️⃣ AMI Creation

* Created a custom AMI from the configured EC2 instance
* Used as a template for launching identical instances

---

3️⃣ Target Group Configuration

* Created a target group with HTTP protocol (port 80)
* Registered EC2 instance
* Configured health checks (`/` path)

---

4️⃣ Application Load Balancer

* Created an internet-facing ALB
* Configured listener on port 80
* Attached target group
* Enabled traffic distribution across instances

---

5️⃣ Launch Template

* Created launch template using:

  * Custom AMI
  * Instance type (t2.micro)
  * Security group
* Added user data script to auto-install Apache and deploy web page

---

6️⃣ Auto Scaling Group

* Configured ASG with:

  * Min: 1 instance
  * Desired: 2 instances
  * Max: 3 instances
* Attached to load balancer
* Enabled multi-AZ deployment

---

7️⃣ Scaling Policy

* Implemented target tracking policy based on CPU utilization
* Adjusted threshold to test scaling behavior

---

8️⃣ Testing & Validation

 ✅ Load Balancing

* Used `curl` to send multiple requests
* Verified responses from different EC2 instances

 ✅ Auto Scaling (Scale-Out)

* Simulated CPU load using:

  ```
  stress --cpu 2 --timeout 300
  ```
* Observed new instance launch

 ✅ Auto Scaling (Scale-In)

* Observed automatic termination of instances during low load

---

Key Features

* High availability using multiple availability zones
* Dynamic scaling based on system load
* Fault tolerance with health checks
* Cost optimization via automatic scale-in

---

Key Learnings

* Auto Scaling depends on **CPU utilization, not request count**
* Load balancing distributes traffic evenly across instances
* Scaling requires **sustained load**, not short bursts
* Infrastructure automation improves reliability and efficiency

---

Conclusion

Successfully built a **scalable and fault-tolerant web architecture** on AWS that dynamically adapts to workload demands while maintaining performance and cost efficiency.

---

Future Enhancements

* Add CloudWatch monitoring dashboard
* Deploy a full-stack application (Node.js/React)
* Enable HTTPS using SSL certificates
* Integrate CI/CD pipeline

---

