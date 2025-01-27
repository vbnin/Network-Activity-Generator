# Network Activity Generator

**Bundle ID**: `com.vbnin.nag`  
**Supported platforms**: macOS 14+, iOS 15+, iPadOS 15+

**Distribution methods**: 
- On macOS, download the PKG from this Github repository and deploy it using an MDM solution.
- On iOS/iPadOS, this app **is not** publicly available. It is only available through App Store Connect in selected Apple Business Manager instances.

## Description

**Network Activity Generator (NAG)** is a versatile app designed to simulate network activity on test devices. It produces realistic network data, making it a useful tool for Mobile Device Management (MDM) demos, testing environments, and cybersecurity training.  

This app provides highly configurable network simulations, allowing users to define website categories, intervals, time-based scheduling, and other behavior to suit their specific requirements.  

## Features
- Simulates network activity across user-defined website categories: filtering websites, ZTNA websites, and threat websites.
- Fully configurable via MDM with support for AppConfig on iOS and managed configuration profiles on macOS.
- Supports scheduling to run activity simulations only during specific hours.
- Includes options to prevent device sleep (iOS), dim the screen (iOS), and launch at login (macOS) for a seamless demo experience.
- Customizable intervals and limits for the number of websites accessed per simulation run.

## Screenshots

<img width="723" alt="Screenshot 2025-01-27 at 10 59 12" src="https://github.com/user-attachments/assets/cd58a6ce-b7d3-4275-ac14-e92405013186" />
<img width="723" alt="Screenshot 2025-01-27 at 10 59 22" src="https://github.com/user-attachments/assets/21270066-56fc-4d6b-83e6-7367bd7e6715" />

---

## Deployment and Pre-Configuration Instructions

### Supported Configuration Keys

When deployed via MDM, the app supports the following configuration keys:

| Key                 | Type      | Description                                                                                     | Default Value when key isn't set|
|---------------------|-----------|-------------------------------------------------------------------------------------------------|----------------------|
| `filteringWebsites` | `string`  | Comma-separated list of websites for filtering/testing network activity.                       | `None`                 |
| `ZTNAWebsites`      | `string`  | Comma-separated list of Zero Trust Network Access websites for demos.                          | `None`                 |
| `threatWebsites`    | `string`  | Comma-separated list of threat websites for cybersecurity training and demos.                  | `None`                 |
| `scheduleInterval`  | `integer` | Interval (in minutes) between website accesses (`5`, `15`, `30`, `60`, or `120`).              | `5`                  |
| `websiteCount`      | `string`  | Number of websites to include per cycle (`5`, `10`, `15`, `20`, or `All`).                     | `All`                |
| `autorunAtLaunch`   | `boolean` | Whether the app automatically starts generating activity upon launch.                          | `false`              |
| `startTime`         | `integer` | Hour of the day (0-23) when activity generation begins.                                        | `0`                  |
| `stopTime`          | `integer` | Hour of the day (0-23) when activity generation stops.                                         | `23`                 |
| `preventSleep`      | `boolean` | Prevents the device from sleeping while the app is running. Only for iOS.                      | `false`              |
| `dimScreen`         | `boolean` | Whether to dim the screen during activity generation. Only for iOS.                            | `false`              |
| `startAtLogin`      | `boolean` | Whether the app launches automatically at login. Only for macOS.                               | `false`              |

---

### How to Pre-Configure the App

#### **iOS Deployment with AppConfig**

1. **Prepare the Configuration in MDM**  
   In your MDM solution (e.g., Jamf Pro), navigate to the AppConfig tab for the app `Network Activity Generator`.

2. **Set Configuration Keys**  
   Copy the XML configuration below and customize the values according to your requirements.
   
```
  <dict>
   <key>filteringWebsites</key>
   <string>https://example1.com,https://example2.com</string>
   <key>ZTNAWebsites</key>
   <string>https://example3.com,https://example4.com</string>
   <key>threatWebsites</key>
   <string>https://example5.com</string>
   <key>scheduleInterval</key>
   <integer>30</integer>
   <key>websiteCount</key>
   <string>10</string>
   <key>autorunAtLaunch</key>
   <true/>
   <key>startTime</key>
   <integer>9</integer>
   <key>stopTime</key>
   <integer>17</integer>
   <key>preventSleep</key>
   <true/>
   <key>dimScreen</key>
   <false/>
   <key>startAtLogin</key>
   <true/>
  </dict>
```

3. **Deploy the App**  
   Assign the app to your devices via your MDM using Volume Purchasing.

4. **Test the Configuration**  
   Once the app is installed, verify that the settings have been applied correctly by running the app.

---

#### **macOS Deployment with Managed Configuration Profiles**

1. **Create a Configuration Profile**  
   Create a configuration profile in your MDM solution (e.g.: Jamf Pro) and create a custom app configuration with the following XML for the bundle ID `com.vbnin.nag`:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
   <plist version="1.0">
   <dict>
       <key>PayloadType</key>
       <string>com.vbnin.nag</string>
       <key>PayloadVersion</key>
       <integer>1</integer>
       <key>PayloadUUID</key>
       <string>YOUR-UNIQUE-UUID-HERE</string>
       <key>PayloadDisplayName</key>
       <string>Network Activity Generator</string>
       <key>filteringWebsites</key>
       <string>https://example1.com,https://example2.com</string>
       <key>ZTNAWebsites</key>
       <string>https://example3.com,https://example4.com</string>
       <key>threatWebsites</key>
       <string>https://example5.com</string>
       <key>scheduleInterval</key>
       <integer>30</integer>
       <key>websiteCount</key>
       <string>10</string>
       <key>autorunAtLaunch</key>
       <true/>
       <key>startTime</key>
       <integer>9</integer>
       <key>stopTime</key>
       <integer>17</integer>
       <key>preventSleep</key>
       <true/>
       <key>dimScreen</key>
       <false/>
       <key>startAtLogin</key>
       <true/>
   </dict>
   </plist>
   ```

2. **Deploy the Profile**  
   Use your MDM to push the configuration profile to your managed macOS devices.

3. **Verify the App**  
   Deploy and launch the app. Check that the configurations are correctly applied.

---

For further assistance or feedback, feel free to open an issue in this repository. Happy testing!
