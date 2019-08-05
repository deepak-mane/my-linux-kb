 # f5
 
 Step 1: Generating your CSR:
Login to the F5-BIG IP console.
Navigate to System > File Management > SSL Certificate List.
Click Create.
Type a name for the certificate.
From the Issuer drop down list, select Certificate Authority.
Fill the form to generate the CSR. ...
Click Finished.
  
  
  To generate a Certificate Signing Request (CSR) on F5 Big IP 11.x, a key pair must be created for the server. These two items are a public/private key pair and cannot be separated. If the public/private key file or password is lost or changed before the SSL certificate is installed, the SSL certificate will need to be re-issued. The private key, CSR and certificate must all match in order for the installation to be successful.

To create a new CSR using the F5 Big IP Configuration utility, perform the steps bellow:

Step 1: Generating your CSR:

Login to the F5-BIG IP console.
Navigate to System > File Management > SSL Certificate List. 
Click Create.
Type a name for the certificate.
From the Issuer drop down list, select Certificate Authority.
Fill the form to generate the CSR.CSR F5 Big IP
Common name: FQDN (fully-qualified domain name) of the server (e.g., www.domain.com, mail.domain.com, or for wildcard certificate *.domain.com).
Division: A department name, such as ‘Information Technology’.
Organization: The full legal name of the organization.
Locality, State or Province, Country: City, state, and country where the organization is located. Do not abbreviate.
E-mail Address: Your email.
Challenge Password, Confirm Password: Enter a password.
The key size must be 2048 bits for all SSL Certificates.
Click Finished
To download the request into a file on your system, Copy the CSR from the Request Text box (including the BEGIN and END tags) as seen below:
CSR
Paste the copied code into your enrollment portal, or save it to a text document.
Your CSR request has been created and is ready for you to copy and paste its contents into the enrollment portal.

If you are unable to use these instructions for your server, Acmetek recommends that you contact either the vendor of your software or the organization that supports it.

F5 Support:
For more information reference F5

For SSL installation instructions click Here.
