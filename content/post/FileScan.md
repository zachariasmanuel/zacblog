+++
date = "2016-04-13T17:18:00+05:30"
title = "Scan and copy all the music files in a directory"

+++




Hey guys! Wrting after a short break and hoping to keep it on from now on. So here's the thing. I love listening to music and I had lots of different music in my mac's music folder. I used to copy collections from my friends and add them to my music folder. And after a certain point, I started loosing track of what's there. Because each folder would have subfolders. And I found multiple copies of the same music in different folders. 

When loaded on a player, repetitions would occur a lot and this I didn't want. I decided to solve the problem and started scanning each and every folder for music, manually. And tried to copy-paste them to one destination so that repetitions will be over written. After 5 to 10 mins I realised its not an easy task since each folder had sub folders and some of them again had further sub folders. So I ended up writing a python script for scanning all my music in the main folder and copying it to an external drive. Executed the script and voila!! Problem solved. Total music size came down to 7GB from 12GB. 

If you are having the same problem and know a bit of tech, follow these steps to solve it.




1\. Assuming you already have python installed in your system. If not, then install python from this link https://www.python.org/downloads/.



2\. Copy the script given below and save to your computer. Put the file name as scan.py


```python
import fnmatch
import os
import sys
import shutil

FILE_TYPE = '*.mp3'

try:
	walk_dir = sys.argv[1]
	dest_dir = sys.argv[2]
	count = 0
except IndexError:
    print('Incorrect input')
    print('Use this format - python [FILE NAME] [SCAN_DIRECTORY] [DESTINATION_DIRECTORY]')
    print('Example - python scan.py /Users/zac/Music/ /Users/zac/Desktop/Output/')
    exit()

def copyFile(file_name, file_path, dest_dir):
	global count
	print('\t- Copying file %s (full path: %s)' % (file_name, file_path))
	shutil.copy2(file_path, os.path.join(dest_dir, filename))
	count = count+1


for root, dirnames, filenames in os.walk(walk_dir):
    for filename in fnmatch.filter(filenames, FILE_TYPE):
        copyFile(filename, os.path.join(root, filename), dest_dir)

print('Copied ' +str(count)+ ' files')
```


3\. Navigate to that path in command line and execute the python file. Add the scanning folder location and destination folder location with the command

Format  : python [FILE NAME] [SCAN_DIRECTORY] [DESTINATION_DIRECTORY]
Example : python scan.py /Users/zac/Music/ /Users/zac/Desktop/Output/



Note : You can use this code to scan any type of files. All you need to do is change the 'FILE_TYPE = '*.mp3'' part in the source code to any other extension you want.

Until next post!
Cheers. :)