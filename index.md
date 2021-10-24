# October 17th 2021

Starting my crypto journey - I was asked by some colleagues if I was up to the task. Creating a crypto wallet for the **Celo DeFi For The People** hackathon, built on the CELO blockchain.

I excitedly accepted the challenge, knowing only theoretically about blockchain in practice; and nothing about implementation details, blockchain offerings or web3.

I was advised to use the open-source **Rainbow Wallet** ("Rainbow")project which was developed with the Ethereum blockchain in mind, and connects to the **Uniswap** crypto and defi exchange.

Okay... so mental overload. So basically, the challenge of the challenge is a refactoring job right? But first -- environment setup.

## Environment Setup

So Rainbow provides setup instructions for *Mac OS* and *Linux*, so I sideloaded *Ubuntu*. Easy.

After that it was a matter of installing the regular requirements:

* NodeJs & NPM
* Yarn
* Android Studio

> I would recommend strongly to use **NVM** to install NodeJs.

---

### Issues

After installing all the prerequisites above, I hit the `yarn setup` or `yarn install` and immediately ran into this issue:

![Unable to download AAR file.](/assets/images/yarn-issue-1.jpeg)

This issue was replicateable and I later realized that it was due to my internet speed - somehow unable to download the file and the install script timing out.

![Successfully build the Rainbow project.](/assets/images/yarn-issue-2.jpeg)


After this issue was one related to *ADB (Android Debug Bridge)*. Basically I had it installed using `apt-get` as well as part of the Android Studio SDK. This caused an issue where the *AVM* would listen for signals from the Android SDK ADB, while the Rainbow wallet would deploy and serve code using the user-installed ADB.

```
adb server version (36) doesn't match this client (39); killing...
```

In order to resolve the issue, I uninstalled ADB from the system and as a result, I would need to; serve the app using `yarn start` as the unprivileged user and owner of the project; build the app using `sudo yarn android` as the user with sudo privelege to access `/root/Android/Sdk/platform-tools/adb` executable.

---

### First Build

Soon, I was able to have my first build of Rainbow on my android AVM, or at least we got the gradle to build the packaged application and load it to my AVM.

![Unable to download AAR file.](/assets/images/react-native-1.jpeg)

Barring some minor information logs complaining about some GraphQL misconfiguration issues - the app built and was launched on the AVM.

![Unable to download AAR file.](/assets/images/react-native-2.jpeg)

What you're seeing above is system logs printed by the Metro Bundler that is serving the app to my device.