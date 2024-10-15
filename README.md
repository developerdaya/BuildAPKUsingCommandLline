you can **build an APK without using Android Studio** by using the **command line** with Gradle and the Android SDK. Here's how you can do it:

### Requirements:
1. **JDK (Java Development Kit)** installed on your system.
2. **Android SDK** installed.
3. **Gradle** installed.
4. An **Android project** directory (which can be created using Android Studio or downloaded).

### Steps to Build APK without Android Studio:

#### 1. Install JDK
Ensure that Java is installed and set up properly. You can check the installation with:

```bash
java -version
```

#### 2. Install Android SDK
You’ll need the Android SDK. You can download it via **Android Command-Line Tools**. Once the SDK is installed, set up the environment variables.

- **Download SDK Tools** from [Android Developer](https://developer.android.com/studio).
- Extract the zip file and add the SDK's `tools` and `platform-tools` directories to your PATH.
- Install build tools and necessary components using SDK Manager (CLI command).

```bash
sdkmanager --install "platform-tools" "build-tools;30.0.3" "platforms;android-30"
```

#### 3. Install Gradle
If you don't have Gradle installed, you can install it manually:
- Download Gradle from the [Gradle website](https://gradle.org/install/).
- Add Gradle to your system's PATH variable.

You can check if Gradle is installed by running:

```bash
gradle -v
```

#### 4. Set Up Android Project
You need an Android project with a `build.gradle` file configured. This can either be a project you create via Android Studio or any other source.

#### 5. Build APK from Command Line

Once everything is set up, navigate to the root of your Android project directory (where `build.gradle` is located) and run the following commands:

1. **Clean the project (optional but recommended):**

```bash
./gradlew clean
```

2. **Build the APK:**

```bash
./gradlew assembleDebug
```

- The `assembleDebug` task compiles your project in debug mode. For a release APK, you would run:

```bash
./gradlew assembleRelease
```

#### 6. Find the Generated APK

Once the build completes, the APK will be generated in:

```
/app/build/outputs/apk/debug/app-debug.apk
```

For a release build, the path will be:

```
/app/build/outputs/apk/release/app-release.apk
```

#### 7. Sign the APK (Optional for Release APK)

If you are generating a **release APK**, you’ll need to sign it before distribution:

1. **Generate a Keystore:**
   Run this command to generate a key:

   ```bash
   keytool -genkey -v -keystore my-release-key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias my-key-alias
   ```

2. **Sign the APK:**

   After building the release APK, sign it with:

   ```bash
   jarsigner -verbose -keystore my-release-key.jks app-release-unsigned.apk my-key-alias
   ```

3. **Optimize (Zipalign) the APK:**

   Run the following command to optimize the APK:

   ```bash
   zipalign -v 4 app-release-unsigned.apk app-release.apk
   ```

### Summary:
- You can build APKs without Android Studio using the **command line** with **Gradle** and **Android SDK**.
- For debugging, you use `assembleDebug`, and for production-ready builds, use `assembleRelease` along with signing and optimizing.
  
Here’s how you can **build an APK using the command line** without Android Studio, step-by-step using **Windows Command Prompt** or **Linux/macOS Terminal**.

### Prerequisites:
1. **JDK (Java Development Kit)**
2. **Android SDK** (with platform-tools, build-tools installed)
3. **Gradle**

### Step-by-Step Instructions:

#### 1. Install Java Development Kit (JDK)

Ensure that Java is installed. You can check it by running the following in your command prompt:

```bash
java -version
```

If not installed, download and install the JDK from the [official Oracle site](https://www.oracle.com/java/technologies/javase-downloads.html).

#### 2. Install Android SDK

You need the **Android SDK** to compile and build APKs. You can download the **Command-Line Tools** from [Android Developer](https://developer.android.com/studio).

Once downloaded, extract it, and install the platform and build tools:

```bash
sdkmanager --install "platform-tools" "build-tools;30.0.3" "platforms;android-30"
```

Make sure to add `platform-tools` and `tools` to your system's PATH. This allows you to run SDK commands from anywhere.

#### 3. Install Gradle

Download and install **Gradle** from the [official Gradle website](https://gradle.org/install/).

Once installed, check the version by running:

```bash
gradle -v
```

#### 4. Prepare an Android Project

If you have an Android project, navigate to its directory. This project should contain the `build.gradle` files. You can either clone a GitHub project or use an existing one.

#### 5. Command to Build APK

Navigate to the root folder of the project (where your `build.gradle` file is located). 

##### 5.1. Clean the Project (Optional but Recommended)

First, clean the project:

```bash
./gradlew clean
```

##### 5.2. Build APK

To build a **debug APK**, run the following command:

```bash
./gradlew assembleDebug
```

For a **release APK**, run:

```bash
./gradlew assembleRelease
```

#### 6. Locate the Generated APK

Once the build completes, the APK will be available in:

- **For Debug APK:**  
  `app/build/outputs/apk/debug/app-debug.apk`
  
- **For Release APK:**  
  `app/build/outputs/apk/release/app-release.apk`

#### 7. Optional: Signing the Release APK

If you are creating a **release APK**, it must be signed. Use the following steps:

1. **Generate a Keystore** (If you don't have one):

   ```bash
   keytool -genkey -v -keystore my-release-key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias my-key-alias
   ```

2. **Sign the APK**:

   ```bash
   jarsigner -verbose -keystore my-release-key.jks app-release-unsigned.apk my-key-alias
   ```

3. **Optimize the APK (Zipalign)**:

   ```bash
   zipalign -v 4 app-release-unsigned.apk app-release.apk
   ```

After this, you can distribute your **signed APK** for production.

---

### Example of Full Commands:

```bash
# Navigate to the project directory
cd /path/to/your/android/project

# Clean the project (optional)
./gradlew clean

# Build debug APK
./gradlew assembleDebug

# Or build release APK
./gradlew assembleRelease

# Sign the release APK (if necessary)
jarsigner -verbose -keystore my-release-key.jks app-release-unsigned.apk my-key-alias

# Align the APK
zipalign -v 4 app-release-unsigned.apk app-release.apk
```

If you have **Gradle installed via Android Studio**, it means that Android Studio comes with its own Gradle version that you can use for building your projects. However, the **Gradle wrapper** (`gradlew`) that comes with each Android project allows you to use the embedded Gradle without manually installing it separately.

Here’s how you can use the **Gradle installed with Android Studio** to build APKs from the command line:

### 1. Using the Gradle Wrapper (`gradlew`)

Every Android project generated by Android Studio includes a **Gradle wrapper** script (`gradlew` for Unix/Linux/Mac or `gradlew.bat` for Windows). The **Gradle wrapper** ensures that your project can build with a specific Gradle version, even if you haven't installed Gradle globally.

#### Steps:

1. **Open Command Line or Terminal**:
   - On **Windows**: Open **Command Prompt** or **PowerShell**.
   - On **macOS/Linux**: Open **Terminal**.

2. **Navigate to Your Project Directory**:
   Use the `cd` command to go to the root directory of your Android project. This is the folder where your `build.gradle` file is located.

   For example:
   
   ```bash
   cd /path/to/your/android/project
   ```

3. **Use the Gradle Wrapper to Build APK**:
   Since Android Studio's Gradle wrapper (`gradlew`) is already configured, you can run the following commands directly:

   - **Clean the Project** (Optional but recommended):
   
     ```bash
     ./gradlew clean
     ```

   - **Build Debug APK**:

     ```bash
     ./gradlew assembleDebug
     ```

     This will create a **debug APK**.

   - **Build Release APK** (For production-ready apps):

     ```bash
     ./gradlew assembleRelease
     ```

     This command will generate the **release APK**, which you can later sign for distribution.

4. **Locate the APK**:
   After running the `gradlew` commands, the generated APK will be in:

   - **For Debug APK**: `app/build/outputs/apk/debug/app-debug.apk`
   - **For Release APK**: `app/build/outputs/apk/release/app-release.apk`

### 2. Using Android Studio’s Embedded Gradle Manually (Optional)

If you want to use Android Studio's embedded Gradle manually, you can use it by pointing your terminal to the Gradle path inside Android Studio.

#### Steps:

1. **Find Gradle Path in Android Studio**:
   - Open Android Studio.
   - Go to **File** > **Settings** > **Build, Execution, Deployment** > **Gradle** (On Mac: Android Studio > Preferences > Gradle).
   - Look for the **Gradle home** directory. It is typically something like:
   
     - On Windows: `C:\Program Files\Android\Android Studio\gradle\gradle-x.x`
     - On Mac/Linux: `/Applications/Android Studio.app/Contents/gradle/gradle-x.x`

2. **Add the Path to Your System** (Optional):
   You can add this path to your system's environment variables (like in the previous steps), but using the **Gradle wrapper** (`gradlew`) is usually more convenient and ensures version consistency across different projects.

---

### 3. Build APK Without Android Studio GUI

You don’t need to open Android Studio to build APKs. You can always use the **Gradle wrapper** as described to build APKs from the command line.

#### For Example:

1. **Navigate to Your Project Folder**:

   ```bash
   cd /path/to/your/android/project
   ```

2. **Run the Gradle Wrapper Command**:

   ```bash
   ./gradlew assembleDebug  # For debug APK
   ./gradlew assembleRelease  # For release APK
   ```

The APK will be generated without having to open Android Studio.


