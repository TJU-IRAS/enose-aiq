# The sensing module



## MOS sensors sampling sequence

Eight MOS sensors’ digitized responses are sampled serially, equally, channel-by-channel, based on the Serial Peripheral Interface (SPI). The order of eight channel does not affect the sampling and grading results, thus no priority need to be considered for the eight sensors.
The eight MOS sensors are deployed in the sensing module circuit following their own datasheets, converting the gas concentration response to a corresponding voltage output (0~5V). The eight voltage outputs are sampled by an analog to digital converter (ADC): AD7606, which is a 16-bit ADC with eight input channels and 200k-SPS (samples per second) sampling rate on all channels. The processing module’s BeagleBone BlackBoard communicates with the AD7606 through SPI0, and serially reads converted results (2 bytes per channel for one sample) of all channels. The sampling rate is 300Hz, and the sampling procedure is conducted in the interrupt function of the AM3358 Timer0. The sampling sequence diagram is shown in Fig.3.

<img src="https://github.com/TJU-IRAS/enose-aiq/blob/main/documents/pics/AD-TimeSequence.png" width="400" height="400" />

Fig.3 Time sequence of MOS sensors sampling