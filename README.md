# rpi-daq
Software for single-module control using a Raspberry Pi

 * Install bitarray python package
 ```
 BITARRAY_DIR=/choose/wherever/you/want
 cd ${BITARRAY_DIR}
 git clone https://github.com/ilanschnell/bitarray.git
 cd bitarray
 sudo python setup.py install
 sudo python setup.py build_ext -i
 ```

 * Download this code
 ```
 HOME_DIR=/choose/wherever/you/want
 cd ${HOME_DIR}/
 git clone https://github.com/asteencern/rpi-daq.git
 ```

 * Install bcm2835 and create shared library
```
cd ${HOME_DIR}/rpi_daq/RPi_software/bcm2835-1.52/src
gcc -shared -o libbcm2835.so -fPIC bcm2835.c
sudo cp libbcm2835.so /usr/local/lib/libbcm2835.so
```

* Compile gpiolib.c and create shared library
```
cd ${HOME_DIR}/rpi-daq
gcc -c -I ${BCM_DIR}/bcm2835-1.52/src ${BCM_DIR}/bcm2835-1.52/src/bcm2835.c -fPIC gpiolib.c
gcc -shared -o gpiolib.so gpiolib.o
```  

* Example of acquisition:
```
python run.py --moduleNumber=63 --nEvent=1000 --acquisitionType=sweep --externalChargeInjection --channelIds=0,10,50,34 --compressRawData --channelIdsMask=22 --channelIdsDisableTOT=22  --channelIdsDisableTOA=22
```
