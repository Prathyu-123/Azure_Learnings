1️⃣ SSH into your Azure VM
ssh azureuser@{publicip}

2️⃣ Install Go on the VM

Check if Go is already there:

go version


If not installed:

sudo apt update
sudo apt install -y golang-go


Verify:

go version

3️⃣ Clone your Golang project
git clone https://github.com/Prathyu-123/devops-web-app.git
cd devops-web-app


Check files:

ls


Look for:

main.go

go.mod

4️⃣ Run the Golang app

First download dependencies:

go mod tidy


Run:

go run main.go


If successful, you’ll see something like:

Server started on port 8080


⚠️ Note the port number (very important).

5️⃣ Allow the app port in Azure (CRITICAL 🔥)

Suppose your app runs on 8080.

Azure Portal →

VM → Networking

Add inbound rule

Port: 8080

Protocol: TCP

Action: Allow

Without this, browser won’t open even if Go app is running.

6️⃣ Access your app in browser 🌍

Open:

http://{publicip}:8080


If you see your web page → 🎉 YOU DEPLOYED A GO APP ON AZURE VM

7️⃣ Run app in background (important)

If you close SSH, the app will stop.
Use nohup:

nohup go run main.go > app.log 2>&1 &


Check:

ps aux | grep go


Logs:

cat app.log

⭐ Better: Build binary (production style)

yayyy!!!!, application is running