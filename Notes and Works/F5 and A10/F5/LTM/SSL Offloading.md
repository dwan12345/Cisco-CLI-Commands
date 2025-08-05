- SSL offloading - the F5 handles SSL/TSL process instead of the servers.
	- SSL Process:
		1. key exchange. Asymmetric keys used to exchange symmetric keys. 
		2. Server proves it legit using a TSL certificate
		3. Now all traffic must be encrypted and decrypted using the symmetric keys
	- SSL process is CPU intensive, so we do not have servers handling it. This is a marketing tool used by F5. You can still say this tho.
	- Server must provide the a valid certificate. If we have 100s of servers, then this is horrific. So better to have the load balancer do it with only 1 certificate. This is a big reason why we want SSL offloading.
	- For any L7 features of F5 to work, the traffic must be decrypted. Features such as HTTP_REQUEST iRules, WAF, cookie persistence. 
	- F5 also provides security patches really quickly, so SSL vulnerabilities are handled really quickly
- SSL Client Profile - used for client side SSL process
- SSL Server Profile (Rebridging) - if you want to send encrypted traffic to the web servers from the F5, us this. This is used for cases such as credit cards and social numbers.
- SSL Passthrough - when SSL is not handled on the F5, so the traffic is just passed through
	- very simple to set up. used when end-to-end encryption is needed for security and compliance reasons.
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