# gusto-gui6
The GUSTO graphical user interfaces started life in a hotel room (as all good things do) in Christchurch, NZ (CHC) while waiting for my ice flight to Antarctica for STO-2 in 2015.  The original gui used PyQt 4 and Python 2.7 to connect to the HEB receiver server over TCP/IP and allowed one to bias mixers, switch local oscillator DCDCs, and display IV curves using matplotlib.

Many more GUIs have proliferated from that template, including autocorrelator control & display, and now GUSTO LO controls.

I've finally been convinced that PyQt 3 is the future of 2023, and this repository updates the old GUIs to use the PyQt 6 framework and Python 3.11

## Installation
### For Mac:
Oh Lord, Ventura has made me upgrade from PyQt4 and Python2.7 to PyQt6 and Python3.

GUIs can be run in a virtual environment or installed locally.  To set up a venv, do:
```
   python -m venv venv
   source venv/bin/activate

   python -m pip install pyqt6 pyqt6-tools pyserial numpy matplotlib
   python startup.py
```

when done working in the virtual environment: `deactivate`

Libraries note:
   for coreSERIAL, a SORAL internal library for making serial and TCP port read/receive calls and waiting for ine terminators, the GUI uses one in this repo.  Optionally do this: `export PYTHONPATH="$PWD/libraries"` from the git repo root.

## Anritsu
This gui displays the Anritsu MA24126A USB power meter head in mW, dBm, and a scrolling screen.

![alt text](https://github.com/abegyoung/gusto-gui6/blob/main/images/meter.jpg?raw=true)

## B1B2LO
Each of the B1 and B2 have their own gui.  For multipliers, stage 1,2,3 are arranged in vertical sections, with 3 columns of Vmon,Imon,DAC in each.  The DAC value is read after CommOpen, and the Vmon/Imon are updated on every DAC setting.  For the PSat drive, a DAC columna and Voltage monitor are paired with a Checkbox for PSat ON/OFF to the far right.

PSat Current is read back in the Server Response window at bottom each time the PSat DAC is updated.

Board rails are displayed in the lower right every time the "refresh" button is clicked, refreshing all ADCs including multiplier Vmon/Imon/DAC.

![alt text](https://github.com/abegyoung/gusto-gui6/blob/main/images/B1B2LO.jpg?raw=true)

Various functions are divided into tabs within the GUI.  Tab 2 has DCDC control and Temp sense reads.

![alt text](https://github.com/abegyoung/gusto-gui6/blob/main/images/B1B2LO_Tab2.jpg?raw=true)

## B3LO
This gui operates the B3LO controller on 4 tabs.

![alt text](https://github.com/abegyoung/gusto-gui6/blob/main/images/B3LO_mainTab.jpg?raw=true)

### Main Tab 
QCL bias setting is controled and monitor is displayed on the left panel.

SLED multplier and PSat settings are controlled disaplayed on the right panel.

A Server response window, refresh button, and communication buttons are at bottom.

### DCDC Tab
DCDC control is here.

### PID AMP Tab
B3LO amplitude pump level pid via optical vane is controlled here.

### PID FRQ Tab
B3LO frequency is controlled via SLED input and QCL bias is controlled from here.

### VCO REG Tab
Hittite synthesizer register settings may be read and written here.

## Bias Server
Front end bias of mixers is here.

![alt text](https://github.com/abegyoung/gusto-gui6/blob/main/images/BiasServer.jpg?raw=true)
