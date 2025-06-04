# Universal Integration for Google Sign-In

## Introduction

The **Universal Integration for Google Sign-In** plugin simplifies integrating Google authentication into Unity projects across multiple platforms.

![Universal Integration for Google Sign-In](https://github.com/user-attachments/assets/a4167ef3-df87-4634-a9cd-56524e035e29)

It supports **Android**, **iOS**, **WebGL**, **Windows**, **macOS**, **UWP**, and the **Unity Editor**, handling platform-specific flows for a seamless user experience.

🔗 Available on the Unity Asset Store:
[https://assetstore.unity.com/packages/slug/293326](https://assetstore.unity.com/packages/slug/293326)

---

## ✅ Supported Platforms

* **WebGL**: JavaScript-based OAuth 2.0 implicit flow.
* **Android**: Native sign-in using Google Play Services.
* **iOS**: ASWebAuthenticationSession + Deep Link.
* **macOS / UWP**: System browser + Deep Link.
* **Windows / Unity Editor**: Loopback server flow.

---

## ⚙️ Platform Setup Guide

### WebGL

* **Client ID**: Use a **Web Client ID** from Google Credentials.
* **Init**: Provide this ID directly.
* **Google Console Setup**:

  * Set **Authorized redirect URIs** to match your domain.
  * Set **Authorized JavaScript origins** to match your domain.

```csharp
UniversalGSignIn.Init("your-web-client-id", OnInit);
```

---

### Android

* **Create Two Client IDs** in Google Cloud Console:

  1. **Android Client ID**

     * Set **package name** and **SHA1 fingerprint** using:

       ```sh
       keytool -keystore path-to-debug-or-production-keystore -list -v
       ```
  2. **Web Client ID**

     * This will be passed to the `Init` method (Google auto-detects Android client ID internally).

```csharp
UniversalGSignIn.Init("your-web-client-id", OnInit);
```

> [!CAUTION]
> Do not use the Android client ID in Unity. Google Play Services automatically uses it on Android devices.

---

### iOS / macOS / UWP (Deep Link + ASWebAuthenticationSession)

* **Client ID**: Create an **iOS Client ID** (even for UWP/macOS).
* **Get iOS URL Scheme** from Google Console.
* **Configure Deep Linking**:

  * Follow Unity’s [Deep Linking Guide](https://docs.unity3d.com/Manual/deep-linking.html)
  * Add the scheme to all target platforms (iOS, macOS, UWP).
* **Init**:

```csharp
UniversalGSignIn.Init("your-ios-client-id", OnInit, urlScheme: "com.googleusercontent.apps.xxxxx");
```

---

### Windows / Unity Editor (Loopback)

* **Client ID**: Create a **Desktop Client ID**.
* **Client Secret**: Required for full sign-in; optional if only requesting offline access.
* **Redirect URI**: Use something like `http://localhost:3000/`.
* **Init**:

```csharp
UniversalGSignIn.Init(
    "your-desktop-client-id",
    OnInit,
    clientSecret: "your-client-secret",
    loopbackLink: "http://localhost:3000"
);
```

---

## 🧪 Basic Usage

### Initialize

```csharp
UniversalGSignIn.Init(clientId, OnInitialized);
```

### Sign In

```csharp
UniversalGSignIn.SignIn(OnSignIn);
```

### Grant Offline Access

```csharp
UniversalGSignIn.GrantOfflineAccess(OnAccessGranted);
```

### Sign Out

```csharp
UniversalGSignIn.SignOut();
```

### Check Sign-In Status

```csharp
bool isSignedIn = UniversalGSignIn.IsSignedIn();
```

### Get Basic Profile

```csharp
var profile = UniversalGSignIn.GetCurrentUserBasicProfile();
```

---

## 🛠️ Error Handling

Always check for errors:

```csharp
void OnSignIn(UniversalGSignIn.GoogleUser user) {
    if (!string.IsNullOrEmpty(user.error)) {
        Debug.LogError("Sign-In Error: " + user.error);
        return;
    }
    Debug.Log("Signed in as: " + user.basicProfile.name);
}
```

---

## 📜 License

Licensed under the [Standard Unity Asset Store EULA](https://unity.com/legal/as-terms).

---

## 📩 Contact

For support or questions: [mohelm97@gmail.com](mailto:mohelm97@gmail.com)

---

🙌 Thank you for using **Universal Integration for Google Sign-In**!
