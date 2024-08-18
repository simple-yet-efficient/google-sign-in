# Google Sign In Plugin

## Introduction

The `GoogleSignIn` plugin simplifies integrating Google Sign-In into Unity projects.

It supports Android, iOS, WebGL, and standalone platforms like Windows and macOS.

The plugin provides an easy way to authenticate users with Google accounts and access their profile information, handling platform-specific details for a seamless user experience.


## Supported Platforms

- **WebGL**: Native support.
- **Android**: Native support.
- **iOS**: Deeplink using `ASWebAuthenticationSession`.
- **macOS, UWP**: Deeplink.
- **Windows, Editor**: Loopback.

### Notes

1. **Deep Linking Configuration**: For platforms that utilize deep linking (iOS, macOS, UWP), you must configure the player settings to enable deep linking. Refer to the [Unity Manual on Deep Linking](https://docs.unity3d.com/Manual/deep-linking.html) and make sure to specify the URL scheme used in the `Init` call.
2. **Loopback Configuration**: For platforms using loopback (Windows, Editor), you need to provide your client secret and specify a loopback URL (e.g., `http://localhost:3000`) in the `Init` call.

This setup is essential for proper authentication and callback handling.

## Getting Started

### 1. Initialize GoogleSignIn

Before using Google Sign-In, you need to initialize the plugin with your Google Client ID.

```csharp
using GoogleSignIn;

void Start() {
    string clientId = "your-client-id.apps.googleusercontent.com";
    GoogleSignIn.Init(clientId, OnInitialized);
}

void OnInitialized() {
    Debug.Log("Google Sign-In Initialized");
}
```

### 2. Sign In the User

To sign in a user, call the `SignIn` method. This will prompt the user to log in with their Google account.

```csharp
void SignInUser() {
    GoogleSignIn.SignIn(OnSignIn);
}

void OnSignIn(GoogleSignIn.GoogleUser user) {
    if (string.IsNullOrEmpty(user.error)) {
        Debug.Log("User signed in: " + user.basicProfile.name);
    } else {
        Debug.LogError("Sign-In Error: " + user.error);
    }
}
```

### 3. Grant Offline Access

If your application requires offline access to Google APIs, request it using the `GrantOfflineAccess` method.

```csharp
void GrantAccess() {
    GoogleSignIn.GrantOfflineAccess(OnAccessGranted);
}

void OnAccessGranted(GoogleSignIn.GrantOfflineAccessResponse response) {
    if (string.IsNullOrEmpty(response.error)) {
        Debug.Log("Access granted, code: " + response.code);
    } else {
        Debug.LogError("Access Error: " + response.error);
    }
}
```

### 4. Sign Out the User

To sign out the user from their Google account:

```csharp
void SignOutUser() {
    GoogleSignIn.SignOut();
    Debug.Log("User signed out.");
}
```

### 5. Check if User is Signed In

To check if the user is currently signed in:

```csharp
bool isSignedIn = GoogleSignIn.IsSignedIn();
Debug.Log("Is user signed in? " + isSignedIn);
```

### 6. Get User's Profile Information

Retrieve the basic profile information of the signed-in user:

```csharp
GoogleSignIn.BasicProfile profile = GoogleSignIn.GetCurrentUserBasicProfile();
Debug.Log("User Name: " + profile.name);
Debug.Log("User Email: " + profile.email);
```



## Error Handling

Most methods in the `GoogleSignIn` plugin return an error message if something goes wrong. Always check for errors in the callbacks to ensure a smooth user experience.

```csharp
void OnSignIn(GoogleSignIn.GoogleUser user) {
    if (!string.IsNullOrEmpty(user.error)) {
        Debug.LogError("Sign-In Error: " + user.error);
        return;
    }
    // Process signed-in user data
}
```


## License

This plugin is licensed under [Standard Unity Asset Store EULA](https://unity.com/legal/as-terms).

## Contact

For any questions or support, feel free to reach out at [mohelm97@gmail.com](mailto:mohelm97@gmail.com).

---

Thank you for using the `GoogleSignIn` plugin! We hope it simplifies the process of integrating Google authentication into your Unity projects.