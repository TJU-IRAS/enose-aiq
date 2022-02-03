# Pre-concentrator Hardware


## Preview

<img src="https://github.com/TJU-IRAS/enose-aiq/blob/main/documents/pics/pre-concentrator.jpg"  style="zoom: 10%;" />



## Thermostat Module

The instrument indeed has a **closed-loop temperature control system** to maintain the working temperature of the pre-concentrator. The control module has a measuring unit to monitor the temperature of the adsorption tube, including a K-Thermocouple inside the metal coil heater (wrapping the adsorbent container), and a MAX6675 chip acquiring the signals of the K-Thermocouple. The control board (STM32) of the pre-concentrator reads the temperature from MAX6675 through SPI, control the metal coil heater through a (silicon controlled) SCR, and control the 12V cooling fan by a relay. The control board integrates a **PID temperator control algorithm**, to keep proper temperature during working (523K when adsorption, and 300K when desorption). The scheme of the temperature control system is shown in Fig.1.


<img src="https://github.com/TJU-IRAS/enose-aiq/blob/main/documents/pics/Thermostat.png"  style="zoom: 10%;" />

Fig.1 The temperature control module of the pre-concentrator

The gas temperature and humidity will surely affect the measurement of the MOS sensors; therefore, it is crucial to maintain consistent gas temperature and humidity at the sensing module (where reaction with the sensors goes on). Since the target gas is preprocessed by the same pre-concentrating workflow, yielding gas at similar temperature and humidity, which guarantee the consistency of the gas condition at the sensing module. As the desorbed gas’ high temperature will influence the sensing effect of MOS sensors, we have proposed a temperature compensation algorithm in [1], which will also be added in the details at the online supplements.

[1] Cheng Lu, Meng Qinghao. Temperature compensation methods for an electronic nose pre-concentrator. Chinese Journal of Scientific Instrument. 2020, 41(1)

