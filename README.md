# DigiVet_audio
DigiVet 3.0

## Prerequisites
- A Linux(Debian)-based system, such as a Raspberry Pi (2nd or 3rd generation), or a computer running Debian.
- The Kasadaka image (see next paragraph).
- If preferred, a GSM dongle, such as the Huawei E169.

## Install Kasadaka image
Download the Kasadaka image from the following Wiki: https://github.com/abaart/KasaDaka/wiki/Virtual-KasaDaka. Once the download has completed, you may import it in the Debian version that you are using as described in the Wiki.

Loging into the system can be done by entering the user name and password, which are both: kasadaka.

Place DigiVet on the Kasadaka
Use the following commands to replace the existing folders and files by the ones needed for DigiVet.

kasadaka@kasadaka:~$ cd KasaDaka/html
kasadaka@kasadaka:~/KasaDaka/html$ rm -rf audio
kasadaka@kasadaka:~/KasaDaka/html$ git clone http://github.com/Rromulus/DigiVet_audio.git

You should now be able to see the DigiVet subdirectories that are cloned from this github to the html directory. In the audio directory, the English path: /html/audio/en/audiofiles_english/ and the French path: /html/audio/fr/audiofiles_french, audiofiles are stored there, as well as the English XML files (path: /html/DigiVet/EN/) and the French versions (path: /html/DigiVet/FR/).

## Adjustment Asterisk extensions file
The last adjustment we should make before testing the application is to replace the extensions.conf file that is used to invoke the XML files.

kasadaka@kasadaka:~$ cd KasaDaka/etc/asterisk
kasadaka@kasadaka:~/KasaDaka/etc/asterisk$ sudo nano extensions.conf
sudo password for kasadaka: kasadaka

After entering the kasadaka sudo password, a screen will pop up that allows you to make changes to the extensions.conf file. Replace the 10th and 14th line in the file such that they match the following two lines respectively:

;10th line replacement
exten => _.,n,Vxml(http://127.0.0.1/DigiVet/EN/welcome.xml)

;14th line replacement
exten => kasadaka,n,Vxml,(http://127.0.0.1/DigiVet/En/welcome.xml)

Save and exit the file by using Ctrl + X, then Ctrl + Y, followed by ENTER. Since the Asterisk file has been adjusted, we should now reboot the system. This can either be done manually or by typing the sudo reboot command in the Terminal. 

## Calling DigiVet
Once the system has rebooted itself, log in and use the Applications Menu to navigate to the softphone called Linphone. This is located under Internet >  Linphone. The softphone will open with the appropriate SIP already entered, namely:  <sip:kasadaka@127.0.0.1>. Dial this number and the system should internally call DigiVet. 

Of course a dongle can also be used to call DigiVet. Insert the dongle containing a simblock-free SIM-card and dial the phone number belonging to the SIM-card to access DigiVet.
