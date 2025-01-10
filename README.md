# BLEarrings Embedded Solution

::: {.contents local="" depth="2"}
:::

The peripheral LBS sample demonstrates how to use the
`lbs_readme`{.interpreted-text role="ref"}.

## Requirements

The sample supports the following development kits:

::: table-from-sample-yaml :::

The sample also requires a smartphone or tablet running a compatible
mobile application. The [Testing](#testing) instructions refer to [nRF
Connect for Mobile](), but you can also use other similar applications
(for example, [nRF Blinky]() or [nRF Toolbox]()).

::: note
::: title
Note
:::
:::

## Overview

You can use the sample to transmit the button state from your
development kit to another device.

::: tabs
::: group-tab
nRF52 and nRF53 DKs

When connected, the sample sends the state of **Button 1** on the
development kit to the connected device, such as a phone or tablet. The
mobile application on the device can display the received button state
and control the state of **LED 3** on the development kit.
:::

::: group-tab
nRF54 DKs

When connected, the sample sends the state of **Button 0** on the
development kit to the connected device, such as a phone or tablet. The
mobile application on the device can display the received button state
and control the state of **LED 2** on the development kit.
:::
:::

You can also use this sample to control the color of the RGB LED on the
nRF52840 Dongle or Thingy:53.

## User interface

The user interface of the sample depends on the hardware platform you
are using.

::: tabs
::: group-tab
nRF52 and nRF53 DKs

LED 1:

:   Blinks when the main loop is running (that is, the device is
    advertising) with a period of two seconds, duty cycle 50%.

LED 2:

:   Lit when the development kit is connected.

LED 3:

:   Lit when the development kit is controlled remotely from the
    connected device.

Button 1:

:   Send a notification with the button state: \"pressed\" or
    \"released\".
:::

::: group-tab
nRF54 DKs

LED 0:

:   Blinks when the main loop is running (that is, the device is
    advertising) with a period of two seconds, duty cycle 50%.

LED 1:

:   Lit when the development kit is connected.

LED 2:

:   Lit when the development kit is controlled remotely from the
    connected device.

Button 0:

:   Send a notification with the button state: \"pressed\" or
    \"released\".
:::

::: group-tab
Thingy:53

RGB LED:

:   The RGB LED channels are used independently to display the following
    information:

    -   Red - If the main loop is running (that is, the device is
        advertising). The LED blinks with a period of two seconds, duty
        cycle 50%.
    -   Green - If the device is connected.
    -   Blue - If user set the LED using Nordic LED Button Service.

    For example, if Thingy:53 is connected over Bluetooth, the LED color
    toggles between green and yellow. The green LED channel is kept on
    and the red LED channel is blinking.

Button 1:

:   Send a notification with the button state: \"pressed\" or
    \"released\".
:::

::: group-tab
nRF52840 Dongle

Green LED:

:   Blinks, toggling on/off every second, when the main loop is running
    and the device is advertising.

RGB LED:

:   The RGB LED channels are used independently to display the following
    information:

    -   Red - If Dongle is connected.
    -   Green - If user set the LED using Nordic LED Button Service.

Button 1:

:   Send a notification with the button state: \"pressed\" or
    \"released\".
:::
:::

## Building and running

::: note
::: title
Note
:::
:::

### Minimal build

You can build the sample with a minimum configuration as a demonstration
of how to reduce code size and RAM usage, using the
`-DFILE_SUFFIX=minimal` flag in your build.

See `cmake_options`{.interpreted-text role="ref"} for instructions on
how to add this option to your build. For example, when building on the
command line, you can add the option as follows:

``` console
west build samples/bluetooth/peripheral_lbs -- -DFILE_SUFFIX=minimal
```

### Testing {#peripheral_lbs_testing}

