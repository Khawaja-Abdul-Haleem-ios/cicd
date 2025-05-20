🚀 iOS CI/CD Pipeline with Fastlane & Jenkins
This project uses Fastlane for automating the iOS app build and TestFlight distribution, integrated with Jenkins for continuous deployment.

📄 Fastlane Configuration Overview
🔐 App Store Connect API Authentication
Instead of using Apple ID and password, the project uses App Store Connect API Key authentication for better security and automation.

ruby
Copy
Edit
app_store_connect_api_key(
  key_id: "YOURKEYID",
  issuer_id: "YOURISSUERID",
  key_filepath: "fastlane/YOURAUTHKEY.p8",
  in_house: false
)
What Each Parameter Means:
key_id: The unique ID of your API key generated from App Store Connect.

issuer_id: A unique ID for your App Store Connect account (team).

key_filepath: The path to the .p8 private key file downloaded from App Store Connect.

in_house: Set to false for public App Store apps (set to true only if you're distributing enterprise/in-house apps).

✅ This authentication method enables headless CI/CD, allowing Jenkins to interact with App Store Connect securely without manual login prompts.

🛠 beta Lane Summary
The beta lane in your Fastfile is designed to:

Build the iOS app using the CICD scheme.

Export the app using the app-store export method.

Upload the build to TestFlight for:

🔹 Internal testers (group: Internal)

🔹 External testers (group: External)

Submit the app for review with automatic release enabled.

Handle errors gracefully (e.g., skip external upload if another build is already in review).

🚀 How to Deploy
🔹 Locally
Run this command inside your iOS project:

bash
Copy
Edit
fastlane beta
🔹 Jenkins Integration
Jenkins is configured to automatically:

Checkout code from your Git repo

Run fastlane beta

Distribute builds via TestFlight

Submit for App Store review

✅ Requirements
Before running:

Add your .p8 API key to fastlane/AuthKey_Z9L46VG577.p8

Ensure provisioning profiles and certificates are valid

TestFlight groups Internal and External must exist

Fastlane must be installed (brew install fastlane)

📬 Feedback
External testers will receive builds via TestFlight. Feedback is directed to:

📧 abc@xyz.com









