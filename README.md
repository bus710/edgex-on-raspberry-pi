# EdgeX on Raspberry Pi

Raspberry Pi (RPI) is a series of well-known single board computers (SBC). The credit card sized computer can run Linux as its operating system so that it can be a useful platform for Internet of Things (IoT) projects. Although there are many of different IoT frameworks, EdgeX framework can be considered as a solid candidate because of its architecture, workflow, and productivity. EdgeX is designed as microservices architecture and thus new features can be easily adapted but very robust in intense situations. The framework is developed with modern web technologies from the beginning so that backend developers can leverage its smooth workflow and maximum productivity.

Recently, EdgeX foundation released a new version called Geneva (each version has a name of cities). Also Canonnical announced a new Ubuntu release 20.10 Groovy Gorilla and they promoted RPI as one of major IoT platforms. These news made me to think about the combination of EdgeX, RPI, and Ubuntu. Running EdgeX on RPI is not something new because Golang and Docker are the cross platform tools used for EdgeX code base but this time the OS can be Ubuntu so that the developers, who want to deploy EdgeX based IoT projects, can minimize the difference between their development system, cloud hosts, and distributed IoT targets.

This short tutorial includes these chapters:
- How to install Ubuntu on RPI
- How to install packages required for EdgeX development
- How to launch and test EdgeX with a virtual device service
- How to develop custom device and app services for a real hardware

<br/>

## Reference

- https://docs.edgexfoundry.org/1.2/examples/LinuxTutorial/LinuxTutorial/
- https://docs.edgexfoundry.org/1.2/examples/LinuxTutorial/EdgeX-Foundry-tutorial-ver1.0.pdf

<br/>