# Setup React-Native Environment in Your Mac

## Global Env

- nvm: https://github.com/nvm-sh/nvm#installation-and-update
- brew: https://brew.sh/index_zh-tw

## For JavaScript

  - `nvm install THE_VERSION_YOU_WANTED`
  - `nvm use THE_VERSION_YOU_WANTED`
  - expo: if you use expo, you need to install it by `npm install -g expo-cli`, or you can skip this step
  - add config in you `~/.bash_profile` or `~/zsh_rc`
      ```
      nvm alias default [THE_VERSION_YOU_INSTALLED] > /dev/null 2>&1
      nvm use default --silent
      ```
  - `source [THE_PREVIOUS_FILE_YOU_MODIFIED]`
  - `ln -s $(which node) /usr/local/bin/node`: you need to do that, because `node_modules/react-native/scripts/packager.sh` will be executed without nvm
    - there are some other [solutions](https://github.com/facebook/react-native/issues/3974#issuecomment-294706244), but those do not work for me

## For iOS

  - install xcode: please do not use beta version, it does not have the same path with the production version.
    - download from app store or click "additional downloads" in https://developer.apple.com/xcode/resources/

  - If you want to test this app in your iPhone, you need to do the following steps
    - generate the signing
      - Click the project
      - Go to the "General" tab (the default tab is "General" already in actually)
      - Choose Team, if you never have the account, you have to "Add an account" (by your `Apple ID`)
      - Click `Manage Certificates` and add one
      - Go back to the main menu, and you need to choose team again. (weird UX)
    - modify `bundle identifer`, or it is existed, so you cannot deploy to your iPhone    

## For Android

  - `brew tap caskroom/versions`
  - `brew update`
  - `brew tap adoptopenjdk/openjdk`
  - `brew cask install adoptopenjdk8`: you need to install jdk8 at first, in order to open `sdkmanager` to accept all agreements, because after 8, it will miss some libraries. 
    - There are some other [solutions](https://stackoverflow.com/questions/47150410/failed-to-run-sdkmanager-list-android-sdk-with-java-9), but it does not work for me
  -  execute `./Library/Android/sdk/tools/bin/sdkmanager --licenses`, and accept all. Every time, you update `sdkmanager`, you have to execute again
  -  `brew cask uninstall adoptopenjdk8`: to uninstall java 8
  -  `brew install java`: install latest java
  - install android studio: https://developer.android.com/studio/
  - create AVD by `AVDManager`
  - export the following
    ```
    export PATH=$PATH:$HOME/Library/Android/sdk/platform-tools
    export PATH=$PATH:$HOME/Library/Android/sdk/tools
    export JAVA_HOME=$(/usr/libexec/java_home)
    export PATH=$JAVA_HOME/bin:$PATH
    export CLASS_PATH=$JAVA_HOME/lib
    export ANDROID_HOME=$HOME/Library/Android/sdk
    ```
  - If you want to use `react-native-cli` to build app and deploy to AVD, you need to open your emulator at first
 