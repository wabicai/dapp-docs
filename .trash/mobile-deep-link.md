# Mobile Deep Link Integration (Three Methods)

We recommend using the custom scheme Deep Link (`onekey-wallet://`) and the raw WalletConnect URI (`wc:`). Use Universal Link as a fallback. Full demo code is available here:

https://github.com/OneKeyHQ/hardware-js-sdk/tree/onekey/packages/connect-examples/react-native-demo

## Methods at a Glance

- Method 1 (Recommended): Deep Link custom scheme — directly opens the OneKey app
  - Format: `onekey-wallet://wc?uri={encoded_wc_uri}`
- Method 2 (Recommended): Raw WalletConnect URI — handled by the OS/OneKey
  - Format: `wc:xxxxx@2?relay-protocol=irn&symKey=...`
- Method 3 (Fallback): Universal Link — works when the custom scheme is unavailable
  - Format: `https://app.onekey.so/wc/connect/wc?uri={encoded_wc_uri}`

`{encoded_wc_uri}` must be created via `encodeURIComponent(wcUri)`.

## Quick Start (Web Minimal Example)

```javascript
// Assume you've obtained a WalletConnect V2 URI (wcUri)
const wcUri = 'wc:xxxxx@2?relay-protocol=irn&symKey=...';

// Method 1: Deep Link (Recommended)
const deepLink = `onekey-wallet://wc?uri=${encodeURIComponent(wcUri)}`;
window.open(deepLink, '_blank');

// Method 3: Universal Link (Fallback)
const universalLink = `https://app.onekey.so/wc/connect/wc?uri=${encodeURIComponent(wcUri)}`;
window.open(universalLink, '_blank');

// Method 2: Raw WalletConnect URI (Recommended)
window.open(wcUri, '_blank');
```

## React Native / Expo (Minimal)

For full demo code, see the React Native demo repository above. Minimal openers:

```ts
import { Linking } from 'react-native';

// Deep Link (recommended)
Linking.openURL(`onekey-wallet://wc?uri=${encodeURIComponent(wcUri)}`);

// Raw WalletConnect (recommended)
Linking.openURL(wcUri);

// Universal Link (fallback)
Linking.openURL(`https://app.onekey.so/wc/connect/wc?uri=${encodeURIComponent(wcUri)}`);
```

## Sample URIs (Copy-Paste Test)

```
Deep Link       onekey-wallet://wc?uri=<WalletConnectURI>
Universal Link  https://app.onekey.so/wc/connect/wc?uri=<WalletConnectURI>
WalletConnect   wc:6b18a69c27df54b4c228e0ff60218ba460a4994aa5775963f6f0ee354b629afe@2?relay-protocol=irn&symKey=99f6e5fa2bda94c704be8d7adbc2643b861ef49dbe09e0af26d3713e219b4355
```

## Mobile Platform Configuration

### iOS (Info.plist)

```xml
<key>CFBundleURLSchemes</key>
<array>
  <string>onekey-wallet</string>
  <string>wc</string>
  <!-- If your app has a custom scheme, register it here as well -->
  <!-- <string>your-app</string> -->
  <!-- <string>your-app-staging</string> -->
  <!-- <string>your-app-dev</string> -->
</array>

<key>com.apple.developer.associated-domains</key>
<array>
  <string>applinks:app.onekey.so</string>
</array>
```

### Android (AndroidManifest.xml)

```xml
<activity android:name=".MainActivity">
  <!-- Deep Link custom scheme -->
  <intent-filter>
    <action android:name="android.intent.action.VIEW" />
    <category android:name="android.intent.category.DEFAULT" />
    <category android:name="android.intent.category.BROWSABLE" />
    <data android:scheme="onekey-wallet" />
  </intent-filter>

  <!-- Universal Link fallback (enable autoVerify for best UX) -->
  <intent-filter android:autoVerify="true">
    <action android:name="android.intent.action.VIEW" />
    <category android:name="android.intent.category.DEFAULT" />
    <category android:name="android.intent.category.BROWSABLE" />
    <data android:scheme="https" android:host="app.onekey.so" android:pathPrefix="/wc" />
  </intent-filter>
</activity>
```

## Key Points & Best Practices

- Always `encodeURIComponent` the `wcUri` before injecting it into URLs.
- Recommended order: Deep Link (fast) or Raw WalletConnect (direct) first, Universal Link as a fallback.
- URI length limits: custom schemes have OS-dependent limits (iOS ~2K). Keep payloads concise.
- Test on real devices: simulators/dev mode can differ from production behavior.
- In Expo dev mode, the initial URL is `exp://...`; ignore it to avoid noise.

## Related Demo / Code

- React Native demo (full examples):
  - https://github.com/OneKeyHQ/hardware-js-sdk/tree/onekey/packages/connect-examples/react-native-demo

## Support & Feedback

- File issues in the `OneKey-Hardware-JS-SDK` repository.
- Please include: device OS version, OneKey app version, sample URI, steps to reproduce, and a short screen recording if possible.
