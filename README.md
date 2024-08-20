# Near-Field-Propagation-Simulator
"X" is an open-source 2D simulator for modeling the electromagnetic wave near field propagation of large transmitter antennas (especially in THz and sub-THz frequencies) in the presence of arbitrary blockages and reflectors in the environment. Terahertz (THz) communications are envisioned to be a key technology in 6G and beyond wireless systems, enabling the demanding high data rates (100 Gbs) and large bandwidths. The large array aperture and high carrier frequencies in the THz band result in a large Rayleigh distance (over 10 meters), which positions most communication applications in the near-field region of the transmitter (Tx) antennas, where the traditional plane-wave assumption is no longer valid. Moreover, the severe propagation loss and blockage issues inherent in the THz band present significant challenges, hindering the system's ability to utilize the available bandwidth effectively. One of the fundamental tools to alleviate these problems and facilitate network optimization and planning is coverage mapping through received power prediction in different locations. However, traditional models developed based on far-field assumptions would fail to capture the near-field characteristics accurately, and running computationally intensive EM simulations on the base stations is not feasible, making effective power prediction extremely challenging for these systems. In this simulator, we provide accurate and efficient modeling of near-field propagation of TX antennas configured with arbitrary phase configurations and locations in interactions with arbitrary numbers of reflectors/blockages with different environmental properties. In this simulator, we provide options to generate interesting and special wavefronts introduced in the near field like Airy beam, Bessel beam, etc., or input user-defined phase configurations for TX antenna elements. Furthermore, "X" supports Reconfigurable Intelligent Surfaces (RIS) and rough scattering to model the near-field propagation. Ultimately, one can define the multiple RX properties as in a multiple UEs scenario to get the calculated power at each RX location on top of the coverage map. We have developed this simulator based on the physical principles of Rayleigh-Sommerfeld Integral Theory and Angular Spectrum Method and evaluate its performance by comparing the results generated from this simulator with a comprehensive EM simulator namely "Feko". The main purpose of this simulator is to provide a user-friendly interface to study the near field propagation model of large TX antenna arrays which are envisioned to be the key technology in the next generations of communication systems and more importantly provide an infrastructure to generate a significant amount of data for AI-enabled solutions. 

## Starting up the Graphic User Interface
In order to work directly with the GUI, you need to pull this repository and open up the 	**main_app.mlapp** in **appdesigner** in MATLAB. appdesigner environment can be opened by running the `appdesigner` in the MATLAB command line. The main app can be set up by easily just running the program.

![startingup](/media/startingup.PNG)
## Setting Up Environmental Properties
In the first part of the program, one can create the environment of interest by choosing the resolution and dimension and adding as many blockages/reflectors with arbitrary properties to the environment.

![Environment](/media/environment.PNG)

## Adding Reflector/Blockage
In order to add a reflector/blockage, one can click on the **Add New Reflector/Blocker** which would pop up a new window. In the new window, the user can define the location and orientation of the object (within the defined dimensions) along with the length and thickness of the object in the environment. **Power Ratio** determines the amount of power being reflected back with respect to the incident E field power. The power ratio of 1 represents perfect reflection, while the power ratio of 0 represents complete blockage (absorber). Furthermore, there are options to consider diffuse scattering by adding roughness parameters and also to place Reconfigurable Intelligent Surfaces as the reflectors by adding a text file that contains the designed phase shifts on the elements of the RIS. By determining the statistical properties of a rough surface $h_rms$ and $L_c$, the code would generate a random surface perturbation and it would be translated to the phase shifts introduced by rough scattering. An example text file to configure a reflector as RIS is included in the main folder, which represents the phase shifts of a rough surface, so by adding the RIS to the environment you would see the rough scattering behavior.

<img src="/media/object.PNG" alt="object" width="400" style="float: left; margin-right: 10px;"/>

## TX Antenna Array Configuration
In order to configure TX antenna arrays, one should determine the frequency at which the simulation is intended to calculate near-field propagation. It should be noted that the resolution defined in environmental properties must be large enough to sample points with spacing less than half a wavelength $d<\lambda/2$. The default option to configure a TX array assumes the TX to be centered at $Y=0$ and the user can define the TX aperture in mm and also the phase configuration by choosing one of the built-in beam types namely as **Beam Steering**, **Focused Beam**, **Airy Beam**, and **Bessel Beam** and set the corresponding parameters. The other option is to set the phase configuration of TX array elements (centered at &Y=0&) manually by importing a text file containing the phase information. The third option is to add multiple TX antenna arrays at different locations in the $X=0$ plane and configure them with arbitrary phase configurations. It should be noted that the resolution of the input E field in the manual setting should be equal to the defined environment resolution. An example text file with 5000 resolution can be found in the main folder. The example E field represents two TX antenna arrays with -45 and 35 degree beam steering angles located at 0.5m and -0.5m.

<img src="/media/tx_env.PNG" alt="tx_env" width="500" style="float: left; margin-right: 10px;"/>
<img src="/media/tx.PNG" alt="tx" width="300" style="float: left; margin-right: 10px;"/>

## Adding Multiple RX Antenna Arrays
By clicking on the **Add New RX** button, one can configure the RX antenna dimension, location, orientation, and its number of elements to calculate the received power at the multi-UE scenario by running the simulation once. In default the RX antenna is assumed to be fully digital, however, one can set it to be an analog antenna array by importing the corresponding phase configurations as a text file.

<img src="/media/rx_env.PNG" alt="rx_env" width="500" style="float: left; margin-right: 10px;"/>
<img src="/media/rx.PNG" alt="rx" width="300" style="float: left; margin-right: 10px;"/>

## Coverage Map and Received Power
After running the simulation the calculated coverage map resulting from near field propagation would be visualized and saved as a text file containing the E field at each location based on the pre-defined resolution. One can change the coverage map visualization mode to be based on normalized magnitude or in db. For more options, you can right-click on the color bar in the figure.  

## AI-enabled System Design
This simulator is a perfect tool to collect data for AI-enabled solutions for different applications of near-field propagation. One can easily make scripts to collect data for various purposes, due to the source code availability of the core simulator. One example of generating a coverage map by interacting with the core near field propagation modeling function can be seen in **func_test.m** file. For more advanced settings you can also refer to the main function **near_field_propagation.m**.
