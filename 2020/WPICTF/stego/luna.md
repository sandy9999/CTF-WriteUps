So, the tar file had a 1.png, a zip file.
exif/strings on 1.png gave the password for the zip **awcIsALegendAndIHopeThisIsAStrongPasswordJackTheRipperBegone**  
unzipping the file gave justincase.png, jut. the png said that it was exported via gimp. Wasn't sure what to do with jut. Thought it was a broken png, ran through some tools, no leads. Tried detect files on cyberchef, found zlib. Extracted via binwalk, found non empty zlib but discarded.

the zlib had a png hex dump which was the flag :(

