# File Signature 2 — SKR CTF (Forensics)

## Quick Note Before Starting

There's a fast way to get the flag: install the `file` file given to you and simply open it in the terminal. If that's all you're looking for, the flag is at the very end of this writeup.

If you're interested in what is likely the **intended method** for solving this challenge, follow the writeup below :D

## Challenge

We're given no hints, but the challenge name itself **"File Signature"** tells us a lot. It strongly suggests this challenge revolves around inspecting a file's signature to obtain the flag.

<img width="497" height="470" alt="Challenge description" src="https://github.com/user-attachments/assets/4497a1c5-4a43-4732-b89f-742cae8ba783" />

## Step 1: Inspect the File

The file we're given is simply named `file`, with no extension — no `.jpeg`, `.pdf`, `.csv`, nothing. Just `file`.

To figure out what we're actually dealing with, we inspect its file signature using `xxd`.

> **What is `xxd`?** It's a command-line tool that displays a file's raw contents in hexadecimal and ASCII format, which is useful for identifying file types based on their signature ("magic bytes") rather than relying on the extension.

```bash
xxd file | head
```

We pipe the output through `head` to limit it to the first 10 lines, since a file's signature/magic bytes appear at the very beginning of the file and are the most relevant for identification.

<img width="1278" height="540" alt="xxd output showing file signature" src="https://github.com/user-attachments/assets/1dfa38e9-7137-4be0-a5dc-f6866a0bc4d6" />

## Step 2: Identify the File Type

In the ASCII column of the output, we can spot the string **JFIF**. A quick search reveals that JFIF (JPEG File Interchange Format) is simply another standard associated with JPEG images.

<img width="1924" height="750" alt="Search result explaining JFIF is associated with JPEG" src="https://github.com/user-attachments/assets/38de6590-0217-4324-9ab8-faaf08c3815a" />

This tells us the original `file` is actually a `.jpeg` image.

## Step 3: Restore the File Extension

Now that we know the correct file type, we copy the file and give it the proper `.jpeg` extension so it can be opened as an image:

```bash
cp file file.jpeg
```

<img width="650" height="106" alt="cp command renaming file to file.jpeg" src="https://github.com/user-attachments/assets/07f01c64-c1e3-4943-adc6-5371ebf0a2b9" />

## Step 4: Open and Inspect the Image

With the extension restored, we can now open `file.jpeg` and view its contents.

<img width="3404" height="1718" alt="Opened file.jpeg showing mirrored flag text" src="https://github.com/user-attachments/assets/e80f59ae-60a3-4004-8370-df1de3c63e86" />

The flag is visible in the image — but it's mirrored.

## Step 5: Unmirror the Image

To fix this, we run the image through an online image rotator/flipper tool ([LINK]([url](https://www.img2go.com/rotate-image))) to flip it back into readable text.

<img width="1934" height="1058" alt="Flipped image revealing the readable flag" src="https://github.com/user-attachments/assets/17d2eb2d-fbd4-4ab7-b33c-a4f9b403be6d" />

## Flag

```
SKR{fil3_sign4tur3_1s_1mp0rt4nt}
```
