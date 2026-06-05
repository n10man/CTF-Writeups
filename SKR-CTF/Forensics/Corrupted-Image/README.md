# Corrupted Image — SKR CTF Forensics

## Challenge Overview
In this challenge we will be dealing with a file that has been corrupted, the challenge's purpose is to teach the player how to retrieve and get back data from a corrupted file.

The hint on this challenge asks us "what needs a signature?" indicating that we will be dealing with magic numbers and signatures.

![](Pasted%20image%2020260605081634.png)
![](Pasted%20image%2020260605081650.png)

## Tools Used
- `xxd` — hex viewer built into Kali Linux
- `ghex` — GUI based hex editor
- `exiftool` — metadata reader
- `file` — file type identifier

## Initial Investigation
After downloading the corruptedFile from the challenge, running the file and exiftool commands give us no useful information.

![](Pasted%20image%2020260605120614.png)
![](Pasted%20image%2020260605081840.png)

## Identifying the File Type
Running the xxd command on the corruptedFile with the head and tail pipes shows us the topmost and bottommost bytes of the file. At the end of the tail we can see **IEND**.

![](Pasted%20image%2020260605121120.png)

IEND marks the end of a PNG file, which indicates that this file was originally a PNG. However looking at the head pipe we can see the magic number at the start reads as "SKR" which is not a valid file format. This means the original file has been tampered with and our job is to reverse that tampering to retrieve the flag.

## Fixing the Magic Number
We install ghex using:

sudo apt install ghex -y

![](Pasted%20image%2020260605082354.png)

ghex is a GUI based hex editor which makes editing magic numbers easier. It displays two panels side by side — the left panel shows the raw hexadecimal values of every byte in the file, and the right panel shows the human readable text interpretation of those same bytes.

![](Pasted%20image%2020260605121459.png)

Running ghex on the corruptedFile opens a window we can interact with. Following a Google search we can confirm the correct PNG magic number in hexadecimal is `89 50 4E 47 0D 0A 1A 0A`.

![](Pasted%20image%2020260605082523.png)
![](Pasted%20image%2020260605121748.png)

On ghex we can see the original corrupted magic number was `89 53 4B 52` which reads as `.SKR` on the right side. We can see that `0D 0A 1A 0A` are already correct, so we only need to change `53 4B 52` (SKR) to `50 4E 47` (PNG), restoring the full correct PNG magic number `89 50 4E 47 0D 0A 1A 0A`.

![](Pasted%20image%2020260605121908.png)
![](Pasted%20image%2020260605122001.png)
![](Pasted%20image%2020260605082446.png)

We then save the file using the save button on the top right of ghex.

![](Pasted%20image%2020260605122121.png)

## Retrieving the Flag
We open the modified corruptedFile.

![](Pasted%20image%2020260605083303.png)

The file now shows a PNG of a poem by SKR. Based on the SKR CTF flag format `SKR{flag_inside_here}` we know the flag is hidden somewhere in the poem. Reading carefully we notice some letters are randomly capitalised such as the R in Rainbow and E in hEllo — collecting these in order gives us the flag.

![](Pasted%20image%2020260605083216.png)

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

Combining them in order gives us: `REPAIRPNGISEASY`

## Flag
**SKR{REPAIRPNGISEASY}**
