# AWS-Session

### 1. **Launch EC2 Instance**
- **Go to AWS Console** → EC2 Dashboard → Launch Instance.
- **Choose Amazon Linux 2** (or Ubuntu).
- **Select t2.micro** (free-tier eligible).
- **Configure Security Group** to allow:
  - **SSH (Port 22)** for access.
  - **HTTP (Port 80)** for web traffic.
- **Launch Instance** and **Download the Key Pair**.

### 2. **Connect to EC2**
- Use the downloaded key to SSH into your EC2 instance:
  ```bash
  ssh -i /path/to/key.pem ec2-user@<EC2_PUBLIC_IP>
  ```

### 3. **Set Up Environment**
- **Update packages**:
  ```bash
  sudo yum update -y   # Amazon Linux
  ```
- **Install Node.js**:
  ```bash
  curl -sL https://rpm.nodesource.com/setup_16.x | sudo bash -
  sudo yum install -y nodejs
  ```

### 4. **Deploy Node.js App**
- **Clone your app** (if in GitHub):
  ```bash
  git clone https://github.com/your-username/your-app.git
  cd your-app
  ```
- **Install dependencies**:
  ```bash
  npm install
  ```

### 5. **Run the App**
- Start your Node.js app:
  ```bash
  node app.js
  ```
- Ensure your app listens on **Port 80** (use `iptables` if needed to redirect traffic):
  ```bash
  sudo iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 3000
  ```

### 6. **Access Your App**
- Visit your EC2 instance’s **public IP** in the browser:
  ```
  http://<EC2_PUBLIC_IP>
  ```

---

This should get your Node.js app running on an EC2 instance quickly!
