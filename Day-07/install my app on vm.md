# 🚀 Deploying a Golang Application on an Azure VM

This guide walks through deploying a simple Golang web application on an Azure Virtual Machine. It’s written to be beginner-friendly while still following good DevOps practices.

---

## 🧩 Prerequisites

* An Azure account
* An Azure VM (Ubuntu recommended) with a **public IP**
* SSH access to the VM
* Your Golang project hosted on GitHub

---

## 1️⃣ Connect to Your Azure VM

From your local terminal, connect to the VM using SSH:

```bash
ssh azureuser@<public-ip>
```

Once connected, you are inside the Azure VM.

---

## 2️⃣ Install Golang on the VM

### Check if Go is already installed

```bash
go version
```

### Install Go (if not present)

```bash
sudo apt update
sudo apt install -y golang-go
```

### Verify installation

```bash
go version
```

---

## 3️⃣ Clone Your Golang Project

Clone the GitHub repository containing your Golang application:

```bash
git clone https://github.com/Prathyu-123/devops-web-app.git
cd devops-web-app
```

Verify the project structure:

```bash
ls
```

You should see key files such as:

* `main.go`
* `go.mod`

---

## 4️⃣ Run the Golang Application

### Download dependencies

```bash
go mod tidy
```

### Start the application

```bash
go run main.go
```

If successful, you will see output similar to:

```
Server running on http://0.0.0.0:8080
```

📌 **Note the port number (8080)** — this is critical for networking configuration.

---

## 5️⃣ Allow Application Port in Azure (CRITICAL)

By default, Azure blocks inbound traffic. You must explicitly allow your app port.

### Steps in Azure Portal

1. Go to **Azure Portal → Virtual Machines**
2. Select your VM
3. Navigate to **Networking**
4. Add an **Inbound port rule**:

   * **Port**: `8080`
   * **Protocol**: `TCP`
   * **Action**: `Allow`

Without this step, the application will run but won’t be accessible from the browser.

---

## 6️⃣ Access the Application from Browser 🌍

Open a browser on your local machine and visit:

```
http://<public-ip>:8080
```

If the page loads correctly:

🎉 **Congratulations! Your Golang application is live on Azure VM.**

---

## 7️⃣ Run the Application in Background

If you close the SSH session, the app will stop unless it runs in the background.

### Use `nohup` to keep it running

```bash
nohup go run main.go > app.log 2>&1 &
```

### Verify the process

```bash
ps aux | grep go
```

### View logs

```bash
cat app.log
```

---

## ⭐ Production-Style Improvement: Build a Binary

Instead of `go run`, build and execute a binary for better performance:

```bash
go build -o webapp
nohup ./webapp > app.log 2>&1 &
```

This approach is faster, cleaner, and closer to real-world production setups.

---

## ✅ Final Outcome

* Golang app successfully deployed on Azure VM
* Application accessible via public IP
* App running persistently in the background

✨ **Yayyy! Your application is running successfully.**
