# Connectivity Workshop

We appreciate that a lot of our customers use Proxy Chaining, however, for the purpose of this training you will be using the PAC file.

You will have total control of the windows environment within the CloudShare virtual machine. The environment is Windows Server 2022 Standard.

Before you begin, in CloudShare on your virtual machine, ensure the Chrome browser is configured to allow Cookies in Incognito mode, or you may see looping issues. This can be set using the slider in the Incognito browser or by navigating to Settings | Privacy & Security | Third-party cookies and set Block third-party cookies in incognito mode to Off. Choose Allow third-party cookies.

Notes:
•	Please ensure you are not accessing the CloudShare environment in isolation as you may see issues with keyboard and mouse access when working in isolation.
•	Be aware that the isolation indicators and block pages you see on your lab environment may differ from the examples shown in the lab documents.

 
Exercise 1: Test Pre-Pend
1.	Connect to the CloudShare environment using the instructions provided by the email you have received.
2.	Open the Chrome browser and navigate to https://bbc.com using the prepend notation:
a.	Type https://safe.menlosecurity.com.
b.	Enter bbc.com, or a domain of your choice, in the dialogue as shown below:
 


3.	Log on as admin@menlo-student<n>.com where <n> is your student number provided by the instructor.  Use the password provided to you by the instructor. 
4.	Click on a link on the page.
5.	Notice that the site you go to is isolated and the URL is prepended with safe.menlosecurity.com.

 
Exercise 2: Configure Proxy Auto Config 

1.	Using the Chrome Browser, log in to the Admin Portal using https://admin.menlosecurity.com as admin@menlo-student<n>.com
(The Admin Portal URL has been saved as a bookmark on your Bookmark Bar on Chrome.)
2.	Type the password provided to you by the instructor.
3.	Click the App Switcher   
4.	Select Settings | Traffic | PAC Settings.
5.	From the PAC Settings Screen, Click the button  
6.	Use the properties below to create your PAC file. Remember that <n> is your two-digit student number:
Property	Value
Display Name	proxy-<n>
Filename	proxy-<n>.dat
Proxy Mode	SSL Inspection + Menlo Authentication (Port:3129)

7.	Take some time to review the settings you have available in:
a.	Direct Connect – Enable the toggle to view the Office 365 URLs and IPs.
b.	Proxy & Roaming – Enable proxy and roaming settings to view the settings.
c.	Default Exceptions – Expand some of the exceptions to view the domains.
d.	Domain Exceptions – Notice that you can import a list of domains.  
e.	Subnet/IP Exceptions.
8.	Once you have reviewed the options, ensure you leave all the settings as default.
9.	Click Save and then Save again.
10.	Select your new file (proxy-<n>) and click on the preview icon.

 

11.	 If you understand JavaScript, review the PAC file. Notice the domains which will be directly accessed.
12.	Close the preview window.
13.	Copy the location of the PAC file .  You will receive confirmation that the PAC file has been copied to the clipboard.

 
Exercise 3: Configuring the Proxy Auto Config File in the Browser
The steps to configure the Proxy Auto Config (PAC) file differs between browsers and operating systems. For the duration of the course, we are using Chrome.
1.	Open the Settings in the Chrome Browser.     
2.	Type Proxy in the search bar. 
3.	Select Open your computer’s proxy settings:























4.	Make sure Automatically detect settings is not selected.
5.	Select Use setup script and paste the address for your proxy automatic configuration. 
For example:
https://global.pac.menlosecurity.com/menlo-<redacted>/proxy-<n>.dat
If you have problems with paste inside the VM, then use the VM Clipboard as shown below:
 

6.	Click Save and close the Settings window.
7.	Open a New Incognito window in your browser. You can access this from the Settings Menu.  Can you work out why you need to open an incognito window?
8.	Browse to the following site, notice it is HTTP http://neverssl.com.
9.	If you see a warning: neverssl.com doesn’t support a secure connection, press continue to site.
10.	When you are asked to authenticate, log on with the same credentials you used for the Admin Portal.

The web page was isolated by Menlo Security as seen by the indicator.  Not all tenants have the indicator switched on, this is a customizable attribute.  Further details on this will be covered later in this training course.
 
11.	Another way to identify pages that are isolated is to view the source code (mouse right-click and select View page source). Notice it is not the source code of the page, you will see tags such as sv-template, also the version and the region can be identified.
 

12.	Notice the version information near the top of the page, and the region you connected to near the bottom of the page. 
For example, europe-west2 is London, asia-southeast1 is Singapore.
 
Exercise 4: Trust Isolated HTTPS
1.	Continuing in the Incognito window, browse to https://www.ycombinator.com/ 
2.	Notice the message that you cannot safely connect to this site and Not Secure is specified next to the URL.  The message also states that the issue is caused by Menlo Security Root CA. 

3.	Do NOT click past the error.
4.	Dismiss the certificate window.
5.	Close the incognito window.
Configure your browser to trust the Menlo Security Root CA

Using the Menlo Security CA certificate from your desktop on your virtual machine, install the certificate.

 

Note: You can also download the certificate from the following resources:
•	Menlo Security Knowledge Base
•	https://deploy.menloadmin.com/instructions/cert/

1.	Open the Settings on the Chrome browser.
2.	Select Privacy and Security | Security. 
3.	Scroll down to Manage certificates.

4.	Click on Manage imported certificate from Windows.
5.	Navigate to the Trusted Root Certification Authorities tab, click Import. The Certificate Import Wizard will be displayed.
6.	Click Next.
7.	Click Browse and select the Certificate file from your desktop.
8.	Click Next. Ensure you choose to place all certificates in the following store ‘Trusted Root Certificate Authorities’.
9.	Click Next and Finish.
10.	The Security Warning dialog is displayed showing the SHA1 Thumbprint. Check as many of the hexadecimal digits as you like to ensure this is the correct certificate.

Note: The current root certificate will expire on 9th November 2025.

The SHA1 Thumbprint of the expiring certificate is: 72 77 74 52 B7 3D 35 96 59 A7 EF 31 5F CA 10 4E 64 7C B0 67

The SHA1 Thumbprint of the new certificate is: D7 AF 71 B3 D0 F1 71 EA 7D F3 AC 03 54 DB 5F 3A 21 86 D5 20

11.	Click Yes to install the certificate and OK to acknowledge the import.
12.	Scroll through the list and you should see the certificate has been installed correctly.
 
13.	Close the Certificate Manager.
14.	Close the Browser.
Verify the Configuration

1.	Open the Chrome Browser.
2.	Go to a different HTTPS website, for example https://slack.com.
3.	Click View Site Information   and the lock to see the Menlo Security certificate is now accepted and is valid.
 

4.	Also, notice the isolation indicator in the browser.
Note: You can’t go immediately to back to https://www.ycombinator.com/ and see this effect because certificate validation results are cached. If you wait a few minutes, you can reload and see your traffic is now properly isolated.
Please Note: Internet Explorer is no longer supported by Menlo Security.
Information about Internet Explorer End of Support for Menlo Users


![image](https://github.com/user-attachments/assets/bfda3776-6393-4a79-bf0e-c6893c80700f)
