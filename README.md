# Cyber-Defenders-Challenge-Mr.-Gamer
Write Up, Screenshots, scripts, etc. for Cyberdefenders Challenge - 98 Mr. Gamer

In this challenge, Expert Witness Files of a Lenovo Image were given. The files were of a Linux user that likes to play minecraft. The challenge was to investigate the EWF files to find out hidden information about the user. 

I first researched about Expert Witness Files on Forensics Wiki. Then I came across an article on how to mount EWF files on Linux by dfirscience.com. After a lot of errors, debugging and parallel attempts on FTK imager, Wine, Autopsy, the best way forward seemed to be to mount the images using sleuthkit and accessing chroot on the EWF images. The steps were to 

1. install sleuthkit
2. /mnt/ewf/ewf1
3. mmls ewf1
4. create logical partition /mntl. from the partition table generated by mmls,      calculate offset by multiplying length of mounted partition to 512 
![Screenshot from 2022-08-17 19-53-29](https://user-images.githubusercontent.com/24385029/203779696-00ac3fd5-3554-4797-9ddc-56526bdd0eb2.png)

5. then mount logical partition as well with 
   mount -o ro,norecovery,loop,offset=537919488 /mnt/ewf/ewf1 /mntl 
6. cd /mntl
7. ls
8. chroot
![Screenshot from 2022-08-25 16-16-34](https://user-images.githubusercontent.com/24385029/203781237-82ff6dc9-dc83-4311-895e-8324c0e7dd8b.png)

lsb_release -a for version id of ubuntu

nano /etc/hostname gives hostname

in home/.minecraft/usercache.json gives uuid of attacker
![Screenshot from 2022-08-25 22-19-36](https://user-images.githubusercontent.com/24385029/203781366-ddbfee0c-726b-41b3-9fd2-c5255a4a9edc.png)


in home/.minecraft/version.dir/version_manifest_v2.json gives sha1 hash of latest version
![Screenshot from 2022-08-25 23-02-41](https://user-images.githubusercontent.com/24385029/203781454-f99da4f8-0240-4ab3-9943-e9c409ea745f.png)


/home/rafael/.config/discord/0.0.16/modules 
nano installed.json!

gives highest module version is discord_voice

![Screenshot from 2022-08-26 16-40-45](https://user-images.githubusercontent.com/24385029/203781556-6bc0c4b6-c43d-42cf-bc74-065784024601.png)


the youtube video is found in the downloads folder it is by rick astley and the answer is found in the channel

var/lib gives vpn service as zerotier

in downloads, marshalsec/screenshots gives cookbook as binging with babish. the screenshots also show temperature as 45F

/home/rafael/.thunderbird/vrvcx2qf.default-release/ImapMail/imap.gmail.com gives inbox. opened it with gedit and found with ctrl+F the anime.

guest wifi password is also found with ctrl+F 

/home/rafael/marshalsec/poc Log4jRCE.java gives values passed to powercat that I DeBase64'ed with cyberchef.
![Screenshot from 2022-09-11 17-50-56](https://user-images.githubusercontent.com/24385029/203782151-b0511830-fde4-4097-9fcd-573aa07448d6.png)


A lot lot lot of detours later, I copied the users keyring and keystore, rebooted my PC(after unmounting the ewf), and reopened my gnome seahorse, opened the users keyring and keystore with the key provided in the hint, and found the client token.
![Screenshot from 2022-09-16 17-37-11](https://user-images.githubusercontent.com/24385029/203782092-1a508a52-4ef1-4c5b-8a94-1d3db2221d86.png)


DONE!

