# TLS-Decrypt

## Microsoft Windows

### Individual

PS C:\Users\cgrosskopf\Downloads> certutil -addstore CA certificate as .cer
CA Intermediate Certification Authorities
Signature matches Public Key
Certificate decrypt.scoe.org added to store.
CertUtil: -addstore command completed successfully.

### Group Policy Object - https://youtu.be/IdLTfCc-DYg

1. Right click Start Menu -> Run -> gpmc.msc
2. Expand Forest -> Domains -> Domain
3. Right Click “Group Policy Objects” -> New 
4. Enter a name for the object
5. Expand Group Policy Objects
6. Right click new object -> Edit
7. Computer Configuration -> Windows Settings -> Security Settings -> Public Key Policies
8. Right click “Trusted Root Certification Authorities” -> Import
9. Click Next
10. Browse to cert_pa-5220-scoe.crt
11. Place all certificates in the following store: “Trusted Root Certification Authorities"
12. Finish
13. Close Edit window
14. Link GPO by right clicking Organizational Unit -> Link an Existing GPO...
15. Select GPO and click OK

### Group Policy Object verification - https://youtu.be/Mdsh7G5yoo0

1. Right click Start Menu -> Run -> certmgr.msc
2. Expand “Trusted Root Certification Authorities” -> Certificates
3. You should see “decrypt.scoe.org” listed



## Mac OS independent

sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain <crt file>

### JAMF

1. Computers -> Configuration Profile -> New
2. Options -> General -> Name “SCOE Decrypt"
3. Options -> Certificate > Configure
4. Certificate name -> “SCOE Decrypt"
5. Select Certificate Option -> Upload
6. Upload Certificate -> Choose File -> Browse to cert_pa-5220-scoe.cer -> Upload
7. Verify Issuer Name “CN=decrypt.scoe.org"
8. Save


### Mosyle

1. Management -> Certificates (Under Management Profile)
2. Add new profile
3. Profile name -> “SCOE Decrypt"
4. Select the file -> browse to cert_pa-5220-scoe.crt
5. Profile Assignment -> “Apply to all current and future devices"
6. Save



## Linux

### Debian Based
codyg@server:~$ sudo mkdir /usr/local/share/ca-certificates/scoe
[sudo] password for codyg:
codyg@server:~$ sudo cp cert_pa-5220-scoe.crt /usr/local/share/ca-certificates/scoe/
codyg@server:~$ sudo update-ca-certificates
Updating certificates in /etc/ssl/certs...
1 added, 0 removed; done.
Running hooks in /etc/ca-certificates/update.d...
done.
codyg@server:~$

### CentOS Based
[cgrosskopf@server ~]$ sudo cp cert_pa-5220-scoe.crt /etc/pki/ca-trust/source/anchors/
[sudo] password for cgrosskopf:
[cgrosskopf@server ~]$ sudo update-ca-trust force-enable
[cgrosskopf@server ~]$ sudo update-ca-trust extract
[cgrosskopf@server ~]$


## Google Admin Panel - https://youtu.be/c1orS9KKIIs

1. Download the cert_pa-5220-scoe.crt
2. Login to G-Suite admin console at https://admin.google.com
3. Navigate to Device Management -> Networks -> Certificates
4. Select the top level OU for the G-Suite domain
5. Click ‘Add Certificate’ and upload the SSL file from step 1. 
6. Once the certificate is uploaded check the ‘Use this certificate as HTTPs certificate authority’ checkbox.
7. Click ‘Save’ in the bottom right corner




