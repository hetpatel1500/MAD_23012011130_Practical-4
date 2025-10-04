
# MAD_23012011130_Practical4 — Alarm using Foreground Service (Kotlin)

A basic Android application that allows you to select a time for an alarm. When the alarm goes off, a foreground service is launched, displays a high-importance notification, and continuously plays an alarm tone until you stop it.


## How to use

* Tap **"Create Alarm"** and choose a time.
* A card showing the scheduled alarm will appear.
* To cancel or stop, press **"Cancel Alarm"**.

## How it works (overview)

* **MainActivity** opens a TimePicker and sets an exact alarm through `AlarmManager` using a `PendingIntent` that targets a `BroadcastReceiver`.
* **AlarmBroadcastReceiver** catches the broadcast and triggers the `AlarmServices`. On Android O and above, it relies on `startForegroundService` for proper behavior.
* **AlarmServices** is a foreground service. It:

  * Makes a notification channel (for O+),
  * Shows an ongoing, high-priority notification,
  * Uses `MediaPlayer` to loop the default alarm sound,
  * Stops playback and clears resources when canceled.

## Permissions and Android requirements

* **Exact alarms**: The manifest includes `SCHEDULE_EXACT_ALARM`. On Android 12+ (API 31), the system may prompt the user to allow exact alarms.
* **Notifications**: On Android 13+ (API 33), the app must ask for `POST_NOTIFICATIONS` permission at runtime so that the service’s notification is visible.

## Build & Run

* SDK: `minSdk` 24, `targetSdk/compileSdk` 36.
* Open in Android Studio (Giraffe or later recommended) and test on a phone/emulator with sound enabled.
* On first launch in Android 12+, you may be asked to grant exact alarm access. On Android 13+, you’ll also be asked for notification permission.

## Project Components

* **MainActivity.kt** — UI handling and alarm setup (`setExactAndAllowWhileIdle` for API 23+).
* **AlarmBroadcastReceiver.kt** — Connects AlarmManager to the service, safely starts/stops it across versions.
* **AlarmServices.kt** — Foreground service showing notification and playing the alarm sound.
* **AndroidManifest.xml** — Declares permissions, service, and receiver.

## Additional Notes

* If the chosen time is earlier than the current time, the app automatically sets it for the next day.
* Alarms are not preserved after a reboot in this sample project.
* If you don’t hear the sound, check that the device’s alarm/notification volume is high enough.

## Screenshots

<div style="display: flex; gap: 10px;">
<img width="270" height="600" alt="Screenshot_20250930_194502" src="https://github.com/user-attachments/assets/ef734cdd-2db3-4a09-bf7b-bc4522346081" />
 <img width="270" height="600" alt="Screenshot_20250930_194657" src="https://github.com/user-attachments/assets/4596441f-73e5-4d66-b383-fd7f72c54a20" />
 <img width="270" height="600" alt="Screenshot_20250930_194709" src="https://github.com/user-attachments/assets/f14eb9f1-cae9-4ec9-a6b1-d50514effcd0" />
</div>
