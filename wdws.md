### **Steps to Install IIS**

1. **Open Server Manager**:  
   - Click the **Start** button, then open **Server Manager**.

2. **Add IIS Role**:  
   - Go to **Manage** > **Add Roles and Features**.  
   - Select **Role-based or feature-based installation** and click **Next**.

3. **Select Web Server (IIS)**:  
   - In the "Roles" section, check **Web Server (IIS)**.
   - Confirm any additional features required by IIS and click **Next**.

4. **Complete the Installation**:  
   - Follow the prompts and click **Install**.  
   - Wait until the installation completes.

---

### **Verify IIS Installation**  

- Open your browser and navigate to:  
   `http://localhost`  

   You should see the **IIS Default Welcome Page**, confirming that IIS is installed and running.


  Here is a **brief step-by-step guide** to expose your Node.js app on port `3000` using **IIS**:

---

### **1. Install URL Rewrite and ARR Modules**
- Download and install:
   - [**URL Rewrite**](https://www.iis.net/downloads/microsoft/url-rewrite)
   - [**Application Request Routing (ARR)**](https://www.iis.net/downloads/microsoft/application-request-routing).

---

### **2. Enable Reverse Proxy in IIS**
- Open **IIS Manager**.
- Click on your **server name**.
- Double-click on **Application Request Routing Cache**.
- On the right pane, select **Server Proxy Settings** → Check **Enable proxy** → Apply.

---

### **3. Create Reverse Proxy Rule**
1. Select your **IIS website** (e.g., "Default Web Site").
2. Double-click **URL Rewrite**.
3. Click **Add Rules** → Select **Reverse Proxy**.
4. In the destination box, enter your Node.js app:  
   `http://localhost:3000`
5. Apply the rule.

---

### **4. Verify Port Bindings**
- Go to your site's bindings and ensure it's listening on port `80` or `443`.
- For HTTPS (443), ensure you have an SSL certificate.

---

### **5. Test Your App**
- Access your server’s public IP or domain:
   - **HTTP**: `http://your-server-ip`
   - **HTTPS**: `https://your-server-ip`  

---

This setup will forward traffic from IIS (port 80/443) to your Node.js app on port `3000`. 🚀

