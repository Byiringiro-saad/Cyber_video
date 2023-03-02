Introduction
------------


This is documentation about social engineering attack conducted through video sharing.
The scripts in funny_comedy.desktop allows you(the victim) to download and play a video file called 'funny_comedy.mp4' hence giving the attack access 
to your terminal. 


The script uses the wget command to download the file from a specified IP address (attacker's machine), saves it to the /tmp directory, and then opens 
it using the xdg-open command. The script also sends a signal to a listening socket at IP address 192.168.56.101 and port 4007 with the access to the 
terminal of the victim.


Prerequisites
--------------

Victim OS: linux mint with socat installed
Attacker OS: Kali linux with python3 installed


This is how the process goes:

* On the attacker's end:
 ----------------------

    1. Change the funny_comedy.desktop file permissions with the chmod command to elevate its privileges. with 'chmod +x funny_comedy.desktop' command
    2. Start the Python3 Server with 'python3 -m http.server 80' command

        Python3 will create a web server on port 80, making the funny_comedy.mp4 in the directory available to everyone on the network. Alternatively,
        this web server can be set up on a virtual private server for remote targets.

        The Python3 terminal must remain open until the target clicks on the funny_comedy.desktop file. If the Python3 server is not accessible when 
        the target opens the funny_comedy, no video will play, but the target's computer will still establish the Netcat connection.

    3. Start the Netcat Listener

    start listening on the port specified in the .desktop file that you shared the victim 
    use 'nc -vv -l -p <port>' command to start listening


* The victim should perfom the following actions:
  ----------------------------------------------

    1. Double-click on the funny_comedy.desktop file which will be appearing as funny_comedy.mp4 (on his machine).
    2. The script will download the funny_comedy.mp4 file from the IP address 192.168.56.101.
    3. The script will save the file to the /tmp directory.
    4. The script will open the file using the default video player on your system.
    5. The script will send a signal to the specified IP address and port number.
    6. The attacker will directly get the access to the victims terminal

NB: Socat allows the attacket to continue having access even when the video on the victim's machine is closed.
