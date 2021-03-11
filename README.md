# FowsniffCTF
Here are the steps I took to complete this CTF:

First, deploy the machine:

![image](https://user-images.githubusercontent.com/53369798/110733884-c01c1000-81f4-11eb-9580-5cd76e738ddc.png)

Next, I conducted an Nmap scan on the machine using the following command:

![image](https://user-images.githubusercontent.com/53369798/110734103-24d76a80-81f5-11eb-851c-69e300597e6f.png)

After checking through the report, I have determined that 4 ports are open:

![image](https://user-images.githubusercontent.com/53369798/110745928-07f96200-820a-11eb-82d5-b2078785d2d9.png)

As the only useful port at this point of the CTF is 80, we can go ahead and investigate their webpage for anything that would help us further enumerate. Doing so lead us to figure out that their Twitter account has been hacked:

![image](https://user-images.githubusercontent.com/53369798/110746587-041a0f80-820b-11eb-8437-cd4baf9feec3.png)

Now knowing this, we can conduct a Google search to discover the aftermath of their most recent hack:

![image](https://user-images.githubusercontent.com/53369798/110746801-5824f400-820b-11eb-823a-87b412b51555.png)

Looks like the hackers prefer to make their prescence known, they even pinned a tweet that reveals a whole lot of leaked passwords:

![image](https://user-images.githubusercontent.com/53369798/110747436-6293bd80-820c-11eb-9a30-b07489bc88de.png)

Here is the most useful information from the pastebin for the leaked passwords, incluiding a mention towards their POP3 services being quite insecure:

![image](https://user-images.githubusercontent.com/53369798/110747699-b900fc00-820c-11eb-8a80-6ca0fe30ac74.png)

Taking action, I begin the process of cracking the hashes by creating a text file containing the available hashes:

![image](https://user-images.githubusercontent.com/53369798/110748395-a76c2400-820d-11eb-8ea7-6cc167fda259.png)

![image](https://user-images.githubusercontent.com/53369798/110748537-d84c5900-820d-11eb-815a-693238c97f43.png)

Now, I'll go ahead and crack these hashes using John The Ripper:

![image](https://user-images.githubusercontent.com/53369798/110748684-13e72300-820e-11eb-981c-0af6b6466b3e.png)

After running the command, here is the output:

![image](https://user-images.githubusercontent.com/53369798/110748878-5b6daf00-820e-11eb-933c-a32483db9ced.png)

Now that we have both the desired usernames and passwords to use, we can go ahead and use Metasploit to force our way into the POP3 service. Let's set up the module we'll being using:

![image](https://user-images.githubusercontent.com/53369798/110749180-bf907300-820e-11eb-8cba-c61deb46b426.png)

