### This will demonstrate a few command one can use to change 
### the behaviour of MAG STBs from Infomir.
 - https://www.infomir.eu/
 - https://wiki.infomir.eu/eng/set-top-box/stb-linux-webkit/



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

<details>

 <summary> Create a backup of the file first </summary>

 ```scp /path/to/rdir_backup.sh  root@MAG_IP_ADDRES:/usr/local/share/app/bin/rdir.sh```

</details>
 
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


### Changing STB Model
 - ```vi /usr/local/share/app/bin/rdir.sh```
 
 - Find ```dd if=/dev/$device bs=1 count=32 skip=$(($shft+96)) 2>/dev/null | strings -n1 | awk '{printf ("%s", $0); exit;}'``` 
 and edit it to any other Informir device from MAG or Aura series.  

 (AuraHD2 may come with the benifit of the option to install "apps" from Infomir portal ```http://apps.infomir.com.ua/```)
 
 ```dd if=/dev/$device bs=1 count=32 skip=$(($shft+96)) 2>/dev/null | strings -n1 | awk '{printf ("MAG254"); exit;}'``` or
 ```dd if=/dev/$device bs=1 count=32 skip=$(($shft+96)) 2>/dev/null | strings -n1 | awk '{printf ("AuraHD"); exit;}'```
</details>

 
<details>

 <summary> Editing env. variables </summary>

 ### Printing env. varibles
 ```fw_printenv```
 
 ### Changing env. variables
 You can change all the variables above  
 and [more](https://wiki.infomir.eu/eng/set-top-box/for-developers/stb-linux-webkit/customization/most-used-variables)  
    ```fw_setenv portal2 http://example.org/c```
 
</details>

<details>
   <summary> Load a portal with different Bootmedia bank </summary>

   ```cd /usr/local/share/app```  
   ```./run.sh $PORTAL_TO_LOAD "file:///usr/local/share/app/web/system/pages/loader/index.html?bootmedia=bank0"```  
    Where bootmedia can be ```bank0``` or ```bank1```
 
</details>

<details>

 <summary> Owerwriting cookies </summary>
   Avoid eventual tracking by cookies  
 
    echo "1" > /mnt/Userfs/cookies.ini
 
</details>

 
<details>
 <summary> Exit Vi </summary>

 To save and exit use  
    ```:wq```  

 To exit without saving changes use  
    ```:q!```

</details>
