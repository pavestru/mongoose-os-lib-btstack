# BTstack library wrapped for Mongoose OS

This is [BTstack](https://github.com/bluekitchen/btstack/) (bluetooth stack) [repackaged for ESP32](https://github.com/bluekitchen/btstack/tree/master/port/esp32) and wrapped as a [Mongoose OS](https://mongoose-os.com/) lib. Please, follow [Bluekitchen](http://bluekitchen-gmbh.com/)'s terms of use and license (free for non-commercial use).

## Process of creating this lib

  - Follow the guide for [Setup and Usage for ESP32 port of BTstack](https://github.com/bluekitchen/btstack/tree/master/port/esp32), including setting up esp-idf toolchain. As a result, BTstack should be found inside `$IDF_PATH/components/btstack` folder.
  - Build an example in `port/esp32/examples/` to see if it works and to use sdkconfig file later for reference.
  - Create directory for the lib and copy the contents of `$IDF_PATH/components/btstack` inside `src/esp32` subdirectory of the lib directory.
  - Create `mos.yml` according to spec for mongoose-os libraries.
  - Open `src/esp32/component.mk` file and copy paths from `COMPONENT_ADD_INCLUDEDIRS` and `COMPONENT_SRCDIRS` into `includes:` and `sources:` inside `mos.yml` file, respectively. (Watch for the tab characters when copying - yaml only supports spaces).
  - Configure `mos_esp32.yml` by using necessary SDKCONFIG_OPTS. See configured sdkconfig in ESP32 port of BTstack for reference.
  - Rename `app_main` function to `mgos_mongoose_os_lib_btstack_init` in `src/esp32/main.c`.
  - Extract the code inside `mgos_mongoose_os_lib_btstack_init` function to a separate function and make it run in a separate task using `xTaskCreate` (from `freertos/task.h`).