Notes before starting: There is a method to get the flag and it is to simply install the "file" file and simply open it in the terminal, but that is the simple and quick way to get the flag and if that is what you are looking for, the flag is all the way at the end of the writuep, however if you are looking for what i am assuming is the "intended method" to solving this challenge, you could follow the writeup down below :)


For this challenge we are not given any hints whatsoever but we can get enough information as to what is required to be done from the challenge name which is called "File signature 2" 
<img width="497" height="470" alt="image" src="https://github.com/user-attachments/assets/4497a1c5-4a43-4732-b89f-742cae8ba783" />

This indicates to us that we would be dealing with a file's signature in order to obtain the flag

Installing the file given to us simply downloads a file called "file" with no extensions, i.e no .jpeg / .pdf / .csv and is simply just a file.

We then would try inspecting the file signature as to see if we can find any useful information, using the xxd command.  What is xxd ?

"xxd file | head" and we use the head pipe filter in order to only get the top 10 ASCII lines of the files signature in order to find what the file type may be 
<img width="1278" height="540" alt="3085" src="https://github.com/user-attachments/assets/1dfa38e9-7137-4be0-a5dc-f6866a0bc4d6" />

**Insert picture of what file signature is and why the first lines are the most importnat.**

from the command we entered above we could see that JFIF exists on the ASCII convertable, and with a quick google search as to what file type JFIF is we could find that it is another way of writing / uploading JPEG files

<img width="1924" height="750" alt="1981" src="https://github.com/user-attachments/assets/38de6590-0217-4324-9ab8-faaf08c3815a" />


with this information we then know that the original "file" had a .jpeg extension. 

With that information we could then insert the command "cp file file.jpeg" in order to copy the original file and attach the .jpeg file format to it 
<img width="650" height="106" alt="55394" src="https://github.com/user-attachments/assets/07f01c64-c1e3-4943-adc6-5371ebf0a2b9" />


 with that we could then open the "file.jpeg" file and view the contents inside of it 
  <img width="3404" height="1718" alt="81049" src="https://github.com/user-attachments/assets/e80f59ae-60a3-4004-8370-df1de3c63e86" />

inside of the "file.jpeg" image we could see that the flag is there, however it is mirrored, which is why we would need to use an online image rotator such as this one (LINK) and simply rotate the image which would give us the flag as we can see below

<img width="1934" height="1058" alt="53381" src="https://github.com/user-attachments/assets/17d2eb2d-fbd4-4ab7-b33c-a4f9b403be6d" />

flag: **SKR{fil3_sign4tur3_1s_1mp0rt4nt}**
