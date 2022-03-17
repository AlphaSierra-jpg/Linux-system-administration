# __The basics of Linux system administration__

## __Summary__

The purpose of this README is to simply administer a Linux system. <br> In this tutorial we will create users and add them to two new groups.<br> Then we will give administrator rights to a group. <br>Then we will see how to generate an RSA key to connect to a machine without a password.<br> Finally we will finish with the installation of WordPress 

<br>

- - - -

## __Initialisation__

One of the first commands to run on a new Linux system is this one:

```
sudo apt update -y && sudo apt upgrade -y
```
It allows to update the system package 

<br>

- - - -

## __Step 1__


This command allows you to create a user with his home folder (his user folder). Once executed you will have to enter the user's password and confirm it. Then you can enter the user's information, otherwise you can prove that you have not entered anything by pressing the enter key. You will only have to confirm with the y key. If any of the information entered is wrong press n and enter the information.

_Command:_
```
sudo adduser bob --home /home/bob/
```

_Output:_

> Adding user '`bob`' ... <br>
    Adding new group '`bob`' (1010) ... <br>
    Adding new user '`bob`' (1010) with group '`bob`' ... <br>
    Creating home directory '`/home/bob/`' ... <br>
    Copying files from '`/etc/skel`' ...  <br>
    Enter new UNIX password: <br>
    Retype new UNIX password: <br>
    passwd: password updated successfully <br>
    Changing the user information for bob <br>
    Enter the new value, or press ENTER for the default <br>
            Full Name []: <br>
            Room Number []:  <br>
            Work Phone []: <br>
            Home Phone []: <br>
            Other []: <br>
    Is the information correct? [Y/n] y <br>

<br>

You will just have to modify __`bob`__ by the name of the other users you have to created 
<br>
To create a group follow the command below, you can modify __`groupname`__ by the name of the group you want and __`12345`__ by the desired gid
```
sudo addgroup groupname --gid 12345
```
Now to add a user to a group you have to use the command below in which you modify __`examplegroup`__ by the name of the group in which you want to add your user and __`exampleusername`__ by the user in question 

```
sudo usermod -a -G examplegroup exampleusername
```
<br>

- - - -

## __Step 2__

The purpose of this step is to assign administrator rights to the group you created earlier. For that we will modify the sudoers file with the command below. 

```
sudo visudo
```
Then you will add this line to the file in the file. You can replace __`examplegroup`__ with the group that will inherit the administrator rights.
```
%examplegroup ALL=(ALL) NOPASSWD:ALL
```
To leave the Document press the keys: ⌃X then ↩ <br>
If the list of keys to use is not displayed at the bottom of your screen you can try using this keystroke sequence: __:q__

if you want to test if the changes have taken place, you can use the following command by replacing __`username`__ with the name of the account on which you want to change and test with the second command

```
su username
sudo apt-get install vim
```

<br>

- - - -
## __Step 3__
In this step we will set up an RSA key. This key will allow us to connect to the machine without using a password. For this we will need  


pour virer mdp, changer ca vers ca
```
sudo nano /etc/ssh/ssh_config
```
```
PasswordAuthentication yes -> PasswordAuthentication no
```


sur le pc qui veut se co
```
ssh-keygen
```

```
cat ~/.ssh/id_rsa.pub | ssh bob@172.16.235.12 "mkdir ~/.ssh -p && cat - >> ~/.ssh/authorized_keys"
```
- - - -
## __Step 4__
