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


<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <rule name="SPA Fallback" stopProcessing="true">
          <match url=".*" />
          <conditions logicalGrouping="MatchAll">
            <!-- don’t rewrite if the request is for an actual file -->
            <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="true" />
            <!-- don’t rewrite if it’s for a real directory -->
            <add input="{REQUEST_FILENAME}" matchType="IsDirectory" negate="true" />
            <!-- (optional) don’t rewrite API calls -->
            <add input="{REQUEST_URI}" pattern="^/api" negate="true" />
          </conditions>
          <!-- rewrite everything else to index.html -->
          <action type="Rewrite" url="/index.html" />
        </rule>
      </rules>
    </rewrite>
  </system.webServer>
</configuration>


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



If you want your Node.js app to be accessible at `http://<your-ip-address>/helloworld`, you can configure IIS to serve it under that specific path while keeping other apps on the same IP. Here's how:

---

### **Steps to Configure IIS for Subpath Access (`/helloworld`)**

#### **1. Use the Existing IIS Website**
Instead of creating a new site, add the Node.js app as a virtual directory or sub-application under your existing IIS website.

1. Open **IIS Manager**.
2. Navigate to your existing website (e.g., `Default Web Site`).
3. **Add a Virtual Directory**:
   - Right-click on the website and select **Add Virtual Directory**.
   - **Alias**: Enter `helloworld` (this is the path in the URL).
   - **Physical Path**: Set it to the folder where your Node.js app resides.
   - Click **OK**.

---

#### **2. Set Up Reverse Proxy for `/helloworld`**
1. Double-click **URL Rewrite** in the IIS site settings.
2. Add a new **Inbound Rule**:
   - Select **Blank Rule** and click **OK**.
3. Configure the rule:
   - **Condition**: Match requests starting with `/helloworld`.
     - Click **Add Conditions** → `{REQUEST_URI}` → Match Pattern: `^/helloworld`.
   - **Action**: Forward traffic to your Node.js app.
     - **Action Type**: Redirect or Rewrite.
     - **Rewrite URL**: `http://localhost:3000/{R:0}`.
     - Check **Append Query String**.

4. Save and Apply the Rule.

---

#### **3. Test Your Setup**
- Restart IIS (`iisreset`).
- Visit `http://<your-ip-address>/helloworld`. It should serve your Node.js app.

---



<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <rule name="Angular Routes" stopProcessing="true">
          <match url=".*" />
          <conditions>
            <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="true" />
            <add input="{REQUEST_FILENAME}" matchType="IsDirectory" negate="true" />
          </conditions>
          <action type="Rewrite" url="/index.html" />
        </rule>
      </rules>
    </rewrite>
  </system.webServer>
</configuration>

