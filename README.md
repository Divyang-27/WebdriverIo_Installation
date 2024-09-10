# WebdriverIo_Installation

WebDriverIO Mobile App Testing Setup
Prerequisites
Node.js and npm

Download and install Node.js, which includes npm (Node Package Manager).
Visual Studio Code

Install Visual Studio Code for the development environment.
Android Studio

Download and install Android Studio for setting up an Android emulator.
Java Development Kit (JDK)

Download and install the JDK (version 8 or higher).
Step-by-Step Configuration
Windows OS
1. Install Android Studio and Set Environment Variables
Download and Install Android Studio

Download Android Studio from the official site and install it.
Open Android Studio and set the SDK path in SDK Manager to C:\Users\<YourUserName>\AppData\Local\Android\Sdk.
Set Environment Variables

Open Control Panel → System → Advanced System Settings → Environment Variables.
Create a new System Variable:
Variable Name: ANDROID_HOME
Variable Value: C:\Users\<YourUserName>\AppData\Local\Android\Sdk
Add the following paths to the Path variable:
%ANDROID_HOME%\platform-tools
%ANDROID_HOME%\emulator
2. Create and Run an Android Emulator
Create a Virtual Device

Open Android Studio and go to the AVD Manager: Click on Configure (+) > Device Manager.
Select Create Virtual Device.
Choose Pixel 8a and select Oreo API Level 26.
Start the Emulator

Open Command Prompt and navigate to the emulator directory:
bash
Copy code
cd C:\Users\<YourUserName>\AppData\Local\Android\Sdk\emulator
Start the emulator:
bash
Copy code
emulator -avd <Your_Emulator_Name>
3. Install Node.js and Appium
Install Node.js

Download and install Node.js from nodejs.org. Verify installation:
bash
Copy code
node -v
npm -v
Install Appium

Install Appium globally:
bash
Copy code
npm install -g appium@next
Install Appium Doctor

Install Appium Doctor:
bash
Copy code
npm install -g appium-doctor
Optionally, run Appium Doctor to verify setup:
bash
Copy code
appium-doctor --android
4. Setup WebdriverIO in Visual Studio Code
Open Visual Studio Code

Create a new project folder and open it in VS Code.
Install WebDriverIO and Appium

Run the following command:
bash
Copy code
npx wdio config
Follow the prompts:
Type of testing: E2E Testing - Web or Mobile Applications.
Automation Backend: On my local machine.
Environment to automate: Mobile - Native, Hybrid, and Web Apps.
Mobile Environment: Android.
Automation Framework: Mocha.
Add services: Appium.
5. Emulator and APK Setup
Create a Batch File for Emulator

Create a .bat file to start your emulator (e.g., Shiva.bat):
batch
Copy code
cd C:\Users\<YourUserName>\AppData\Local\Android\Sdk\emulator
emulator -avd <Your_Emulator_Name>
Install APK on Emulator

Copy your APK file to C:\Users\<YourUserName>\AppData\Local\Android\Sdk\platform-tools.
Open Command Prompt from this directory and run:
bash
Copy code
adb install <name_of_apk.apk>
6. Configure WebDriverIO for Mobile Testing
Update WebDriverIO Configuration

In wdio.conf.js, update the capabilities section:
javascript
Copy code
const path = require('path');

exports.config = {
  // Include this line in specs
  specs: [
    './test/specs/**/*.js'
  ],

  capabilities: [{
    'appium:platformName': 'Android',
    'appium:deviceName': 'Shiva_Pixel',
    'appium:automationName': 'UiAutomator2',
    'appium:noReset': true,
    'appium:app': path.join(process.cwd(), "/app/android/YourApp.apk")
  }],
  
  services: [
    ['appium', {
      command: 'appium',
    }]
  ]
};
Update package.json

Add the following script:

"scripts": {
  "wdio": "wdio run ./wdio.conf.js"
}
7. Create Test Files
Create Test Folder Structure
Inside webdriverio-appium-v8, create the following folder structure:

test/
└── specs/
    └── example.test.js
8. Running Tests
Run Tests
In the VS Code terminal, run:
npx wdio wdio.conf.js
9. Using Appium Inspector
Download and Install Appium Inspector

Search for "Appium Inspector download" and install the .exe file.
Configure and Start a Session

Launch Appium Inspector and configure it:
Platform Name: Android
Device Name: Shiva_Pixel
App Package: (Get this from the APK info app)
App Activity: (Choose from the available activities)
Automation Name: UiAutomator2
Save and start the session.
