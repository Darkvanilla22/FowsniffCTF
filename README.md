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
NOTE: The user "stone" did not have their password's hash cracked

![image](https://user-images.githubusercontent.com/53369798/110748878-5b6daf00-820e-11eb-933c-a32483db9ced.png)

Let's also answer this question from the room while we still see the passwords to everyone:

![image](https://user-images.githubusercontent.com/53369798/110753526-adb1ce80-8214-11eb-98c3-4e15e41589b5.png)

Since we need to bruteforce a login for an online service, let's go ahead and use Hydra for this. I've went ahead and seperated the usernames and passwords into different text files to be used with Hydra:
NOTE: "-f" means that the first succuessful attempt will end the attack

![image](https://user-images.githubusercontent.com/53369798/110754682-13528a80-8216-11eb-9da0-16af3bb12ce2.png)

And we have a result!:

![image](https://user-images.githubusercontent.com/53369798/110754982-6d535000-8216-11eb-8acd-4a29f1152a47.png)

So, now that we've deduced that we an applicable login to use to get into the POP3 service, let's go ahead and set up a Netcat connection to the service:

![image](https://user-images.githubusercontent.com/53369798/110755747-4b0e0200-8217-11eb-83a3-a1dc0d757f70.png)

After a quick snooping around the server I was able find this interesting message, sent by "stone". Here it is:

![image](https://user-images.githubusercontent.com/53369798/110755933-87d9f900-8217-11eb-89c7-07dc32703413.png)

Well, looks like the email gave us credentials to an SSH login that we can use:

![image](https://user-images.githubusercontent.com/53369798/110756244-f028da80-8217-11eb-8a0a-c75903bbd221.png)

Additionally, there is a second message, this time sent by "baksteen":

![image](https://user-images.githubusercontent.com/53369798/110757733-b78a0080-8219-11eb-8738-25b5e8fad716.png)

Reading through the message, here is an important piece of information that is valuable to us:

![image](https://user-images.githubusercontent.com/53369798/110757978-fc159c00-8219-11eb-8a36-8db766b39fa2.png)

So, it seems like "baksteen" hasn't actually seen the email from his manager ("stone").

Let's waste no time here and try to login to SSH using his account:

![image](https://user-images.githubusercontent.com/53369798/110758310-64647d80-821a-11eb-8a76-a5b4ae8322e9.png)

Alright, 
