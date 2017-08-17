ZX Sensor driver for Android Things
===================================

This driver supports ZXSensor peripherals using the I2C and UART protocols.

How to use the driver
---------------------

### Gradle dependency

To use the `zxsensor` driver, simply add the line below to your project's `build.gradle`,
where `<version>` matches the last version of the driver available on [jcenter][jcenter].

```
dependencies {
    compile 'com.blundell:driver-zxsensor:<version>'
}
```

### Sample usage

```java
import com.blundell.zxsensor.ZxSensor;
import com.blundell.zxsensor.ZxSensorUart;

// Access the ZXSensor (choose I2C or UART) here we show UART:

ZxSensorUart zxSensorUart;

try {
    zxSensorUart = ZxSensor.Factory.openViaUart(BoardDefaults.getUartPin());
} catch (IOException e) {
    throw new IllegalStateException("Can't open, did you use the correct pin name?", e);
}
zxSensorUart.setSwipeLeftListener(swipeLeftListener);
zxSensorUart.setSwipeRightListener(swipeRightListener);

ZxSensor.SwipeLeftListener swipeLeftListener = new ZxSensor.SwipeLeftListener() {
        @Override
        public void onSwipeLeft(int speed) {
            Log.d("TUT", "Swipe left detected");
        }
    };

ZxSensor.SwipeRightListener swipeRightListener = new ZxSensor.SwipeRightListener() {
        @Override
        public void onSwipeRight(int speed) {
            Log.d("TUT", "Swipe right detected");
        }
    };

// Start monitoring:

zxSensorUart.startMonitoringGestures();

// Stop monitoring:

zxSensorUart.stopMonitoringGestures();

// Close the ZXSensor when finished:

zxSensorUart.close();
```


[jcenter]: https://bintray.com/blundell/maven/driver-zxsensor/_latestVersion
