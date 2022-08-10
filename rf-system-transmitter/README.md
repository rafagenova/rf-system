# radio frequency system for sending and reception of data

## 1. NRF905 notes

### &bull; nrf905 timing to obey info

| nrf905 timing    |   max    |    
| ----------- |   ----------- |
| power down mode to standby mode |   3 ms    |
| standby mode to TX shock burst mode |   650 us    |
| standby mode to RX shock burst mode |   650 us    |
| RX shock burst mode to TX shock burst mode |   550 us    |
| TX shock burst mode to RX shock burst mode |   550 us    |

### &bull; nrf905 modulation
the modulation of nRF905 is Gaussian Frequency Shift Keying (GFSK) with a datarate of 100kbps.
</br> the data is internally Manchester encoded (TX) and Manchester decoded (RX).

### &bull; nrf905 output frequency

Output Frequency
The operating RF-frequency of nRF905 is set in the configuration register by CH_NO and HFREQ_PLL.

| operating frequency|
| ----------- | 
| <i> f = (422.4 + (CH_NO)/10)&bull; (1 + HFREQ_PLL) MHz </i>| 

<i> obs1: CH_NO varies from '000000000' to '1111111111' </i>

<i> obs2: HFREQ_PLL varies from '0' to '1' </i>

| Operating frequency    |   HFREQ_PLL    |    CH_NO   | 
| ----------- |   ----------- | ----------- |
| 430.0 MHz |  [0]   | [001001100]  |
| 433.1 MHz |  [0]   | [001101011]  |
| 433.2 MHz |  [0]   | [001101100]  |
| 434.7 MHz |  [0]   | [001111011]  |
| 862.0 MHz |  [1]   | [001010110]  |
| 868.2 MHz |  [1]   | [001110101]  |
| 868.4 MHz |  [1]   | [001110110]  |
| 869.8 MHz |  [1]   | [001111101]  |
| 902.2 MHz |  [1]   | [100011111]  |
| 902.4 MHz |  [1]   | [100100000]  |
| 927.8 MHz |  [1]   | [110011111]  |

### &bull; nrf905 antenna ports impedance

| optimum differential load impedance at the antenna ports|   frequency    | 
| ----------- | ----------- |
| 225&Omega; + j210 |  900MHz    | 
| 300&Omega; + j100 |  430MHz   | 

<i> obs: a low load impedance (for instance 50&Omega;) can be obtained by fitting a simple matching network or a RF transformer (balun) </i>

### &bull; PCB layout and decoupling guidelines

<i> 

1. A PCB with a minimum of two layers including a ground plane is recommended for optimum performance.

2. The nRF905 DC supply voltage should be decoupled as close as possible to the VDD pins with high performance RF capacitors.

3. It is preferable to mount a large surface mount capacitor (e.g. 4.7uF tantalum) in parallel with the smaller value capacitors.

4. The nRF905 supply voltage should be filtered and routed separately from the supply voltages of any digital circuitry.

5. Long power supply lines on the PCB should be avoided.

6. All device grounds, VDD connections and VDD bypass capacitors must be connected as close as possible to the nRF905 IC.

7. For a PCB with a topside RF ground plane, the VSS pins should be connected directly to the ground plane.

8. For a PCB with a bottom ground plane, the best technique is to place via holes as close as possible to the VSS pins (a minimum of one via hole should be used for each VSS pin).

9. Full swing digital data or control signals should not be routed close to the crystal or the power supply lines.

10. A fully qualified RF-layout for the nRF905 and its surrounding components, including antennas and matching networks, can be downloaded from <b> www.nordicsemi.no. </b>

</i>

| nrf905 features    |   description    |    
| ----------- |   ----------- |
| &bull; Carrier detect |   When the nRF905 is in ShockBurst TM RX, the Carrier Detect (CD) pin is set high if a RF carrier is present at the channel the device is programmed to. </br > </br > This feature is very effective to avoid collision of packages from different transmitters operating at the same frequency. </br > </br > Whenever a device is ready to transmit it could first be set into receive mode and sense whether or not the wanted channel is available for outgoing data.    |
| &bull; Address match |   When the nRF905 is in ShockBurst TM RX mode, the Address Match (AM) pin is set high as soon as an incoming package with an address that is identical with the device’s own identity is received. </br > </br > If Address Match (AM) is high then the MCU can make a decision to wait and see if Data Ready (DR) will be set high indicating a valid data package has been received or ignore that a possible package is being received and switch modes.|
|  &bull; Data ready |   In ShockBurst TM TX Auto Retransmit the Data Ready (DR) signal is set high at the beginning of the pre-amble and is set low at the end of the preamble. The Data Ready (DR) signal therefore pulses at the beginning of each transmitted data packet.  </br > </br > In ShockBurst TM RX, the signal is set high when nRF905 has received a valid package, i.e. a valid address, package length and correct CRC. The MCU can then retrieve the payload via the SPI interface. The Data Ready (DR) pin is reset to low once the data has been clocked out of the data buffer or the device is switched to transmit mode.|
|  &bull; Auto retransmit |   One way to increase system reliability in a noisy environment or in a system without collision control is to transmit a package several times. </br > </br > By setting the AUTO_RETRAN bit to “1” in the configuration register, the circuit keeps sending the same data package as long as TRX_CE and TX_EN is high.|

### &bull; nrf905 schematic example

![Alt text](images/nrf905schematic.png?raw=true "Title")

## 2. Components & schematics

### &bull; voltage regulator (3.7v battery to 3.3v system)

| 3.3V LDO    |   packacge    |    comments |
| ----------- |   ----------- |  ----------- |
| MCP1700T-3302E/TT |  SOT-23-3   |46 in stock at JLCPCB @ 30/05 <br /> Max current of 250 mA <br /> Max dropout voltage of 350 mV |

### &bull; power input schematic

![Alt text](images/power-input-schematic.png?raw=true "Title")

### &bull; transceiver schematic

![Alt text](images/transceiver-schematic.png?raw=true "Title")