# Aries Mobile Components

---

Keychain iOS 15, simulator and device, is not supported right now. Related
issue is [here](https://github.com/oblador/react-native-keychain/issues/510)
and apple developer forum link is
[here](https://developer.apple.com/forums/thread/685773). Pull requests for
fixes for this are much appriciated!

---

> TODO: this should be removed and just link to the docs website

React Native components that will help you build a better wallet.

## Requirements

These components have been tested against React Native `0.66.x` and `0.68.x`. Different minimum versions apply for different packages. But above `0.64.x`
every package should work fine.

## Installation

**yarn**

```console
yarn add @aries-components/expo-qr-scanner
yarn add @aries-components/keychain
```

**npm**

```console
npm install @aries-components/expo-qr-scanner
npm install @aries-components/keychain
```

### QrScanner

This is a simple camera view, with barcode cut-out, to scan qrcodes. It uses `expo-camera` under the hood and is customizable.
Please check the documentation inside the component for more information.

#### Usage

```tsx
import React from 'react'
import { QrScanner } from '@aries-components/expo-qr-scanner'

export const CustomScanner = () => {
  // This callback will be called with a string from whatever the QR scanner
  // scanned.
  const onScan = (result: string) => console.log(`Result: ${result}`)

  // This callback will be called when the user presses the `cancel` button
  // It is common practise to hide the view here or navigate back
  const onCancel = () => console.log('navigate back!')

  return <QrScanner onScan={onScan} onCancel={onCancel} />
}
```

### Keychain

A simple package that allows you to use secure storage to set and get a Key

In order to use `useKeychain` the outer component MUST be wrapped inside a `<KeychainProvider />`

#### Usage

```tsx
import React from 'react'
import { KeychainProvider, useKeychain } from '@aries-components/keychain'

// The `KeychainProvider` should be above the components where you would like to
// use the keychain
export const Wrapped = () => (
  <KeychainProvider service="mock_service">
    <App />
  </KeychainProvider>
)

// ...

// Get the keychain accessor
const keychain = useKeychain()

// Set your wallet key in the secure storage
// This will be derived with argon2i for security
await keychain.setWalletKey('my-custom-password')

// Get your wallet key from secure storage
const myDerivedPassword = await keychain.getWalletKey()

// Reset your wallet key
// Accepts a boolean whether to reset the salt used in the key derivation
keychain.resetWalletKey(false)
```

### Storybook

In order to test the user-interface components of this repository, a storybook
has been setup. This allows everyone to test changes to components as much as
possible.

#### Testing

To test the components run the following commands:

```console
cd demo

yarn

yarn ios

# In a new terminal
yarn storybook-watcher
```
