Sure! Here’s a structured GitHub-level documentation for setting up WebDriverIO mobile app testing on both Windows and macOS, including Java Development Kit (JDK) installation.

---

# WebDriverIO Mobile App Testing Setup

## Prerequisites

1. **Node.js and npm**
   - Download and install [Node.js](https://nodejs.org/), which includes npm (Node Package Manager).

2. **Visual Studio Code**
   - Install [Visual Studio Code](https://code.visualstudio.com/) for the development environment.

3. **Android Studio**
   - Download and install [Android Studio](https://developer.android.com/studio) for setting up an Android emulator.

4. **Java Development Kit (JDK)**
   - Download and install the [JDK](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html) (version 8 or higher).

## Step-by-Step Configuration

### Windows OS

#### 1. Install Android Studio and Set Environment Variables

1. **Download and Install Android Studio**
   - Download Android Studio from the [official site](https://developer.android.com/studio) and install it.
   - Open Android Studio and set the SDK path in SDK Manager to `C:\Users\<YourUserName>\AppData\Local\Android\Sdk`.

2. **Set Environment Variables**
   - Open Control Panel → System → Advanced System Settings → Environment Variables.
   - Create a new System Variable:
     - **Variable Name**: `ANDROID_HOME`
     - **Variable Value**: `C:\Users\<YourUserName>\AppData\Local\Android\Sdk`
   - Add the following paths to the **Path** variable:
     - `%ANDROID_HOME%\platform-tools`
     - `%ANDROID_HOME%\emulator`

#### 2. Create and Run an Android Emulator

1. **Create a Virtual Device**
   - Open Android Studio and go to the AVD Manager: Click on **Configure** (+) > **Device Manager**.
   - Select **Create Virtual Device**.
   - Choose **Pixel 8a** and select **Oreo API Level 26**.

2. **Start the Emulator**
   - Open Command Prompt and navigate to the emulator directory:
     ```bash
     cd C:\Users\<YourUserName>\AppData\Local\Android\Sdk\emulator
     ```
   - Start the emulator:
     ```bash
     emulator -avd <Your_Emulator_Name>
     ```

#### 3. Install Node.js and Appium

1. **Install Node.js**
   - Download and install Node.js from [nodejs.org](https://nodejs.org/). Verify installation:
     ```bash
     node -v
     npm -v
     ```

2. **Install Appium**
   - Install Appium globally:
     ```bash
     npm install -g appium@next
     ```

3. **Install Appium Doctor**
   - Install Appium Doctor:
     ```bash
     npm install -g appium-doctor
     ```
   - Optionally, run Appium Doctor to verify setup:
     ```bash
     appium-doctor --android
     ```

#### 4. Setup WebdriverIO in Visual Studio Code

1. **Open Visual Studio Code**
   - Create a new project folder and open it in VS Code.

2. **Install WebDriverIO and Appium**
   - Run the following command:
     ```bash
     npm init wdio <folder_name> --save-dev
     ```
   - Follow the prompts:
     - **Type of testing**: E2E Testing - Web or Mobile Applications.
     - **Automation Backend**: On my local machine.
     - **Environment to automate**: Mobile - Native, Hybrid, and Web Apps.
     - **Mobile Environment**: Android.
     - **Automation Framework**: Mocha.
     - **Add services**: Appium.

#### 5. Emulator and APK Setup

1. **Create a Bat File for Emulator**
   - Create a `.bat` file to start your emulator (e.g., `Shiva.bat`):
     ```batch
     cd C:\Users\<YourUserName>\AppData\Local\Android\Sdk\emulator
     emulator -avd <Your_Emulator_Name>
     ```

2. **Install APK on Emulator**
   - Copy your APK file to `C:\Users\<YourUserName>\AppData\Local\Android\Sdk\platform-tools`.
   - Open Command Prompt from this directory and run:
     ```bash
     adb install <name_of_apk.apk>
     ```

#### 6. Configure WebDriverIO for Mobile Testing

1. **Update WebDriverIO Configuration**
   - In `wdio.conf.js`, update the `capabilities` section:
     ```javascript
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
     ```

2. **Update `package.json`**
   - Add the following script:
     ```json
     "scripts": {
       "wdio": "wdio run ./wdio.conf.js"
     }
     ```

#### 7. Create Test Files

1. **Create Test Folder Structure**
   - Inside `webdriverio-appium-v8`, create the following folder structure:
     ```
     test/
     └── specs/
         └── example.test.js
     ```

#### 8. Running Tests

1. **Run Tests**
   - In the VS Code terminal, run:
     ```bash
     npx wdio wdio.conf.js
     ```

#### 9. Using Appium Inspector

1. **Download and Install Appium Inspector**
   - Search for "Appium Inspector download" and install the `.exe` file.

2. **Configure and Start a Session**
   - Launch Appium Inspector and configure it:
     - **Platform Name**: Android
     - **Device Name**: Shiva_Pixel
     - **App Package**: (Get this from the APK info app)
     - **App Activity**: (Choose from the available activities)
     - **Automation Name**: UiAutomator2
