# <img src="https://github.com/hhumbertoAv/FLOC/assets/6061953/39adf1cb-08eb-4d51-a1fe-5fd26966350e" width="40"/> EcoFloc: Energy Measuring System Tool for Linux

## Acknowledgments

<p align="center">
  <img src="https://github.com/hhumbertoAv/FLOC/assets/6061953/fcd7f192-e585-49f0-b766-137e5224ff72" width="45%"/>
</p>


EcoFloc has been made possible thanks to Technopôle Domolandes[^1], an organization deeply committed to innovation and the development of the Landes region in France and beyond, as well as the Université de Pau et des Pays de l'Adour and Université de Toulouse. These institutions are engaged in advancing research and development in France, contributing significantly to technological progress and regional growth. Their continuous efforts have been instrumental in bringing this project to life.

## Description

EcoFloc is a comprehensive and versatile tool developed by the R&D laboratory of Technopôle Domolandes[^1] and supported by Université de Pau et des Pays de l'Adour and Université de Toulouse. It is designed to measure the energy consumption of applications in GNU/Linux environments. EcoFloc enables users and developers to track energy usage across various software components using a single tool, leveraging existing libraries like RAPL[^2] or power equations. This tool provides capabilities for both real-time energy assessment and long-term monitoring. It supports continuous energy tracking of applications, capable of measuring energy over extended periods even if the applications are closed and subsequently reopened. The initial release includes applications for measuring the energy consumption of hardware components such as CPU, RAM, hard drives, and network cards.



## Features
<p align="justify">
For each component, EcoFloc calculates the energy consumption based on the load generated by running processes identified by their PID. It uses load and energy consumption data provided by the GNU/Linux kernel interfaces or, in their absence, from a database of technical specifications (datasheets) which can be either predefined or customized.
</p>

### Limitations

It is important to note that, as with any software tool that measures hardware energy consumption, there is a margin of variability. The values provided by EcoFloc are approximations and should not be considered absolutely precise.



### Mathematical Formulas and Customization
FLOC includes a set of pre-defined mathematical formulas tailored for the four devices. These formulas have been proven[^3] to reflect the proportion of energy consumption by a process in relation to the total computer usage. Developers and contributors have the flexibility to define and maintain their own formulas, making FLOC a highly adaptable tool for various usage scenarios.


## Technical Specifications

As we mentioned, this initial release of `floc` features four distinct applications, targeting the measurement of power and energy consumption across CPUs, RAM, storage devices, and network interface cards. Each application is in its own folder, where you'll find both the source code and configuration files. This setup not only facilitates easy exploration and customization but also facilitates understanding. While `floc` provides a unified interface to execute all tools collectively, users are still able to delve into each application's specific folder to explore its code, access comprehensive documentation, and make any desired modifications.


### General System Requirements
EcoFloc requires an Arch-based or Debian-based GNU/Linux distribution with the Linux kernel version 5.12 or higher. Please, refer to each application folder to explore applications' specific requirements.

### General Inputs
<p align="justify">
EcoFloc operates with the following primary inputs:

1. **Process ID (PID) (`-p`):** The process identifier to analyze.
2. **Application Name (`-n`):** The name of the application to measure (it considers all the app. PIDs).
3. **Total Analysis Time (`-t`):** Sets the duration for energy and power value calculations.
4. **Measurement Interval (`-i`):** Determines the interval at which EcoFloc takes load and power measurements, impacting the allocated CPU time for the tool.
5. **Dynamic Mode (`-d`):** Allows EcoFloc to evaluate applications that can be closed and reopened during the analysis.
6. **Export Mode (`-f`):** Exports the measurement results to a CSV file.



More detailed specification of these parameters is specified in each application’s folder
</p>

### Outputs
<p align="justify">
The outputs of each application of EcoFloc after analyzing a process are as follows:

- **Execution Time:** Duration of the monitored process execution.
- **Average Power (in Watts):** The mean power consumption over the set analysis period.
- **Energy Consumption (in Joules):** Total energy used during the total analysis time.
</p>

## Compilation and Execution

### Automated Installation

To install EcoFloc, run the following command in your terminal as root:
```bash
/bin/bash/floc_installer.sh
```
This script requires Python3 to be installed on your system. It installs both the EcoFloc console application and a user interface that can be executed with the `flocUI` command.

### Manual Compilation and Installation

To compile and install the EcoFloc project on your system, follow these steps:

1. **Open your terminal.**
2. **Navigate to the root directory of the FLOC project:**
    - Use the `cd` command to change to the project directory.
3. **Compile the project and manage installations:**
    - Execute `make clean` to delete all executable files from the local folder.
    - Execute `make` to compile the project and install FLOC, making it ready for use.
    - Use `make uninstall` to remove FLOC from your system.
    - Use `make install` to copy FLOC onto your system, allowing it to be used as a common GNU/Linux command.

### Running FLOC:

To use EcoFloc and specify which application to execute, run:
```
./floc --cpu -p or -n [PID or App Name] -i [interval] -t [duration] --d --f [file.csv]
./floc --sd -p or -n [PID or App Name] -i [interval] -t [duration] --d --f [file.csv]
./floc --nic -p or -n [PID or App Name] -i [interval] -t [duration] --d --f [file.csv]
./floc --ram -p or -n [PID or App Name] -t [duration] --d --f [file.csv]
```



## References
[^1]: [Têchnopole Domolandes](https://www.domolandes.fr
[^2]: Running Average Power Limit (RAPL): [Intel® 64 and IA-32 Architectures Software Developer's Manual](https://www.intel.com/content/www/us/en/developer/articles/technical/intel-sdm.html), specifically in the section detailing power and thermal management.
[^3]: Humberto, A.V.H.: An energy-saving perspective for distributed environments:
Deployment, scheduling and simulation with multidimensional entities for Software and Hardware. Ph.D. thesis, UPPA, https://www.theses.fr/s342134 (2022)
