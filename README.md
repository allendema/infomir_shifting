# Getting started

<details>
<summary> Seting up SSH </summary>

 

- The shipped Firmware has port 22 open for SSH-Connections.

- This is not the case if you updated the Firmware from Settings.
(You can install one with the port 22 open from: [https://soft.infomir.com/](https://soft.infomir.com/))

- By default you can use user ```root``` and ```930920``` as user and password respectivly.

- You can change that to whatever you like, and/or set up SSH to use your public key.
    - ```ssh-copy-id -i ~/.ssh/mykey root@mag_stb_IP```
    - https://www.ssh.com/academy/ssh/copy-id

</details>



<details>

<summary> Preventing "Your Portal is blocked" </summary>

- Infomir will try to connet to different domains to get a list of blocked portals.

- Download Portal domains to a file.
    - Then it will be saved to ```/mnt/Userfs/data/ad.json```
- You can create a script to remove this file on every boot.

- Open up ```vi``` to edit ```/etc/hosts```
    - ```bash vi /etc/hosts```
    - add following domains there:
    - ```0.0.0.0 stat.infomir.com```
    - ```0.0.0.0 <your STB model>.dbcs.infomir.com```

    - # If this does not do anything, alternate the NAND. 


</details>

<details>

<summary> Changing Mac Address, Serial Number, STB Model etc. </summary>

### Printing current values
- Print current MACAddres with:
    - ```/bin/sh /usr/local/share/app/bin/rdir.sh MACAddress```
 
 
- Print current Model with:

    - ```/bin/sh /usr/local/share/app/bin/rdir.sh Model```

### Changing MACAddress
- Open up ```vi``` to edit ```/usr/local/share/app/bin/rdir.sh```
    - Find this line:  
    
      ```dd if=/dev/$device bs=1 count=32 skip=$(($shft+32)) 2>/dev/null | strings -n1 | awk '{printf ("%s", $0); exit;}'```  
      and edit it to wanted MACAddres, see below.  
        
        
        
    - ``` dd if=/dev/$device bs=1 count=32 skip=$(($shft+32)) 2>/dev/null | strings -n1 | awk '{printf ("00:1A:79:00:00:00"); exit;}' ```



</details>
