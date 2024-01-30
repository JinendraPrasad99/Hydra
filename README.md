# Hydra - Guide
A Detailed Guide On Hydra -  Kali Linux

![image](https://github.com/JinendraPrasad/Hydra/assets/99186783/7b257321-89b2-4d84-b3c8-d69d81e8df5a)


Hydra is a very fast network logon cracker that supports many different services. It is a parallelized login cracker that supports numerous protocols to attack. New modules are easy to add, besides that, it is flexible and very fast. This tool gives researchers and security consultants the possibility to show how easy it would be to gain unauthorized access from a remote to a system.

For most protocols, SSL is supported (e.g., https-get, ftp-ssl, etc.). If not, all necessary libraries are found during compile time, your available services will be fewer. Type "hydra" to see what is available.


**To guess the Password for a specific username**

If you have a correct username but want to log in without knowing the password, you can use a list of passwords and brute force passwords on the host for **ftp** service.
```
hydra -l ignite -P pass.txt xxx.xxx.xxx.xx1 ftp
```
Here -l option is for username -P for password lists and host IP address for FTP service. 

**To guess username for specific password**

You may have a valid password but no idea what username to use. Assume you have a password for a specific FTP login. You can brute force the field with the correct username wordlists to find the correct one. 
```
hydra -L users.txt -p 123 xxx.xxx.1.xx1 ftp
```
You can use the -L option to specify user wordlists and the -p option to specify a specific password. Here, our wordlist is users.txt for which the -L option is used, and the password is 123 and for that -p option is used over FTP.

**Brute forcing Username and Password**

Now if you don’t have either of username or password, for that you can use brute force attack on both the parameters username and password with wordlist of both and you can use -P and -U parameters for that.
```
hydra -L users.txt -P pass.txt xxx.xxx.xx.xxx ftp
```
**Verbose and Debug Mode**

-V option is used for verbose mode, where it will show login+pass combination for each attempt. Here, I have two wordlists users.txt and pass.txt so the brute force attack was making combinations of each login+password and verbose mode showed all the attempt.
```
hydra -L users.txt -P pass.txt xxx.xxx.xx.xxx ftp -V
```
Now is the -d option used to enable debug mode. It shows the complete detail of the attack with waittime, conwait, socket, pid, RECV
```
hydra -l ignite -P pass.txt xxx.xxx.xxx.xxx ftp -d
```
-d option enabled debug mode which, as shown displayed complete detail of the attack.

**NULL/Same as Login or Reverse login Attempt**

Hydra has an option -e which will check 3 more passwords while brute forcing. [n] for null, [s] for same i.e., as same as username and [r] for reverse i.e., the reverse of username. As shown in the 
screenshot, while brute-forcing the password field, it will first check with null option then same option and after that reverse. And then the list which I have provided.

```
hydra -L users.txt -P pass.txt xxx.xxx.xxx.xxx ftp -V -e nsr
```

**Saving output in Disk**

This tool gives you an option to save the result into the disk. Basically for record maintenance, better readability and future preferences we can save the output of the brute force attack into a file by using -o parameter. 

```
hydra -L users.txt -P pass.txt xxx.xxx.xxx.xxx ftp -o result.txt
```

**Password generating using various set of characters**

To generate passwords using various set of characters, you can use -x option. It is used as -x min:max:charset where,
Min: specifies minimum number of characters in password.
Max: specifies maximum number of characters in password.
Charset: charset can contain 1 for numbers, a for lowercase and A for uppercase characters. Any other character which is added is put to the list.
Let’s consider as example: 1:2:a1%.The generated passwords will be of length 1 to 2 and contain lowercase letters, numbers and/or percent signs and dots.

```
hydra -l ignite -x 1:3:1 ftp://xxx.xxx.xx.xxx
```
here minimum length of password is 1 and max length is 3 in which it will contain numbers and for password 123 it showed success.

**To attack on specific port rather than default**

Network admins sometimes change the default port number of some services for security reasons. In the previous commands hydra was making brute force attack on ftp service by just mentioning the service name rather than port, but as mentioned earlier default port gets changed at this time hydra will help you with -s option. If the service is on a different default port, define it using -s option.

```
nmap -sV xxx.xxx.xxx.xxx
hydra -L users.txt -P pass.txt xxx.xxx.xxx.xxx ssh -s 2222
```

So to perform, first I tried running nmap scan at the host. And the screenshot shows all open ports where ssh is at 2222 port. So post that I tried executing the hydra command with -s parameter and port number.

**Attacking on Multiple Hosts**

As earlier I performed brute force attack using password file pass.txt and username file users.txt on single host i.e., xxx.xxx.xxx.xxx. But if there are multiple hosts, for that you can use -M with the help of which brute force is happening at multiple hosts.
```
hydra -L users.txt -P pass.txt -M hosts.txt ftp
```
Now in the above command, I have used the -M option for multiple hosts so, it is very time-consuming to display all the attempts taking place during the attack, for that medusa has provided the -F option such that the attack will exit after the first found login/password pair for any host.

```
hydra -L users.txt -P pass.txt -M hosts.txt ftp -F
```

**Using Combo Entries**

This tool gives you a unique parameter -C for using combo entries. First, you need to create a file that has data in colon-separated "login: pass" format, and then you can use the -C option mentioning the file name and perform a brute force attack instead of using the -L/-P options separately. In this way, the attack can be faster and give you the desired result in less time.
```
cat userpass.txt
hydra -C userpass.txt xxx.xxx.xxx.xxx ftp
```

**Concurrent Testing on Multiple Logins**

If you want to test multiple logins concurrently, for that you can use -t option by mentioning the number and hence hydra will brute force concurrently.

```
hydra -L users.txt -P pass.txt xxx.xxx.xxx.xxx ftp -t 3 -V
```

**Attacking on secured service connection**

While performing attack on ftp connection, you just mention the service name along with appropriate options, but if the host has ftp port open but and ftp is secured, so if you use,
```
hydra -l ignite -P pass.txt ftp://xxx.xxx.xxx.xxx 
```
This command will not execute properly and hence 0 valid password found. So in order to perform attack on secured ftp connection, then run this command.
```
hydra -l ignite -P pass.txt ftps://xxx.xxx.xxx.xxx
```

This is one way to attack on secured ftp, hydra provides one more way to attack on secured service

```
hydra -l ignite -P pass.txt xxx.xxx.xxx.xxx ftp
hydra -l ignite -P pass.txt xxx.xxx.xxx.xxx ftps
```

The first did not worked as the host xxx.xxx.xxx.xxx has secured ftp, but second worked and showed us valid password found. In this way you can perform brute force attack on hosts which have secured services open.











