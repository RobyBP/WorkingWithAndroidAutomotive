# Car Hardware APIs

Starting with Car App API level 3, the Car App Library has APIs that you can use to access vehicle properties and sensors.
## Requirements

Add a dependency on `androidx.car.app:app-automotive` to the `build.gradle` file for your Android Automotive OS module.

Additionally, in you `AndroidManifest.xml` file, you need to [declare relevant permissions](https://developer.android.com/training/permissions/declaring) needed to request the car data you want to use. Note that these permissions must also be granted to you by the user. For more information, check out the [runtime permissions documentation](https://developer.android.com/training/permissions/requesting)

## Adding property listeners

To access vehicle information, you need to retrieve an instance of the `CarHardwareManager` class:

```kotlin
val carInfo = carContext.getCarService(CarHardwareManager::class.java).carInfo
```

Create a property listener using the `OnCarDataAvailableListener` interface. This listener captures the updates and changes to the energy level property.
You can find the list of available listener in the [official documentation](https://developer.android.com/reference/androidx/car/app/hardware/info/CarInfo#public-methods_1)

```kotlin
val listener = OnCarDataAvailableListener<EnergyLevel> { data ->
    if (data.rangeRemainingMeters.status == CarValue.STATUS_SUCCESS) {
        val rangeRemaining = data.rangeRemainingMeters.value
        // Perform actions based on the updated energy level
    } else {
        // Handle error, such as displaying an error message
    }
}
```

Add the defined property listener to `carInfo`.

```kotlin
carInfo.addEnergyLevelListener(carContext.mainExecutor, listener)
```

The `carContext.mainExecutor` ensures that the listener executes on the main thread, avoiding potential threading issues.

If at any point you no longer require the property updates, it's recommended to remove the listener to conserve resources.

```kotlin
carInfo.removeEnergyLevelListener(listener)
```
