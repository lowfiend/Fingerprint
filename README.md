# Fingerprint Dialog [![Download](https://api.bintray.com/packages/omaflak/maven/fingerprintdialog/images/download.svg)](https://bintray.com/omaflak/maven/fingerprintdialog/_latestVersion)

**FingerprintDialog** is an Android library that simplifies the process of **fingerprint** authentications. It can display **dialogs** to perform fingerprint auhentication very easily.

Furthermore, the library provides a fingerprint view that you can use like regulars xml views. In both cases the FingerprintDialog library implements in a simple way the use of a CryptoObject.

# Gradle Dependency

```groovy
implementation 'me.aflak.libraries:fingerprintdialog:2.5.0'
```

## Without CryptoObject

You only want to check if the user's fingerprint is enrolled in the phone.

```java
FingerprintDialog.initialize(this)
    .title(R.string.title)
    .message(R.string.message)
    .callback(new FingerprintDialogCallback(...))
    .show();
```

[**EXAMPLE**](https://github.com/omaflak/FingerprintDialog-Library/blob/master/app/src/main/java/me/aflak/fingerprintdialoglibrary/FingerprintExample.java)
        
## With CryptoObject

Check if the user's fingerprint is enrolled in the phone and detect if a new fingerprint was added since last time authentication was used.

```java
FingerprintDialog.initialize(this)
    .title(R.string.title)
    .message(R.string.message)
    .callback(new FingerprintDialogSecureCallback(...), "KeyName")
    .show();
```
        
[**EXAMPLE**](https://github.com/omaflak/FingerprintDialog-Library/blob/master/app/src/main/java/me/aflak/fingerprintdialoglibrary/FingerprintSecureExample.java)

## Secure a CryptoObject via authentication

CryptoObject can be used to perform cryptographic operations on Android. You can set the CryptoObject to be valid only if the user has authenticated via fingerprint before. You have to use `setUserAuthenticationRequired(true)` when creating the CryptoObject.

```java
FingerprintManager.CryptoObject cryptoObject;
// cryptoObject = ...

if(FingerprintDialog.isAvailable(this)) {
    FingerprintDialog.initialize(this)
            .title(R.string.fingerprint_title)
            .message(R.string.fingerprint_message)
            .callback(new FingerprintCallback(...))
            .cryptoObject(cryptoObject)
            .show();
}
```

## Fingerprint View

The library also provides a Fingerprint object which is a view that you can display the way you want.

```xml
<me.aflak.libraries.view.Fingerprint
    android:id="@+id/fingerprint"
    android:layout_width="200dp"
    android:layout_height="200dp"/>
```

```java
Fingerprint fingerprint = findViewById(R.id.fingerprint);
fingerprint.callback(new FingerprintCallback(...));
fingerprint.authenticate();
```

[**EXAMPLE**](https://github.com/omaflak/FingerprintDialog-Library/blob/master/app/src/main/java/me/aflak/fingerprintdialoglibrary/FingerprintViewExample.java)

# Customization

Several functions are available to customize your dialog.

```java
FingerprintDialog.initialize(this)
        .title(R.string.fingerprint_title)
        .message(R.string.fingerprint_message)
        .enterAnimation(DialogAnimation.Enter.RIGHT)
        .exitAnimation(DialogAnimation.Exit.RIGHT)
        .circleScanningColor(R.color.colorAccent)
        .callback(this)
        .show();
```

You can also customize the fingerprint view directly from the xml.

```xml
<me.aflak.libraries.view.Fingerprint
    xmlns:fingerprint="http://schemas.android.com/apk/res-auto"
    fingerprint:circleScanningColor="@android:color/black"
    fingerprint:fingerprintScanningColor="@color/colorAccent"
    android:id="@+id/fingerprint"
    android:layout_width="200dp"
    android:layout_height="200dp" />
```

# Rendering

<p float="left">
    <img src="https://github.com/omaflak/FingerprintDialog/blob/master/GIF/demo1.gif" width="400" />
    <img src="https://github.com/omaflak/FingerprintDialog/blob/master/GIF/demo2.gif" width="400" />
</p>

# License

```
MIT License

Copyright (c) 2017 Michel Omar Aflak

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```