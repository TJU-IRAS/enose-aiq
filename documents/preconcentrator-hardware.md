# Pre-concentrator Hardware


## Preview

<img src="https://github.com/TJU-IRAS/enose-aiq/blob/main/documents/pics/pre-concentrator.jpg" width="400" height="400" />

Fig.1 The internal photo of the pre-concentrator


## Thermostat Module

The instrument indeed has a **closed-loop temperature control system** to maintain the working temperature of the pre-concentrator. The control module has a measuring unit to monitor the temperature of the adsorption tube, including a K-Thermocouple inside the metal coil heater (wrapping the adsorbent container), and a MAX6675 chip acquiring the signals of the K-Thermocouple. The control board (STM32) of the pre-concentrator reads the temperature from MAX6675 through SPI, control the metal coil heater through a (silicon controlled) SCR, and control the 12V cooling fan by a relay. The control board integrates a **PID temperator control algorithm**, to keep proper temperature during working (523K when adsorption, and 300K when desorption). The scheme of the temperature control system is shown in Fig.2.


<img src="https://github.com/TJU-IRAS/enose-aiq/blob/main/documents/pics/Thermostat.png" width="400" height="400" />

Fig.2 The temperature control module of the pre-concentrator

The gas temperature and humidity will surely affect the measurement of the MOS sensors; therefore, it is crucial to maintain consistent gas temperature and humidity at the sensing module (where reaction with the sensors goes on). Since the target gas is preprocessed by the same pre-concentrating workflow, yielding gas at similar temperature and humidity, which guarantee the consistency of the gas condition at the sensing module. As the desorbed gas’ high temperature will influence the sensing effect of MOS sensors, we have proposed a temperature compensation algorithm in [1], which will also be added in the details at the online supplements.

[1] Cheng Lu, Meng Qinghao. Temperature compensation methods for an electronic nose pre-concentrator. Chinese Journal of Scientific Instrument. 2020, 41(1)

## MOS sensors sampling sequence

Eight MOS sensors’ digitized responses are sampled serially, equally, channel-by-channel, based on the Serial Peripheral Interface (SPI). The order of eight channel does not affect the sampling and grading results, thus no priority need to be considered for the eight sensors.
The eight MOS sensors are deployed in the sensing module circuit following their own datasheets, converting the gas concentration response to a corresponding voltage output (0~5V). The eight voltage outputs are sampled by an analog to digital converter (ADC): AD7606, which is a 16-bit ADC with eight input channels and 200k-SPS (samples per second) sampling rate on all channels. The processing module’s BeagleBone BlackBoard communicates with the AD7606 through SPI0, and serially reads converted results (2 bytes per channel for one sample) of all channels. The sampling rate is 300Hz, and the sampling procedure is conducted in the interrupt function of the AM3358 Timer0. The sampling sequence diagram is shown in Fig.3.

<img src="https://github.com/TJU-IRAS/enose-aiq/blob/main/documents/pics/AD-TimeSequence.png" width="400" height="400" />

Fig.3 Time sequence of MOS sensors sampling



