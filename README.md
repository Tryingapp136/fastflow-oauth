# FastFlow

A beautiful intermittent fasting app with dynamic UI and animations.

## Withings Integration

This repository includes the OAuth callback page needed for the Withings API integration in the FastFlow app. The callback URL is:

```
https://tryingapp136.github.io/fastflow-oauth/callback/
```

### How it works

1. The FastFlow app redirects users to the Withings authorization page
2. After authorizing, Withings redirects back to our callback page
3. The callback page displays the authorization code
4. Users copy this code back to the FastFlow app
5. The app exchanges the code for an access token to fetch weight data

## Development

### Prerequisites

- Flutter SDK
- Android Studio or VS Code
- Withings Developer Account for API access

### Setup

1. Clone the repository
2. Run `flutter pub get` to install dependencies
3. Add your Withings API credentials in the appropriate files

## License

This project is licensed under the MIT License - see the LICENSE file for details.
