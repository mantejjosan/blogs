# Host Your Site Directly From Your Phone! 🤯📱

Have you ever wanted to showcase a site directly from your phone? Now, you can do it! In this tutorial, we'll walk you through hosting a website on your mobile device using Termux, Flask, and Cloudflare, all without spending a dime. If you prefer using your laptop, check out the full tutorial [here]( {{< relref "QuickSelfHosting" >}} ).

> Yeah, this site is also live hosted from my mobile and will disappear once shutdown the server.

Let's dive into the steps for setting up your own server on a mobile device:

> Skip to Steps

---

## What Are We Trying to Achieve?

Whether you're working on a personal project, want to test a website, or simply showcase your work to friends or clients, this guide will help you make your local site accessible on the internet straight from your mobile device! 🚀

---

## Steps

We'll be using Termux for this tutorial, which makes it possible to run a local server on your mobile device. If you need a laptop version, be sure to check this tutorial here.

### 1. Install Termux

First, download and install Termux from the Google Play Store or F-Droid. Termux is a powerful terminal emulator and Linux environment for Android.

---

### 2. Grant Storage Permissions

Once installed, open Termux and grant it storage permissions to access files on your phone. You can do this by running:

```bash
termux-setup-storage
```

This command allows Termux to interact with the files on your device.

---

### 3. Update Termux Packages

To ensure everything is up to date, run the following commands to update your Termux environment:

```bash
pkg update && pkg upgrade
```

This will make sure that you have the latest packages available for installation.

---

### 4. Install Python and Pip

Now, we need to install Python and Pip, which are required to run Flask. Run the following commands:

```bash
pkg install python
pkg install python-pip
```

---

### 5. Install Flask

Now that Python is installed, you can install Flask, a lightweight web framework, by running:

```bash
pip install flask
```

---

### 6. Create a Flask Server

Once Flask is installed, you can create a simple Flask app. Let's make a basic server just like the laptop version. Create a directory and a Flask app script:

```bash
mkdir flask_app
cd flask_app
vim app.py
```

Inside `app.py`, paste the following code:

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return "Hello, World! Welcome to my mobile-hosted site."

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=5000)
```

---

### 7. Set Up Cloudflare Tunnel

To make your local server accessible online, we'll use Cloudflare Tunnel. Here's how you do it:

#### 7.1 Create a Cloudflare Account

Sign up for a free account at Cloudflare.

---

#### 7.2 Install Cloudflared

To install the cloudflared tool for setting up the tunnel, run the following:

```bash
pkg install cloudflared
```

---

#### 7.3 Start the Cloudflare Tunnel

Once cloudflared is installed, run the following command to expose your Flask server to the internet. Replace http://127.0.0.1:5000 with the URL of your Flask app:

```bash
cloudflared tunnel --url http://127.0.0.1:5000
```

Cloudflare will give you a public URL ending with .trycloudflare.com. This is the link you can share with your friends or teammates for easy access to your website.

---

### Bonus Tip: Use a Script for Automation

You can automate the process of starting both the Flask server and the Cloudflare tunnel with this handy script. Create a file called `host.sh`:

```bash
#!/bin/bash

# Start Flask server in debug mode in the background and save its process ID
FLASK_PORT=5000  # Replace with your Flask server port if different
export FLASK_ENV=development  # Enable Flask debug mode
FLASK_CMD="flask run --host=0.0.0.0 --port=$FLASK_PORT"
$FLASK_CMD > flask.log 2>&1 &
FLASK_PID=$!

echo "Starting Flask server in debug mode..."
sleep 5

# Extract the Flask server URL
FLASK_URL="http://127.0.0.1:$FLASK_PORT"
echo "Flask server running at: $FLASK_URL"

# Start Cloudflare tunnel and log its output
CLOUDFLARE_LOG="cloudflared.log"
CLOUDFLARE_CMD="cloudflared tunnel --url $FLASK_URL"
echo "Starting Cloudflare tunnel..."
$CLOUDFLARE_CMD > $CLOUDFLARE_LOG 2>&1 &
CLOUDFLARE_PID=$!

# Wait for Cloudflare tunnel to start
sleep 10

# Extract the Cloudflare tunnel link specifically ending with .trycloudflare.com
CLOUDFLARE_LINK=$(grep -o "https://[a-zA-Z0-9.-]*\.trycloudflare\.com" $CLOUDFLARE_LOG | head -n 1)

# Display the Cloudflare tunnel link
if [[ -n $CLOUDFLARE_LINK ]]; then
    echo "Cloudflare Tunnel Link: $CLOUDFLARE_LINK"
else
    echo "Failed to retrieve Cloudflare tunnel link. Check the log at $CLOUDFLARE_LOG for details."
fi

# Clean up on exit
cleanup() {
    echo "Stopping servers..."
    kill $FLASK_PID $CLOUDFLARE_PID
    echo "Servers stopped."
}
trap cleanup EXIT

# Keep the script running to hold the background processes
wait
```

---

## Congratulations! 🎉

You've now successfully hosted your website online directly from your mobile device! Share the Cloudflare link with anyone you want to showcase your project to. Whether it's for quick feedback, testing, or showcasing to friends and clients, you now have a mobile web server at your fingertips.

For a more detailed version of this tutorial, visit our laptop-based tutorial here.

Happy Hosting! 🌐


