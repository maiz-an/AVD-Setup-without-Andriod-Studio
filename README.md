# Android SDK & AVD Setup Guide

This guide will help you download, configure, and manage Android SDKs, AVDs (Android Virtual Devices), and emulator settings. Follow the steps below to set up everything on your system.

---

## 1. **Download SDK and Set Environment Variables**

### Step 1: Download and Unzip the Android SDK

#### **How to Download the SDK:**
1. **Go to the Official Android Developer Site:**
   - Visit the [Android SDK Download Page](https://developer.android.com/studio#downloads).

2. **Download Command Line Tools (CLI):**
   - Under "Command line tools only," select the appropriate version for your operating system (Windows, macOS, or Linux).

3. **Extract the ZIP File:**
   - Windows: Right-click the downloaded `.zip` file and choose "Extract All" to a preferred directory (e.g., `C:\AndroidSDK`).
   - macOS: Double-click the `.zip` file, and it will be extracted to a folder.

   **Important:** Make a note of the extracted directory path (e.g., `C:\AndroidSDK` or `~/Android/sdk`).

#### **Install Required SDK Components:**
After unzipping the SDK:
1. Open a Command Prompt (Windows) or Terminal (macOS).
2. Navigate to the directory where you extracted the SDK.

   Example for Windows:
   ```bash
   cd C:\AndroidSDK\cmdline-tools\bin
   ```
   Example for macOS:
   ```bash
   cd ~/Android/sdk/cmdline-tools/bin
   ```
3. Run the following command to accept licenses and download the latest platform tools:
   ```bash
   sdkmanager "platform-tools" "platforms;android-34"
   ```

---

### Step 2: Set the SDK Path as a System Variable

#### **For Windows:**
1. Open "Control Panel" and go to "System" > "Advanced System Settings."
2. Click on "Environment Variables."
3. Under "System Variables," click "New."
   - Variable Name: `ANDROID_HOME`
   - Variable Value: Path to your extracted SDK folder (e.g., `C:\AndroidSDK`).
4. Edit the `Path` variable (under "System Variables") and add the following:
   - `C:\AndroidSDK\platform-tools`

#### **For macOS:**
1. Open the `.bash_profile` or `.zshrc` file in your home directory:
   ```bash
   nano ~/.zshrc
   ```
2. Add the following lines:
   ```bash
   export ANDROID_HOME=~/Android/sdk
   export PATH=$PATH:$ANDROID_HOME/platform-tools
   ```
3. Save the file and apply changes:
   ```bash
   source ~/.zshrc
   ```

### Step 3: Set the `ANDROID_HOME` Variable
- Ensure `ANDROID_HOME` is correctly set to your extracted SDK directory.

**Why this is important:** Setting these paths allows your system to recognize and use the Android SDK.

---

## 2. **Install Build Tools and Platform for Android 34**

Run these commands in your terminal or command prompt:

```bash
sdkmanager "build-tools;34.0.0"
sdkmanager "platforms;android-34"
```

These commands install the necessary tools and platform for Android 34.

### Step 3: Add Platform Tools to PATH
Make sure your `platform-tools` directory is included in your system's PATH variable.

**Example:** On Windows, it will be under the SDK folder: `C:\Users\YourUsername\AppData\Local\Android\Sdk\platform-tools`.

---

## 3. **Install System Images and Create an AVD**

### Install System Images
Run the following command to download the system image for Android 34:
```bash
sdkmanager "system-images;android-34;google_apis;x86_64"
```

### Create a New AVD (Android Virtual Device)
```bash
avdmanager create avd --name "MyAVD" --package "system-images;android-34;google_apis;x86_64"
```
- Replace `MyAVD` with a name you choose for your emulator.
- This creates an emulator with Google APIs for Android 34.

---

## 4. **List and Run Emulators**

### List Available Emulators
To see all available AVDs on your system:
```bash
emulator -list-avds
```

### Run an Emulator
```bash
emulator -avd MyAVD -netdelay none -netspeed full -gpu on -memory 4096 -cores 4 -no-snapshot-load -feature KeyboardSupport
```
- `-gpu on`: Enables GPU acceleration.
- `-memory 4096`: Allocates 4GB of memory to the emulator.
- `-cores 4`: Uses 4 CPU cores for the emulator.
- `-feature KeyboardSupport`: Enables physical keyboard support.

---

## 5. **Force Kill an Emulator**

If an emulator freezes or needs to be stopped:
```bash
adb -s emulator-5554 emu kill
```
- Replace `emulator-5554` with your emulator’s ID (found in the list from the previous step).

---

## 6. **Update SDK and AVD**

### Update All SDK Components
```bash
sdkmanager --update
```

### Update the Emulator
```bash
sdkmanager "emulator"
```

---

## 7. **Start and Stop the ADB Server**

Sometimes you may need to restart the ADB server:

### Kill the ADB Server
```bash
adb kill-server
```

### Start the ADB Server
```bash
adb start-server
```

---

## 8. **Pull and Push Files to/from AVD**

### Pull Files from AVD
To copy files from the AVD to your local system:

**Example 1:** Pull files to `C:\AVDFiles`:
```bash
adb pull /sdcard/Download/ C:\AVDFiles
```

**Example 2:** Pull files to `D:\avd\Avdx`:
```bash
adb pull /sdcard/Download/ D:\avd\Avdx
```

### Push Files to AVD
To send files from your computer to the AVD:

**Example 1:** Push a file to the AVD’s `Download` folder:
```bash
adb push C:\AVDFiles\myfile.txt /sdcard/Download/
```

**Example 2:** Push an image:
```bash
adb push C:\Users\Moham\Downloads\Bg.JPG /sdcard/Download/
```

### Create a Directory for Downloaded Files
To create a new directory inside the AVD:
```bash
adb shell mkdir /sdcard/Download
```

---

## 9. **Uninstall SDK Components**

### Uninstall Individual Components
To remove specific SDK components:
```bash
sdkmanager --uninstall "build-tools;34.0.0"
sdkmanager --uninstall "platforms;android-34"
sdkmanager --uninstall "system-images;android-34;google_play;x86_64"
```

### Uninstall Multiple Components at Once
```bash
sdkmanager --uninstall "build-tools;34.0.0" "platforms;android-34" "system-images;android-34;google_play;x86_64"
```

---

## 10. **Final Thoughts**

Congratulations on setting up your Android development environment! With everything installed and configured, you’re ready to build and run your Android projects.

Remember, I believe in you—you’ve got this! 😊

