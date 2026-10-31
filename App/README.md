# Back Screen Studio – Xiaomi 17 Pro / Pro Max

An Android app that adds three things to the back screen:

* **💬 Your messages**: a list of your chats (WhatsApp, Telegram, SMS, Messenger…). Tap one to read each message, with sender and time. 📱 opens that chat on the main screen.
* **🔊 Volume**: a slider plus − / + buttons, mute, and a choice of Media, Ring or Alarm volume.
* **🖼 Your own background**: any photo from your gallery, with adjustable darkening.

## How it works (and why Shizuku is needed)

HyperOS blocks third-party apps from opening on the back screen ("error 102").
It does **not** block *moving* an app that is already running there. Back Screen Studio:

1. starts its back-screen view on the main screen,
2. uses shell rights (through **Shizuku**) to run `am display move-stack <task> 1`,
3. optionally keeps the back screen awake and stops Xiaomi's own back-screen launcher
   (`com.xiaomi.subscreencenter`) from taking over again.

No root is needed. Shizuku runs entirely on the phone through Wireless debugging.

## 1. Build the APK (one time, on a computer)

1. Install **Android Studio** (free): https://developer.android.com/studio
2. Unzip this folder, then in Android Studio choose **File → Open** and select `BackScreenStudio`.
3. Wait for "Gradle sync" to finish. The first time, it downloads a few hundred MB.
4. Choose **Build → Build App Bundle(s) / APK(s) → Build APK(s)**.
5. Click **locate**. The file is `app/build/outputs/apk/debug/app-debug.apk`.
6. Copy the APK to your phone and install it. Allow "install unknown apps" when asked.

You can also plug the phone in with USB debugging on and press ▶ Run in Android Studio. That installs the app directly.

## 2. Set up Shizuku on the phone (one time)

1. Install **Shizuku** from Google Play or https://shizuku.rikka.app/download/
2. Go to **Settings → About phone** and tap **OS version** 7 times to enable Developer options.
3. Go to **Settings → Additional settings → Developer options** and turn on:
   * **USB debugging**
   * **USB debugging (Security settings)**. Xiaomi requires this for input commands; it may ask you to sign in to your Mi account.
   * **Wireless debugging**
4. Open Shizuku, tap **Pairing** under "Start via Wireless debugging", and follow its steps.
   You enter the pairing code from the notification. Then tap **Start**.
5. Shizuku must be started again after every reboot: open Shizuku and tap Start.

## 3. Set up Back Screen Studio

1. **Allow Shizuku access**, then tap *Allow* in the pop-up.
2. **Open notification access settings**, then turn on *Back Screen Studio – messages*.
   If it is greyed out, open the app's info page, use the ⋮ menu, choose *Allow restricted settings*, and try again.
3. **Choose picture** for the background and set how dark it should be.
4. Tap **▶ Show on back screen** and flip the phone over.

Tap **✕** on the back screen, or **Return to Xiaomi's back screen** in the app, to go back to the normal back screen.

### Recommended Xiaomi settings
HyperOS can kill background apps. To stop that:
* **Settings → Apps → Back Screen Studio → Battery saver → No restrictions**
* **Autostart → on**
* Lock the app in the Recents screen: long-press its card and tap the lock.

## Good to know
* **Messages only show up once the app is installed and allowed.** It collects them from
  notifications, so it sees what your notifications show. The app keeps the
  latest 50 messages for each of up to 30 chats, stored only on your phone. Use *Clear all* to delete them.
* **Battery**: the "keep awake" option keeps the back screen on while the view is showing. Turn it off if you
  only want to glance. Xiaomi's screen then falls back to its clock after about 10 seconds.
* After a HyperOS update Xiaomi could change this behaviour. If *Show on back screen* stops working,
  check the log at the bottom of the app.
* If Xiaomi's own back screen stays black after you return, lock and unlock the phone once.

## Without Shizuku (from a computer with ADB)
`scripts/send-to-back.sh` does the same move from a PC over USB.

## Credits
The back-screen move technique was discovered by
[MiRearScreenSwitcher](https://github.com/AntiOblivionis/MiRearScreenSwitcher) and documented by
[xiaomi-rear-vibe](https://github.com/ranshuo-ICer/xiaomi-rear-vibe). Measured back-screen size: 976 × 596 px,
with the cameras over the left 296 px.
