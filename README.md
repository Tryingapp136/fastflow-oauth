# FastFlow

FastFlow is a health tracking app that integrates with Health Connect and Withings to help users track their fasting, water intake, and weight.

## Setup Withings Integration with HTTPS App Links

To enable Withings integration in the app with secure HTTPS callbacks, follow these steps:

### 1. Set up GitHub Pages for OAuth Callback

1. Fork or clone the repository at https://github.com/Tryingapp136/fastflow-oauth
2. Make sure GitHub Pages is enabled for the repository:
   - Go to repository Settings → Pages
   - Set the source to deploy from the main branch
   - Wait for the page to be published at https://tryingapp136.github.io/fastflow-oauth/

### 2. Configure App Links

1. Get your app's SHA-256 fingerprint:
   - For debug builds: `cd android && ./gradlew signingReport`
   - For release builds: Use your release keystore's SHA-256 fingerprint

2. Update `.well-known/assetlinks.json` in the GitHub repository:
   ```json
   [{
     "relation": ["delegate_permission/common.handle_all_urls"],
     "target": {
       "namespace": "android_app",
       "package_name": "com.fastflow.fastflow",
       "sha256_cert_fingerprints": [
         "YOUR_SHA256_FINGERPRINT_HERE"
       ]
     }
   }]
   ```

### 3. Register with Withings

1. Visit [Withings Developer Portal](https://developer.withings.com) and create an account
2. Create a new application with the following details:
   - **Application Name**: FastFlow
   - **Description**: A health tracking app for fasting, water intake, and weight
   - **Callback URL**: `https://tryingapp136.github.io/fastflow-oauth/callback`
   - **Required APIs**: Weight and Body Metrics

3. Once your application is created, you'll receive a Client ID and Client Secret
4. Update the following values in `lib/services/withings_service.dart`:
   ```dart
   static const String _clientId = 'YOUR_CLIENT_ID'; 
   static const String _clientSecret = 'YOUR_CLIENT_SECRET';
   ```

## How the OAuth Flow Works

1. When a user attempts to connect their Withings account from the FastFlow app, they are directed to the Withings OAuth authorization page via the `flutter_web_auth_2` package.
2. After successful authorization, Withings redirects the user to the HTTPS callback URL on GitHub Pages.
3. The GitHub Pages site extracts the authorization code and redirects back to the app using the `fastflow://callback` scheme.
4. The app processes the authorization code and exchanges it for access tokens using the Withings API.
5. The app displays a success screen and saves the user's Withings connection details securely.
