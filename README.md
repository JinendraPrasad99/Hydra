# Hydra
A Detailed Guide On Hydra -  Kali Linux


Hydra is a very fast network logon cracker that supports many different services. It is a parallelized login cracker that supports numerous protocols to attack. New modules are easy to add, besides that, it is flexible and very fast. This tool gives researchers and security consultants the possibility to show how easy it would be to gain unauthorized access from a remote to a system.

For most protocols, SSL is supported (e.g., https-get, ftp-ssl, etc.). If not, all necessary libraries are found during compile time, your available services will be fewer. Type "hydra" to see what is available.



**To guess the Password for a specific username**

If you have a correct username but want to log in without knowing the password, you can use a list of passwords and brute force passwords on the host for **ftp** service.

**hydra -l ignite -P pass.txt 192.xxx.xxx.xx1 ftp**

Here -l option is for username -P for password lists and host IP address for FTP service. 

**To guess username for specific password**

You may have a valid password but no idea what username to use. Assume you have a password for a specific FTP login. You can brute force the field with the correct username wordlists to find the correct one. 

**hydra -L users.txt -p 123 192.xxx.1.xx1 ftp**

You can use the -L option to specify user wordlists and the -p option to specify a specific password. Here, our wordlist is users.txt for which the -L option is used, and the password is 123 and for that -p option is used over FTP.

**Brute forcing Username and Password**

Now if you don’t have either of username or password, for that you can use brute force attack on both the parameters username and password with wordlist of both and you can use -P and -U parameters for that.

**hydra -L users.txt -P pass.txt 192.168.1.141 ftp**




































