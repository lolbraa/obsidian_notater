# IOS Command Structure
>[!info]- Bilde
>![[IOS CLI-1.png]]
>![[IOS CLI-2.png|test]]

Enter privileged EXEC mode.
```
Switch> enable
```
# Config
Se config
```
show ip interface brief 
show run
show running-config
show startup-config // Display the current contents of NVRAM.
```

Enter Global Configuration mode
>When in privileged EXEC mode, one of the commands starting with the letter ‘C’ is configure. Type either the full command or enough of the command to make it unique. Press the \<tab\> key to issue the command and press ENTER.

```
S1# configure
```

Save and Verify Configuration Files to NVRAM
```
copy running-config startup-config
```

Configure a message of the day (MOTD) banner.
```
S1# config t
S1(config)# banner motd "This is a secure system. Authorized Access Only!"
S1(config)# exit
```
## Config Switch
Assign a hostname to a switch.
```
Switch# configure terminal 
Switch(config)# hostname S1 
S1(config)# exit
```

Configure switch with an IP address.
> Switches can be used as plug-and-play devices. This means that they do not need to be configured for them to work. Switches forward information from one port to another based on MAC addresses.
```
S1# configure terminal
S1(config)# interface vlan 1
S1(config-if)# ip address 192.168.1.253 255.255.255.0
Switch(config)#ip default-gateway 192.168.0.65
S1(config-if)# no shutdown
S1(config-if)#
S1(config-if)# exit
```

## Config Ruter
Syntax
```
Router(config)# **interface** _type-and-number_  
Router(config-if)# **description** _description-text_  
Router(config-if)# **ip address** _ipv4-address subnet-mask_  
Router(config-if)# **ipv6 address** _ipv6-address/prefix-length_  
Router(config-if)# **no shutdown**
```

Eksempel 
```
R1> enable
R1# configure terminal
Enter configuration commands, one per line.
End with CNTL/Z.
R1(config)# interface gigabitEthernet 0/0/0
R1(config-if)# description Link to LAN
R1(config-if)# ip address 192.168.10.1 255.255.255.0
R1(config-if)# ipv6 address 2001:db8:acad:10::1/64
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)#
*Aug  1 01:43:53.435: %LINK-3-UPDOWN: Interface GigabitEthernet0/0/0, changed state to down
*Aug  1 01:43:56.447: %LINK-3-UPDOWN: Interface GigabitEthernet0/0/0, changed state to up
*Aug  1 01:43:57.447: %LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/0, changed state to up
R1(config)#
R1(config)#
R1(config)# interface gigabitEthernet 0/0/1
R1(config-if)# description Link to R2
R1(config-if)# ip address 209.165.200.225 255.255.255.252
R1(config-if)# ipv6 address 2001:db8:feed:224::1/64
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)#
*Aug  1 01:46:29.170: %LINK-3-UPDOWN: Interface GigabitEthernet0/0/1, changed state to down
*Aug  1 01:46:32.171: %LINK-3-UPDOWN: Interface GigabitEthernet0/0/1, changed state to up
*Aug  1 01:46:33.171: %LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/1, changed state to up
R1(config)#
```

Se config
```
show ip interface brief
```

| Commands                                                       | Description                                                                                                                                                                                                                                                          |
| -------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **show ip interface brief**  <br>**show ipv6 interface brief** | The output displays all interfaces, their IP addresses, and their current status. The configured and connected interfaces should display a Status of “up” and Protocol of “up”. Anything else would indicate a problem with either the configuration or the cabling. |
| **show ip route**  <br>**show ipv6 route**                     | Displays the contents of the IP routing tables stored in RAM.                                                                                                                                                                                                        |
| **show interfaces**                                            | Displays statistics for all interfaces on the device. However, this command will only display the IPv4 addressing information.                                                                                                                                       |
| **show ip interface**                                          | Displays the IPv4 statistics for all interfaces on a router.                                                                                                                                                                                                         |
| **show ipv6 interface**                                        | Displays the IPv6 statistics for all interfaces on a router.                                                                                                                                                                                                         |

## Passord
Examine the current switch configuration.
```
Switch# show running-config
```

Secure access to the console line.
>To secure access to the console line, access config-line mode and set the console password to letmein. 
```
S1# configure terminal
S1(config)# line console 0 
S1(config-line)# password letmein 
S1(config-line)# login
S1(config-line)# exit
S1(config)# exit
```

