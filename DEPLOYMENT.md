# Amudi Foods — Production Deployment & Operations Guide

## 📌 Architecture Overview

The Amudi Foods B2B platform consists of:
- **Buyer Order Portal (`index.html`)**: Mobile-first single-page web app for registered buyers.
- **Admin Operations Portal (`admin.html`)**: Desktop-optimized portal for managing catalog, buyers, and orders.
- **Backend API (`apps-script/Code.gs`)**: Google Apps Script Web App integrated with Google Sheets and Gmail.

Both portal files are **100% self-contained** (all styles, scripts, and API clients embedded) for instant, zero-configuration hosting on **GitHub Pages**.

---

## 🚀 Live Production Configuration

- **Google Apps Script Web App URL:**  
  `https://script.google.com/macros/s/AKfycbz8d4H2_2SWA0V6HJsZD0B5OBjDu7tNmR7Tbpg_yKL-IhWuuYhi5WK3DpzV-GKUK0zi/exec`
- **Google Sheet ID (Orders DB):**  
  `14htQ-b0rYEPyIYR1nBRKohIOdI_-Qfx0Oiwuhniwam8`
- **Internal Team Alert Email:**  
  `orders@amudifoods.com.np`
- **Email Sender Display Name:**  
  `"Amudi Foods"`

---

## ⚙️ Step 1: Deploy / Update Google Apps Script Backend

Whenever you modify `apps-script/Code.gs`:

1. Open your Google Sheet (`14htQ-b0rYEPyIYR1nBRKohIOdI_-Qfx0Oiwuhniwam8`).
2. Go to **Extensions > Apps Script**.
3. Copy and paste the updated contents of [`apps-script/Code.gs`](./apps-script/Code.gs) into your script editor.
4. If setting up for the first time:
   - Run the function `setupInitialData` from the function dropdown to seed initial categories, sample products, custom questions, and your admin user.
5. **Publish a New Version (Crucial)**:
   - Click **Deploy > Manage deployments**.
   - Click the **Pencil (Edit)** icon on your active deployment.
   - Set **Version** to **New version**.
   - Ensure **Execute as** is set to `Me` and **Who has access** is set to `Anyone`.
   - Click **Deploy**.

---

## 🌐 Step 2: Host Static Frontend on GitHub Pages

1. Initialize and push this repository to GitHub:
   ```bash
   git init
   git add .
   git commit -m "Deploy Amudi Foods B2B Production Portal"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
   git push -u origin main
   ```

2. In your GitHub repository:
   - Go to **Settings > Pages** (in the left sidebar).
   - Under **Build and deployment > Source**, select **Deploy from a branch**.
   - Under **Branch**, select `main` (or `master`) and folder `/ (root)`.
   - Click **Save**.

3. Your URLs will be live in ~60 seconds:
   - **Buyer Order Portal:** `https://<YOUR_USERNAME>.github.io/<YOUR_REPOSITORY>/`
   - **Admin Operations Portal:** `https://<YOUR_USERNAME>.github.io/<YOUR_REPOSITORY>/admin.html`

---

## 🔒 Security & Admin Account

- **Default Admin Username:** `admin@amudifoods.com.np`
- **Initial Password:** Set inside `CONFIG.ADMIN_PASSWORD` in `Code.gs` (update as needed in Apps Script).
- **Buyer Accounts:** Buyers cannot self-register. The admin provisions buyer accounts from `admin.html`, which automatically generates secure passwords and emails them via Gmail.
