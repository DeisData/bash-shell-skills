# Hashtag denotes a comment. The line will be skipped

# Change to your desktop 
cd ~/Desktop

# Make a new folder for our fake data
mkdir fake_data
cd fake_data

# Create some empty files.
touch 2020-06-09-data.txt
touch 2020-06-09-calibration.txt

# Make sure the new files are created. Notice we can combine options)
ls -Fs

# Let's add some info to our file and confirm it with the editor (spoiler alert - redirects!)
echo Hello World > 2020-06-09-data.txt
nano 2020-06-09-data.txt

# Let's edit and add information to another.
nano 2020-06-09-calibration.txt
