# Host Your Site Without Spending A Buck! 🤯
 
Today, you’ll learn how to set up your site on the internet without spending a penny! You can use your phone or laptop as a hosting service by setting up a local server using Flask and exposing it to the internet with Cloudflare and the Cloudflare daemon.

> [Skip to Steps](#steps)

---

## What We Are Trying to Achieve

Ever designed a frontend that you desperately want to showcase to your friends, teammates, or clients for quick feedback? Or perhaps you want to test your website’s vulnerabilities to enhance its security? No matter your goal, this guide will show you how to make your local project accessible online in minutes.

---

## Steps

These steps focus on Linux, but there are alternatives available for Windows as well. If you're using a phone, check out [this tutorial for mobile]({{< relref "SelfHostingWithMobile.md" >}}).

---

### 1. Create a Site

Start by creating the project or site you want to showcase. It could be a blog, portfolio, or even a simple Markdown file converted into HTML. 

Need help with Markdown? [Check out this guide](link-to-markdowntohtml.html).

---

### 2. Set Up a Local Server

To share your website, you’ll need a local server. Think of it like sharing an image via AirDrop or WhatsApp: the server hosts your files, and users can access them by requesting the files from the server.

**Ways to Set Up a Local Server:**
- **Using VSCode/Code Editor**: Use the built-in "Live Server" extension.
- **Manual Setup**: Use frameworks like Flask or Express.js.

For simplicity, we’ll use Flask here (works for both laptops and phones).

#### Steps to Set Up Flask:

1. Open your terminal or PowerShell.
2. Install Flask using pip:
   ```bash
   pip install flask
   ```
3. Create the necessary directories:
```bash
mkdir server templates
```

4. Create a Flask app:
```bash
vim app.py
```
Paste the following code:
```python
from flask import Flask, render_template

app = Flask(__name__)

@app.route("/")
def home():
    return render_template("index.html")

if __name__ == "__main__":
    app.run()

```

5. Place your index.html inside the templates folder. To serve a custom page, modify the render_template line above.


6. Run your server:
```bash
flask run
```

For real-time updates during development, use:
```bash
flask run --debug
```

For now, stop the server after confirming it works. We’ll restart it after setting up the Cloudflare tunnel.




---

3. Create a Cloudflare Tunnel

To make your local server accessible over the internet, we’ll use Cloudflare tunnels. This ensures a secure connection without needing to configure port forwarding or deal with NAT traversal.

Steps:

1. Create a Cloudflare Account: Sign up for a free account on Cloudflare.


2. Install Cloudflared:

- For Windows: Follow the official guide.

- For Ubuntu/Debian-based systems:
```bash
wget https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb
sudo dpkg -i cloudflared-linux-amd64.deb
```

- For Arch-based systems:
```
yay -S cloudflared

```

3. Create a Tunnel: Run the following command, replacing <server-url> with the URL of your running Flask or live server:

```bash
cloudflared tunnel --url <server-url>

```

4. Restart your Flask server:
```bash
flask run

```


---

Bonus Tip: Automate the Process

Running two servers (Flask and Cloudflare) in separate terminals can be tedious. Use the following script to simplify the process:

1. Create a script called host.sh:
```bash
#!/bin/bash
flask run &
cloudflared tunnel --url http://127.0.0.1:5000

```

2. Make it executable:
```bash
chmod +x host.sh
```

3. Run the script:
```bash
./host.sh

```

This will start both servers simultaneously.


---

Congratulations! You’ve successfully hosted your local site online. Now, share the Cloudflare-provided link with your friends, teammates, or clients for quick access.

Happy hosting! 🚀



