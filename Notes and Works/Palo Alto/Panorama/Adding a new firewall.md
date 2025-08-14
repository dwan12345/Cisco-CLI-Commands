
# Configuration
- Add serial num to panorama
	- find the serial number of the PA. it is on the device, or you can find it in the GUI or CLI
	- panor -> managed devices -> summary -> add device
	- paste in the serial number
	- generate Auth key
	- copy the auth key
	- commit to panor
- telling the PA about panor
	- PA -> device -> setup -> management -> panorama settings
	- put in the IP of the panor
	- paste in the auth key
	- commit
- verify
	- panor -> managed devices
	- you should see that it is connected