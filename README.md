# BME68x (I2C) - STM32 HAL and BME68x API Based Library
A simple C library based on BME68x API and STM32 HAL for Bosch Sensortec BM68x series of sensors with I2C interface. (Tested on STM32F411RE)

This library measures temperature, humidity, pressure and IAQ with BME680x (I2C) sensors based on STM32 HAL and BME68x API.

* For more information about BME68x API check: https://github.com/BoschSensortec/BME68x-Sensor-API
* For more information about the IAQ calculation check: https://github.com/G6EJD/BME680-Example

## Example Usage
1) Configure an I2C peripheral on CubeMX,
2) Copy library files to the project directory,
3) Include the library,
```c
/* USER CODE BEGIN Includes */

#include <bme680/bme68x_necessary_functions.h>

/* USER CODE END Includes */
```
4) Initialise the library,
```c
/* USER CODE BEGIN 2 */

	/* BME680 API forced mode test */
	struct bme68x_data data;
	bme68x_start(&data, &hi2c1);

/* USER CODE END 2 */
```
5) Make the measurement and calculate the IAQ,
```c
if (bme68x_single_measure(&data) == 0) {

	// Measurement is successful, so continue with IAQ
	data.iaq_score = bme68x_iaq(); // Calculate IAQ
	
	HAL_Delay(2000);
}
```
6) Data is now available in the bme6x_data structure (The variable 'data'),
```c
data.temperature
data.pressure
data.humidity
data.gas_resistance
data.iaq_score
```

## Licensing
Library Name: 	BME68x (I2C) - STM32 HAL and BME68x API Based Library

Written By:	Ahmet Batuhan Günaltay (Great thanks to David Bird for IAQ calculation method and functions.)

Date Written:	26/05/2021 (DD/MM/YYYY)

Last Modified:	26/05/2021 (DD/MM/YYYY)

Description:	This library measures temperature, humidity, pressure and IAQ with BME680x (I2C) sensors based on STM32 HAL and BME68x API. For more information about the IAQ calculation check: https://github.com/G6EJD/BME680-Example

References: https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bme680-ds001.pdf [Datasheet]
 
Copyright (C) 2021 - Ahmet Batuhan Günaltay
(IAQ calculation substantial portion, the ideas and concepts is Copyright (c) David Bird 2018)
 
	This software library is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.

    This software library is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with this program.  If not, see <https://www.gnu.org/licenses/>.
