# 🛡️ LifeSwitch: Escalating Wellness Check

A self-contained wellness monitoring system for **Home Assistant**. It monitors your daily activity via motion sensors. If you are inactive for a set number of days, it sends a notification to your phone. If you still don't respond, it automatically escalates to an emergency email for a loved one.

---

## 📋 Prerequisites
Before installing the blueprint, you need to set up a **Helper** and an **Email Service**.

### 1. Create the Last Activity Helper
This acts as a timer that resets every time you move or check in.

1. Go to **Settings** > **Devices & Services** > **Helpers**.
2. Click **+ Create Helper** > **Date and/or time**.
3. **Name:** `Wellness Last Activity`
4. **Icon:** `mdi:clock-check`
5. **Type:** Select `Date and time`.
6. Click **Create**.

### 2. Set up the Email Service (SMTP)
Home Assistant needs an integration to send emails. Below is the setup for Gmail.

**Step A: Get a Google App Password**
* Go to your Google Account Security and turn on **2-Step Verification**.
* Search for **App Passwords**. Create one named "Home Assistant" and copy the 16-character code.

**Step B: Update Configuration**
Add this to your `configuration.yaml` file:

```yaml
notify:
  - name: smtp_gmail
    platform: smtp
    server: "smtp.gmail.com"
    port: 587
    timeout: 15
    sender: "your-email@gmail.com"
    encryption: starttls
    username: "your-email@gmail.com"
    password: "xxxx xxxx xxxx xxxx" # Your 16-character App Password
    recipient: "your-email@gmail.com"
