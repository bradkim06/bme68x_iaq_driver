# Bosch BME680 Device Driver Sample

See Detail https://bradkim06.github.io/nordic_connect_sdk/bme68x/

## Quick Start

1. add device bosch,bme68x in your dts or overlay file like below

```
i2c: &i2c0 {
	compatible = "nordic,nrf-twim";
	status = "okay";
	clock-frequency = <I2C_BITRATE_FAST>;

	pinctrl-0 = <&i2c0_default>;
	pinctrl-1 = <&i2c0_sleep>;
	pinctrl-names = "default", "sleep";

	bme68x:bme68x@76 {
		compatible = "bosch,bme68x";
		status = "okay";
		friendly-name = "bosch environment sensor";
		reg = <0x76>;
	};
};
```

2. build & flash

```
west build -b {your_board_name}
west flash
```

3. See Log Output

```
[00:05:30.973,541] <inf> bme680: temp: 22.769145°C; press: 101308.554687Pa; humidity: 40.439014%
[00:05:30.973,541] <inf> bme680: iaq: 55(acc:1); CO2: 512ppm VOC: 0ppm
```

## Configuration

- CONFIG_SETTINGS : Configure the Kconfig option and a settings backend to save the persistent state of the BSEC library.
- CONFIG_BME68X : To enalbe this driver.
- CONFIG_BME68X_IAQ : To enable driver iaq measuring.

## Referecne Code

[BME68X IAQ driver Document](https://developer.nordicsemi.com/nRF_Connect_SDK/doc/2.4.99-dev2/nrf/drivers/bme68x_iaq.html)