Secure privileged mode access.
```
S1> enable
S1# configure terminal 
S1(config)# enable password c1$c0 
S1(config)# exit
```

Configure an encrypted password to secure access to privileged mode.
> The enable password should be replaced with the newer encrypted secret password using the enable secret command. Set the enable secret password to itsasecret.
> Note: The enable secret password overrides the enable password. If both are configured on the switch, you must enter the enable secret password to enter privileged EXEC mode
```
S1# config t
S1(config)# enable secret itsasecret 
S1(config)# exit
```


Encrypt the enable and console passwords.
>As you noticed in Step 7, the enable secret password was encrypted, but the enable and console passwords were still in plain text. We will now encrypt these plain text passwords using the service password-encryption command.

```
S1# config t
S1(config)# service password-encryption 
S1(config)# exit
```

Introduction to Networks -Device Security




https://contenthub.netacad.com/itn-dl/16.4.3

# Diverse
## No DNS lookup
[How to disable Automatic DNS Lookup In Cisco Devices - GNS3 Network](https://www.gns3network.com/how-to-disable-dns-lookup-in-cisco-devices/)
```
no ip domain-lookup
```

## Shutdown unused ports
[How to disable unused Cisco Access Ports - TechDirectArchive](https://techdirectarchive.com/2019/08/14/disable-unused-access-ports/)
Task: Disable interfaces Gi0/1 to G10/24 on switch7 for example
```
switch7(config)#interface range Gi0/1-24
switch7(config-if)#shutdown
```

Eksempel
```
S1(config)#interface range FastEthernet 0/1-4
S1(config-if-range)#shutdown

%LINK-5-CHANGED: Interface FastEthernet0/1, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/2, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/3, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/4, changed state to administratively down
S1(config-if-range)#interface range FastEthernet 0/7-21
S1(config-if-range)#exit
S1(config)#interface range FastEthernet 0/7-21
S1(config-if-range)#shutdown
```

# SSH
[How to configure SSH on Cisco IOS](https://networklessons.com/cisco/ccna-200-301/configure-ssh-cisco-ios)
Let’s configure a hostname:

```
Router(config)#hostname R1
```

And a domain name:

```
R1(config)#ip domain-name NETWORKLESSONS.LOCAL
```

Now we can generate the RSA keypair:

```
R1(config)#crypto key generate rsa
The name for the keys will be: R1.NETWORKLESSONS.LOCAL
Choose the size of the key modulus in the range of 360 to 4096 for your
  General Purpose Keys. Choosing a key modulus greater than 512 may take
  a few minutes.

How many bits in the modulus [512]: 2048
% Generating 2048 bit RSA keys, keys will be non-exportable...
[OK] (elapsed time was 3 seconds)
```

When you use the **crypto key generate rsa** command, it will ask you how many bits you want to use for the key size. How much should you pick?

It’s best to check the [next generation encryption](https://www.cisco.com/c/en/us/about/security-center/next-generation-cryptography.html) article from Cisco for this.  At this moment, a key size of 2048 bits is acceptable. Key sizes of 1024 or smaller should be avoided. Larger key sizes also take longer to calculate.

Once the keypair has been generated, the following message will appear:

```
R1#
%SSH-5-ENABLED: SSH 1.99 has been enabled
```

As you can see above, SSH version 1 is the default version. Let’s switch to version 2:

```
R1(config)#ip ssh version 2
```

SSH is enabled but we also have to configure the VTY lines:

```
R1(config)#line vty 0 4
R1(config-line)#transport input ssh
R1(config-line)#login local
```

This ensures that we only want to use SSH (not telnet or anything else) and that we want to check the local database for usernames. Let’s create a user:

```
R1(config)#username admin password my_password
```

Everything is now in place. We should be able to connect to R1 through SSH now.

## Eksempel
```
R1(config)#enable secret ThisisaSecret
R1(config)#service password-encryption
R1(config)#security passwords min-length 10
R1(config)#ip domain-name netsec.com
R1(config)#username netadmin password Ci$co12345
R1(config)#line vty 0 4
R1(config-line)#transport input ssh
R1(config-line)#login local
R1(config-line)#exit
R1(config)#crypto key generate rsa
The name for the keys will be: R1.netsec.com
Choose the size of the key modulus in the range of 360 to 4096 for your
  General Purpose Keys. Choosing a key modulus greater than 512 may take
  a few minutes.

How many bits in the modulus [512]: 1024
% Generating 1024 bit RSA keys, keys will be non-exportable...[OK]
```