After programming the sample to your dongle or development kit, one of
the LEDs starts blinking to indicate that the advertising loop is active
(see [User interface](#user-interface) for details).

To test the sample using the [nRF Connect for Mobile]() application,
complete the following steps:

::: tabs
::: group-tab
nRF52 and nRF53 DKs

1.  Install and start the [nRF Connect for Mobile]() application on your
    smartphone or tablet.

2.  Power on the development kit or insert your dongle into the USB
    port.

3.  Connect to the device from the application. The device is
    advertising as `Nordic_LBS`. The services of the connected device
    are shown.

4.  In **Nordic LED Button Service**, enable notifications for the
    **Button** characteristic.

5.  Press **Button 1** on the device.

6.  Observe that notifications with the following values are displayed:

    -   `Button released` when **Button 1** is released.
    -   `Button pressed` when **Button 1** is pressed.

7.  Write the following values to the LED characteristic in the **Nordic
    LED Button Service**. Depending on the hardware platform, this
    produces results described in the table.

      -----------------------------------------------------------------------
      Hardware platform     Value    Effect
      --------------------- -------- ----------------------------------------
      nRF52 and nRF53 DKs   `OFF`    Switch the **LED 3** off.

      -----------------------------------------------------------------------

    \+
    +\-\-\-\-\-\-\-\--+\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--+
    \| \| `ON` \| Switch the **LED 3** on. \|
    +\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--+\-\-\-\-\-\-\-\--+\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--+
    \| nRF52840 Dongle \| `OFF` \| Switch the green channel of the RGB
    LED off. \|

    \+
    +\-\-\-\-\-\-\-\--+\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--+
    \| \| `ON` \| Switch the green channel of the RGB LED on. \|
    +\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--+\-\-\-\-\-\-\-\--+\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--+
    \| Thingy:53 \| `OFF` \| Switch the blue channel of the RGB LED off.
    \|

    \+
    +\-\-\-\-\-\-\-\--+\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--+
    \| \| `ON` \| Switch the blue channel of the RGB LED on. \|
    +\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--+\-\-\-\-\-\-\-\--+\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--+
:::

::: group-tab
nRF54 DKs

::: note
::: title
Note
:::
:::

1.  Install and start the [nRF Connect for Mobile]() application on your
    smartphone or tablet.

2.  Power on the development kit or insert your dongle into the USB
    port.

3.  Connect to the device from the application. The device is
    advertising as `Nordic_LBS`. The services of the connected device
    are shown.

4.  In **Nordic LED Button Service**, enable notifications for the
    **Button** characteristic.

5.  Press **Button 0** on the device.

6.  Observe that notifications with the following values are displayed:

    -   `Button released` when **Button 0** is released.
    -   `Button pressed` when **Button 0** is pressed.

7.  Write the following values to the LED characteristic in the **Nordic
    LED Button Service**. Depending on the hardware platform, this
    produces results described in the table.

      -----------------------------------------------------------------------
      Hardware platform     Value    Effect
      --------------------- -------- ----------------------------------------
      nRF54 DKs             `OFF`    Switch the **LED 2** off.

      -----------------------------------------------------------------------

    \+
    +\-\-\-\-\-\-\-\--+\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--+
    \| \| `ON` \| Switch the **LED 2** on. \|
    +\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--+\-\-\-\-\-\-\-\--+\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--+
:::
:::

## Dependencies

This sample uses the following libraries:

-   `lbs_readme`{.interpreted-text role="ref"}
-   `dk_buttons_and_leds_readme`{.interpreted-text role="ref"}

In addition, it uses the following Zephyr libraries:

-   `include/zephyr/types.h`{.interpreted-text role="file"}
-   `lib/libc/minimal/include/errno.h`{.interpreted-text role="file"}
-   `include/sys/printk.h`{.interpreted-text role="file"}
-   `include/sys/byteorder.h`{.interpreted-text role="file"}
-   `GPIO Interface <zephyr:api_peripherals>`{.interpreted-text
    role="ref"}
-   `zephyr:bluetooth_api`{.interpreted-text role="ref"}:
    -   `include/bluetooth/bluetooth.h`{.interpreted-text role="file"}
    -   `include/bluetooth/hci.h`{.interpreted-text role="file"}
    -   `include/bluetooth/conn.h`{.interpreted-text role="file"}
    -   `include/bluetooth/uuid.h`{.interpreted-text role="file"}
    -   `include/bluetooth/gatt.h`{.interpreted-text role="file"}

The sample also uses the following secure firmware component:

-   `Trusted Firmware-M <ug_tfm>`{.interpreted-text role="ref"}
