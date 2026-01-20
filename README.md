# 🛡️ LifeSwitch: Escalating Wellness Check

A self-contained wellness monitoring system for **Home Assistant**. It monitors your daily activity via motion sensors. If you are inactive for a set number of days, it sends a notification to your phone. If you still don't respond, it automatically escalates to an emergency email for a loved one.

---

## 📋 Prerequisites
Before installing the blueprint, you need to set up two things: a **Helper** (to track time) and an **Email Service**.

### 1. Create the Last Activity Helper
This "Helper" acts like a clock that resets to zero every time you move or press the "I'm Okay" button.

1. Go to **Settings** > **Devices & Services** > **Helpers**.
2. Click **+ Create Helper** > **Date and/or time**.
3. **Name:** Wellness Last Activity.
4. **Icon:** `mdi:clock-check`.
5. **Type:** Select **Date and time**.
6. Click **Create**.

### 2. Set up the Email Service (SMTP)
Home Assistant needs a "Post Office" to send emails. Below is the setup for Gmail.

#### Step A: Get a Google App Password
1. Go to your **Google Account Security**.
2. Turn on **2-Step Verification**.
3. Search for **App Passwords**. Create one named "Home Assistant" and copy the 16-character code.

#### Step B: Add to Home Assistant
Open your `configuration.yaml` file. Paste the following (replacing with your details):

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

**Note:** Save and Restart Home Assistant.

> 💡 **Using other mail services?** If you don't use Gmail, check the [Official Home Assistant SMTP Documentation](https://www.home-assistant.io/integrations/smtp/) for settings like Outlook, iCloud, or Yahoo.

---

## 🚀 Installation & Setup

### 1. Import the Blueprint
1. Copy the `wellness_check.yaml` file from this repository to your Home Assistant folder: `/config/blueprints/automation/lifeswitch/`.
2. Go to **Settings** > **Automations & Scenes** > **Blueprints**.
3. Find **LifeSwitch: Wellness v3** and click **Create Automation**.

### 2. Fill in the Fields
The setup screen will ask for several inputs. Use these examples as a guide:

* **Motion Sensors:** Select all sensors that detect you being home (e.g., Living Room, Hallway).
* **Last Activity Helper:** Select the `input_datetime.wellness_last_activity` you created.
* **Notification Title:** `Wellness Check-In`
* **Notification Message:** `No activity detected for {{ days }} days. Tap here to view your dashboard or press the button below to reset.`
* **Dashboard Path:** `/dashboard-main/wellness` (The URL of your reset button).
* **Notification Service:** `notify.mobile_app_your_phone_name`
* **Email Notifier Service:** `notify.smtp_gmail`
* **Emergency Email Address:** `emergency_contact@example.com`

---

## 🛠️ Testing Your Setup
It is vital to test that your phone and email alerts actually work before relying on them.

### Step 1: Test the Email
1. Go to **Developer Tools** > **Actions**.
2. Search for **Notifications: Send a notification via smtp_gmail**.
3. Enter a test message and your email in the target field.
4. Click **Perform Action**. If you receive the email, your "Post Office" is working!

### Step 2: Test the Reset Button
1. Add the `input_datetime.wellness_last_activity` to your dashboard.
2. Create a button that calls the script or event `lifeswitch_reset`.
3. Press the button. The time on your dashboard helper should instantly update to the current time.

---

## 📖 How it Works (The Logic)
If you set **Days to Wait** to `3` and **Check Time** to `11:00:00`:

* **Day 3 at 11:00 AM:** If the helper shows no activity for 3 days, you get a **Phone Notification** with an "I'm Okay" button.
* **Day 4 at 11:00 AM:** If you still haven't moved or pressed the button, the **Emergency Email** is sent to your contact.
* **Resetting:** Any motion detected by your sensors or a press of the "I'm Okay" button resets the counter back to 0 days.
