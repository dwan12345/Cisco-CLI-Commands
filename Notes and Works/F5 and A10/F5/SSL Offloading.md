- SSL offloading - the F5 handles SSL/TSL process instead of the servers.
	- SSL Process:
		1. key exchange. Asymmetric keys used to exchange symmetric keys. 
		2. Server proves it legit using a TSL certificate
		3. Now all traffic must be encrypted and decrypted using the symmetric keys
	- SSL process is CPU intensive, so we do not have servers handling it
	- Server must provide the a valid certificate. If we have 100s of servers, then this is horrific. So better to have the load balancer do it with only 1 certificate
	- enhances scalability
- SSL offloading is required for cookie persistence to work because the cookie resides in the payload of the HTTP message.
- you need a certificate, a self signed certificate will work fine for a lab
	- system -> file management -> SSL certificate list -> create
- Create a new SSL Client Profile to use the certificate
	1. local traffic -> profiles -> SSL -> client -> create
	2. Set parent profile to clientssl
	3. edit the certificate to the one you created. Change "Certificate" and "Key" to the certificate you created
	4. make sure to click add
- Add the Client SSL profile to the VS
	1. navigate to virtual servers -> *select your VS* -> *scroll down to SSL Profile (Client)*
	2. Add the SSL Client Profile we created
	3. click update
- to test:
	1. access web server using HTTPS
	2. Check if the certificate is provided
- 