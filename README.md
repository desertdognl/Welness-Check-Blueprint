# LifeSwitch: Wellness

## Description

The LifeSwitch Wellness blueprint is an automation blueprint that monitors activity via sensors and escalates to email if the user does not respond to mobile alerts.

## Installation

1. Copy the `wellness_check.yaml` file to your Home Assistant configuration directory.

2. Customize the input variables in the `wellness_check.yaml` file to fit your needs. You can find the input variables listed below.

## Input Variables

### Motion Sensors

- **Name**: Motion Sensors
- **Description**: Select sensors that detect daily activity. (Example: binary_sensor.living_room_motion)
- **Type**: Entity selector (multiple)

### Last Activity Helper

- **Name**: Last Activity Helper
- **Description**: Select the Input Datetime helper you created. (Example: input_datetime.wellness_last_activity)
- **Type**: Entity selector

### Days to Wait

- **Name**: Days to Wait
- **Description**: Days of inactivity allowed before alerting. (Example: 3)
- **Type**: Number
- **Default**: 3
- **Unit of Measurement**: days
- **Min**: 1
- **Max**: 14

### Daily Check Time

- **Name**: Daily Check Time
- **Description**: What time each day the check occurs. (Example: 11:00:00)
- **Type**: Time
- **Default**: 11:00:00

### Notification Title

- **Name**: Notification Title
- **Description**: Example: Wellness Check-In
- **Type**: Text

### Notification Message

- **Name**: Notification Message
- **Description**: Example: No activity detected for {{ days }} days. Tap here to view your dashboard or press the button below to reset.
- **Type**: Text (multiline)

### Dashboard Path

- **Name**: Dashboard Path
- **Description**: Example: /dashboard/check-in
- **Type**: Text

### Notification Service

- **Name**: Notification Service
- **Description**: Example: notify.mobile_app_phone
- **Type**: Text

### Emergency Email Address

- **Name**: Emergency Email Address
- **Description**: Example: your_emergency_contact@example.com
- **Type**: Text

## Usage

1. Configure the input variables in the `wellness_check.yaml` file to fit your needs.

2. Restart Home Assistant.

3. The blueprint will monitor activity via sensors and escalate to email if the user does not respond to mobile alerts.

## Troubleshooting

- If you are not receiving notifications, make sure that the motion sensors are working properly and that the input variables are correctly configured.

- If you are receiving notifications but they are not formatted correctly, make sure that the input variables are correctly configured and that the template syntax is correct.

- If you are not receiving emails, make sure that the email notifier service is correctly configured and that the emergency email address is correct.

## Contributing

Contributions are welcome! If you have any suggestions, bug reports, or feature requests, please open an issue on the repository.

If you would like to contribute code, please fork the repository and submit a pull request.


## 📜 License
MIT License - feel free to use and modify for your own projects.

[![Buy Me A Coffee](https://img.shields.io/badge/Buy%20Me%20a%20Coffee-ffdd00?style=for-the-badge&logo=buy-me-a-coffee&logoColor=black)](https://www.buymeacoffee.com/desertdog)
