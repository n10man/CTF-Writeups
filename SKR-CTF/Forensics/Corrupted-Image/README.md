
In this challenge we will be dealing with a file that has been corrupted, the challenge's purpose is to teach the player how to retrieve and get back data from a corrupted file. 
![[Pasted image 20260605081634.png]]

The hint on this challenge asks us "what needs a signature?" indicating that we will be dealign with magic numbers and signatures. 
![Pasted image 20260605081650.png](app://6403d3dc25f2c0506e862d2185532b8985b5/Users/ahmed/Documents/Obsidian%20Vault/Pasted%20image%2020260605081650.png?1780618610788)
What are [magic numbers?](https://gist.github.com/leommoore/f9e57ba2aa4bf197ebc5)

![[Pasted image 20260605081707.png]]

After downloading the corruptedFile from the challenge 
![[Pasted image 20260605120614.png]]

Running the file and exiftool commands on the corruptedFile give us no useful information, which means that we will have to be using a hexeditor to get information for this file. The hexeditor that i am using here is going to be xxd (A hexeditor which is built into kali linux) and ghex editor later on (this one we would have to install)


![[Pasted image 20260605081840.png]]

running the xxd command on the corruptedFile with the head and tail pipes show us the top most and bottom most of the files signatures, and at the end of the tail signature , we can see **IEND** , and with the google search below as to what IEND stands for when its a signature 
![[Pasted image 20260605121120.png]]
we can see that IEND marks the end of a PNG file, which indicates that this file was originally a PNG file, but looking at the head pipe we can see the magic number at the start with its signature just being "SKR" which isnt a valid file format. This means that the original file has been tampered with and switched from PNG format to SKR, and our job is to reverse that tempering in order to retrieve the flag


Now we will install ghex editor using the command : 
sudo apt install ghex -y 
![[Pasted image 20260605082354.png]]
ghex is a GUI based hex editor which would make editing the magic numbers easier 

![[Pasted image 20260605121459.png]]
running the ghex command on the corruptedFile then opens a window which we can interact with the magic numbers in. 

As mentioned earlier we would have to change the magic number at the beginning from SKR to PNG in order to retrieve the original file. 
![[Pasted image 20260605082523.png|697]]

Following a google search for what is the magic number for PNG we can see that the magic number / file signature for PNG in hexadecimal is 89 50 4E 47 0D 0A 1A 0A which means that we would have to change the magic numbers at the beginning of the corruptedFile to be the same as this
![[Pasted image 20260605121748.png]]



on ghex you could start by seeing the original pattern first  and we can see that 0d 0A 1A and 0A are already there which means we would only have to delete 52 and whatever is before it 
![[Pasted image 20260605121908.png]]
![[Pasted image 20260605122001.png]]

After deleting the current file signature, we would enter the beginning of the PNG file signature numbers, and with it we would see that the signature on the right of the window went from SKR to PNG which means that what we did was correct so far. 
![[Pasted image 20260605082446.png]]


after that we would save the file modification using the save button on the top right of the ghex editor ![[Pasted image 20260605122121.png]]

and we would then proceed to opening the new modified corruptedFile using the open command
![[Pasted image 20260605083303.png]]


with it we can now see that the file does show us a png of a poem by SKR, based on the flag format from SKR CTFs we know that the format is SKR{flag_inside_here} which means that whatever the poem is by SKR must have the flag for us, however not the entire poem is the flag, because by reading the poem carefully, we could notice that some letters are capitalised such as as the R in Rainbow and E in hEllo, which could mean that we must combine all these letters to form the flag inside of the curly brackets.
![[Pasted image 20260605083216.png]]

Rainbow     → R
hEllo       → E
deeP        → P
fAIR        → A, I, R
deeP        → P
aNd         → N
thouGhts    → G
kIttenS     → I, S
hEAd        → E, A
hiS         → S
readY       → Y


forming the word: 
REPAIRPNGISEASY


which forms the flag: 

SKR{REPAIRPNGISEASY}

which is our final flag and allows us to pass the challenge!
