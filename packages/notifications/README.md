# notifications

[![pub package](https://img.shields.io/pub/v/notifications.svg)](https://pub.dartlang.org/packages/notifications)

A plugin for tracking notifications on the device. Works exclusively for Android.

## Installation
Add ```notifications``` as a dependency in  `pubspec.yaml`.
For help on adding as a dependency, view the [documentation](https://flutter.io/using-packages/).

## Usage

### Android: Register service in the manifest 
The plugin uses an Android system service to track notifications. 
To allow this service to run the following code should be put imn the Android manifest, 
between the `<application></application>` tags.
```xml
<service android:name="cachet.plugins.notifications.NotificationListener"
    android:label="notifications"
    android:permission="android.permission.BIND_NOTIFICATION_LISTENER_SERVICE">
    <intent-filter>
        <action android:name="android.service.notification.NotificationListenerService" />
    </intent-filter>
</service>
```

### Flutter: Listen to notification events
```dart
Notifications notifications = new Notifications();
StreamSubscription<NotificationEvent> events;
events = notifications.noiseStream.listen(onData);
```

Where the `onData()` method handles the incoming `NotificationEvents`. An example could be:
```dart
void onData(NotificationEvent event) => print(event.toString());
```