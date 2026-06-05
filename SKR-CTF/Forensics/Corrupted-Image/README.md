In this challenge we will be dealing with a file that has been corrupted, the challenge's purpose is to teach the player how to retrieve and get back data from a corrupted file.

![](Pasted%20image%2020260605081634.png)

The hint on this challenge asks us "what needs a signature?" indicating that we will be dealing with magic numbers and signatures.

![](Pasted%20image%2020260605081650.png)

![](Pasted%20image%2020260605081707.png)

After downloading the corruptedFile from the challenge

![](Pasted%20image%2020260605120614.png)

Running the file and exiftool commands on the corruptedFile give us no useful information, which means that we will have to be using a hexeditor to get information for this file. The hexeditor that i am using here is going to be xxd (A hexeditor which is built into kali linux) and ghex editor later on (this one we would have to install)

![](Pasted%20image%2020260605081840.png)

Running the xxd command on the corruptedFile with the head and tail pipes show us the top most and bottom most of the files signatures, and at the end of the tail signature we can see **IEND**

![](Pasted%20image%2020260605121120.png)

We can see that IEND marks the end of a PNG file, which indicates that this file was originally a PNG file, but looking at the head pipe we can see the magic number at the start with its signature just being "SKR" which isnt a valid file format. This means that the original file has been tampered with and switched from PNG format to SKR, and our job is to reverse that tampering in order to retrieve the flag.

Now we will install ghex editor using the command:
sudo apt install ghex -y

![](Pasted%20image%2020260605082354.png)

ghex is a GUI based hex editor which would make editing the magic numbers easier

![](Pasted%20image%2020260605121459.png)

Running the ghex command on the corruptedFile then opens a window which we can interact with the magic numbers in.

As mentioned earlier we would have to change the magic number at the beginning from SKR to PNG in order to retrieve the original file.

![](Pasted%20image%2020260605082523.png)

Following a google search for what is the magic number for PNG we can see that the magic number / file signature for PNG in hexadecimal is 89 50 4E 47 0D 0A 1A 0A which means that we would have to change the magic numbers at the beginning of the corruptedFile to be the same as this

![](Pasted%20image%2020260605121748.png)

On ghex we can see the original pattern first and we can see that 0D 0A 1A and 0A are already there which means we would only have to change 53 4B 52 (SKR) to 50 4E 47 (PNG)

![](Pasted%20image%2020260605121908.png)

![](Pasted%20image%2020260605122001.png)

The original corrupted magic number was 89 53 4B 52 which read as .SKR on the right side. We changed bytes 53 4B 52 (which spell SKR) to 50 4E 47 (which spell PNG), restoring the full correct PNG magic number 89 50 4E 47 0D 0A 1A 0A

![](Pasted%20image%2020260605082446.png)

After that we would save the file modification using the save button on the top right of the ghex editor

![](Pasted%20image%2020260605122121.png)

We would then proceed to opening the new modified corruptedFile using the open command

![](Pasted%20image%2020260605083303.png)

With it we can now see that the file shows us a PNG of a poem by SKR. Based on the flag format from SKR CTFs we know that the format is SKR{flag_inside_here}. By reading the poem carefully we can notice that some letters are capitalised such as the R in Rainbow and E in hEllo, which means we must combine all these capitalised letters to form the flag.

![](Pasted%20image%2020260605083216.png)

The capitalised letters in order are:

| Line | Capital Letter |
|---|---|
| Rainbow | R |
| hEllo | E |
| deeP | P |
| fAIR | A, I, R |
| deeP | P |
| aNd | N |
| thouGhts | G |
| kIttenS | I, S |
| hEAd | E, A |
| hiS | S |
| readY | Y |

Combining them in order gives us: REPAIRPNGISEASY

**Flag: SKR{REPAIRPNGISEASY}**
