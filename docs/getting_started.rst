Getting Started
===============

This guide will walk you through setting up your LimeSDR XTRX board with the required hardware and software, including LimeSuiteNG and GNU Radio Companion. LimeSuiteNG will be used to perform a basic setup and verify the board connection, and a simple FM receiver example in GNU Radio will be covered. For more detailed information, please refer to the LimeSuite and GNU Radio documentation.

Requirements
------------

- **Host:** A PC or any other host with an mPCIe slot (or an mPCIe to PCIe adapter if needed).
- **Operating System:** Ubuntu or another compatible OS.

Step 1: Preparing the Hardware
------------------------------

1. **Prepare the mPCIe Card:** Insert the mPCIe card into the adapter (if using one) and ensure it’s securely connected to the PC's mPCIe slot.

2. **Connect antenna:** For FM Receiver example a suitable FM antena should be connected to X2 U.FL connector.

Step 2: Preparing the Software
------------------------------

Build and install the LimeSuiteNG software by following the installation steps to support board configuration and control. If you want to try FM receiver example GNU Radio Companion has to be istalled before LimeSuiteNG.

**1. Install GNU Radio Companion:**
 .. code-block:: bash
 
 	sudo apt-get install gnuradio

**2. Clone LimeSuiteNG source code:**
 .. code-block:: bash
 
 	git clone https://github.com/myriadrf/LimeSuiteNG.git
 	
**3. Build and install LimeSuiteNG on Linux:**

 .. code-block:: bash
 
 	cd LimeSuiteNG
	sudo ./install_dependencies.sh
	cmake -B build && cd build
	make
	sudo make install
	sudo ldconfig
 	
Steps above should be enough to build and install LimeSuiteNG on Linux host, for complete documentation visit `https://limesuiteng.myriadrf.org <https://limesuiteng.myriadrf.org/gettingstarted/>`__ . For GNU Radio Companion visit `https://www.gnuradio.org/ <https://www.gnuradio.org/>`__ .

Step 3: Launching LimeSuiteNG GUI and Exploring Capabilities
------------------------------------------------------------

LimSuiteNG GUI software can be used to explore LMS7002M capabilities because it provides graphical interface to tune and modify various LMS7002M IC settings. In this example LMS7002M chip will be configured to generate test signal using NCO available in RXTSP block. FFT viewer from LimeSuiteNG GUI will be used to view test signal.   

1. **Launch the Software:**  
   
   LimeSuiteNG GUI can be launched from Linux terminal by executing following command:
   
   .. code-block:: bash
   
    	limeGUI
   
2. **Verify the connection**  

	Select LimeSDR XTRX device from dropdown list: 
   
	.. figure:: images/limesuiteng_connection.png
		:align: center
		
		Figure 1. LimeSuiteNG device connection.

	After selecting your device you should see INFO message with connected device:
   
	.. figure:: images/limesuiteng_connected_device.png
		:align: center
	
		Figure 2. LimeSuiteNG connected device.   
   
3. **Use basic software functions** 

	Configure LMS7002M IC with default sample rate, receive and tranmit frequency, gain settings by clicking "Submit" button:

	.. figure:: images/limesuiteng_default_config.png
		:align: center

		Figure 3. Default configuration. 

	Select LMS7002M from device tree and select RXTSP tab. Modify parameters as shown in figure below and click "Upload NCO" and "Load to DC I", "Load to DC Q" buttons.
	
	.. figure:: images/limesuiteng_rxtsp.png
		:align: center	

		Figure 4. RXTSP settings. 

	Open Modules->fftviewer modify settings as shown in figure below and click "START/STOP" button to view test signal.

	.. figure:: images/limesuiteng_fftviewer.png
		:align: center	

		Figure 5. FFT Viewer. 


Step 4: FM Receiver Example
---------------------------

	Launch GNU Radio Companion and open FM_receiver.grc example from LimeSuiteNG/plugins/gr-limesdr/examples directory. Click "Execute the flow graph" button. 
	
	.. figure:: images/gnu_radio_fm_receiver.png
		:align: center
		
		Figure 6. FM Receiver example on GNU Radio Companion.
	
	In FM Receiver window (Figure 7) change "RX baseband" frequency to avalable FM station in your area and select L for "LNA Path". You should be able to hear demodulated FM radio signal from your host audio output. 

	.. figure:: images/gnu_radio_fm_receiver_window.png
		:align: center
		
		Figure 7. FM Receiver window.