Setup Cordova and Android (Ubuntu)
===

### Requirements
- Java SDK.
- Android SDK.
- Gradle.
- Android Emulator (Required for emulate).
- In some cases you have to manualy setup PATH variables for Java SDK, Android SDK and Gradle.
- `cordova` install via `npm`.

### Steps todo
- Install `cordova`:
- Install Android SDK.
- Add PATH environment variable in file `~/.bashrc`

```shell
export PATH=${PATH}:~/android-sdk-linux/tools

export PATH=${PATH}:~/android-sdk-linux/platform-tools
```

### Refs
https://cordova.apache.org/docs/en/latest/guide/cli/index.html#installing-the-cordova-cli
https://askubuntu.com/questions/904136/android-home-environment-variable
https://gradle.org/install/
https://github.com/johnkmzhou/cordova-create-react-app