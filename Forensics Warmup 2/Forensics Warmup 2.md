# Forensics Warmup 2 — SKR CTF

## Challenge Overview
This challenge is called Forensics Warmup 2, which means it would be similar to the first Forensics Warmup 1 in the tutorial section which indicates that there wont be multiple steps when we have to solve it.

![](72818.png)

## Tools Used
- `exiftool` — metadata reader built into Kali Linux

## Initial Investigation
The hint for the challenge is "what is EXIF Data?"

![](4811-1.png)

Which indicates we will be using the exiftool built into Kali Linux.

## What is EXIF Data?
EXIF (Exchangeable Image File Format) is metadata that is stored inside image files, it can contain information such as the camera model, date, GPS location, and other fields that could be useful for forensics.

## Downloading the File
When clicking the download link, we are redirected to a webpage with an image that says SAFETY.

![](safety.png)

## Retrieving the Flag
After downloading the safety image onto our system, we could use the **exiftool** command followed by the file name in order to get the output that could give us the flag.

![](image.png)

As we can see from the output of the exiftool command, the flag is visible and appears in the Artist field of the metadata.

![](13576.png)

## Flag
**SKR{Art15t_1n_1M@g3s}**