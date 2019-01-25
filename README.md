

### PROJECT IS ON TRANSITION STATE FROM PRIVATE TO OPEN SOURCE, SO SOME PART OF SW DO NOT WORK YET...


### HomeBrain project description:

OS Linux based software package, which allows turn your laptop or mini computer (BeagleBoard) into a centralized 
data acquisition system from I/O modules by ModBus RTU protocol, and transfer data to the user via friendly MQTT protocol.

### Project includes follow components:

1. **Build**        - a set of scripts for project build under Linux Host and Linux Target.

                      **Linux Host build** is usefull for debugging the project and further transition to the target.
                      As result you will have set of binaries, which can be started on Linux Ubuntu and similar.

                      **Linux Target build** based on BuildRoot package, result is an image of the file system
                      in ext2/ext4 format, which are ready for extracting on SD card to use in miniPC (BeagleBone)

2. **HomeBrain**    - the main process, which communicate with I/O modules via ModBus RTU protocol.
                      Reads ModBus registers and saves data in the internal table of points (discrete, analog)
3. **mqttgtw**      - the process that converts data from the HomeBrain point table to MQTT topic values.
4. **pointmonitor** - This tools allows you to view the current state of the HomeBrain points (discrete, analog). 
                      It is not necessary for the system operation, and needed only on debugging stage.
5. **csvparser**    - parser for *.csv documents, which describes the configuration for mqttgtw.

### Project structure

**homebarin** - it's git global repository, which do not contain source code, and used only to organize submodules.

**Build / HomeBrain / mqttgtw / pointmonitor / csvparser** - it's git submodules.

### Supported system :

*   Host: Ubuntu Linux 18.04 
*   Target: BeagleBone Black 

### Schematic project map:

---picture---


### Installation for development:

######  1. clone all project:

```bash
   cd /home
   git clone https://github.com/azhigaylo/homebrain.git
   git submodule init
   git submodule update
   git pull --recurse-submodules
   git submodule update --recursive --remote
```

next time:
```bash
   git pull --recurse-submodules
   git submodule update --recursive --remote
```

######  2. First step it's HOST preparetion. Needed to setup some development and thirdparty. There two variant of preparation:

           - prepare HOST for host build (CMake/DLT/Mosquitto/BuildRoot will be uploaded and built.) 
```bash
           ./prepare_all.sh -i
```
           - prepare HOST for target build  (DLT/Mosquitto will be built for ARM) 
```bash
           ./prepare_all.sh -it
```
           - help :
```bash
           ./prepare_all.sh --help
```

######  3. Second step it's build all project.There two variant of build:

           - build for HOST, result will be available in folder <homebrain_products>
```bash
           ./build_all.sh
```
           - build for TARGET, result will be available in folder </homebrain_third_party/host/buildroot/output/images/>
```bash
           ./build_all.sh -t
```
           - help :
```bash
           ./build_all.sh --help
```

### For possible contributors:

Pull requests are welcome.
If you would like to make changes/fix, please follow these rules:

1. The pull requests accepted only in "development" barnch
2. All changes/fixes should be tested before commit


### an example of implemented system that are based on HomeBrain complex

## License
[MIT](https://choosealicense.com/licenses/mit/)
