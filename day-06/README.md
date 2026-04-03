# Day-6: VPC Networking – Subnets and Firewalls

# 🌐 What is a VPC in GCP?

A VPC (Virtual Private Cloud) in Google Cloud Platform is:

- 👉 A private network inside Google’s cloud  
- 👉 Where you run your servers, apps, and databases securely  

---

## 🧠 Simple Analogy

Think of a VPC like:

🏢 **Your Company Office Building**

- VPC = Entire building  
- Subnets = Different rooms/floors  
- Servers = Employees working inside  
- Firewall = Security guard  
- Router = Directions for movement  
- NAT = Receptionist handling outside calls  

---

## 📦 Core Components

### 1️⃣ VPC = Isolated Network (CIDR)

Defined using CIDR range  
Example:
```bash
172.16.0.0/16
```


👉 This means:

- You get **65,536 IP addresses**  
- Fully private network  

✔️ No one outside can access it unless you allow  

---

### 2️⃣ Subnets (Public & Private)

Inside VPC → you create subnets  

#### 🔹 Public Subnet
- Has access to internet  
- Example: Web server  

#### 🔹 Private Subnet
- No direct internet access  
- Example: Database (more secure)  

👉 From diagram:
- App → Public  
- DB → Private ✅  

---

### 3️⃣ IP Addressing

Every VM (server) gets:

- Internal IP → inside VPC  
- External IP → optional (for internet access)  

---

### 4️⃣ Router & Route Table

📍 Router decides:  
👉 “Where should this traffic go?”

Example routes:

- Internal traffic → stay inside VPC  
- Internet traffic → go via Internet Gateway  

---

### 5️⃣ Internet Gateway (IGW)

👉 Allows communication with internet  

✔️ Needed for:

- Websites  
- APIs  
- Public apps  

---

### 6️⃣ Firewall Rules 🔥

Controls:

- Who can access what  
- Which ports allowed  

Example:

- Allow HTTP → Port 80  
- Allow HTTPS → Port 443  
- Block everything else  

---

### 7️⃣ NAT (Network Address Translation)

Used for private subnet  

👉 Problem:  
Private servers can’t access internet  

👉 Solution:  
Use NAT  

✔️ Allows:

- DB server → download updates  
- But still **no incoming access**  

---

### 8️⃣ VPN (Optional)

👉 Connect your local system/company network → VPC  

Example:

- Your laptop → securely connect to cloud DB  

---

## 🧩 Real-World Architecture Example

### 🛒 Example: E-commerce App (like Amazon)

### Step 1: Create VPC
```bash
VPC: 172.16.0.0/16
```


---

### Step 2: Create Subnets

- Public Subnet → 172.16.1.0/24  
- Private Subnet → 172.16.2.0/24  

---

### Step 3: Deploy Components

#### 🌍 Public Subnet
- Web Server (Frontend)  
- Load Balancer  

👉 Users access:
```bash
www.example.com
```

---

#### 🔒 Private Subnet
- Database (MySQL/PostgreSQL)  
- Backend services  

👉 Not accessible from internet  

---

## 🔁 Flow of Request

1. User → Website  
2. Request → Load Balancer  
3. Load Balancer → App Server  
4. App Server → Database (private subnet)  
5. Response → User  

---

## 🔐 Security Flow

- Firewall allows:
  - HTTP/HTTPS → Web server  
  - DB access → only from app server  

✔️ DB is completely hidden  

---

## 🔥 Interview-Ready Summary

👉 **VPC in GCP = Private isolated network**

It provides:

- IP addressing (CIDR)  
- Subnets (public/private)  
- Routing  
- Firewall security  
- Internet/NAT access  

---

## ⚡ Key Takeaways

✔ VPC is isolated  
✔ Subnets divide network  
✔ Public vs Private separation  
✔ Router controls traffic  
✔ Firewall controls security  
✔ NAT enables private internet access  
✔ VPN connects external networks  

---

## 🚀 Final Simple Line

👉 **“VPC is like a secure private network in the cloud where you control traffic, security, and communication between your resources.”**
