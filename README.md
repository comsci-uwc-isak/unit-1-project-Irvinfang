![CarRental](logo.png)

Car Rental Minimal App
===========================

A car rental management minimal app in Bash.

Contents
-----
  1. [Planning](#planning)
  1. [Design](#design)
  1. [Development](#development)
  1. [Evalution](#evaluation)

Planning
----------
### Definition of the problem
The car rental program can be divided into 8 parts which are to install the system, create documentation (user manual), create a car, record a trip, query the trip history of a car, edit, and delete the car, and being able to store the system (backup). For creating a car, the user has to input the license plate, car brand, model, and the maximum capacity in the system for it to recognize and confirm the vehicle. By querying and editing the trip and trip history of a car, the program has to require an easy manual for the user to input the distance of the trip. As for the backup system, it requires a script that copies all the files to the backed-up storage (ex: USB). 
### Proposed solution
I decided to use the bash program to create a series of scripts that can function for the car rental program, and the reason I used bash to create this program is because it is easier to create on the computer, and also because this is the language that I'm currently learning. The way this program works is to create the car profile, and after that the user has to input the details of the car (license plate, car brand, model, and the amount of passengers it can obtain). If the user wants to record the trip distances, they can simply just input the license plate of the car into the recording program and it'll show the total distance the car has traveled.
### Success Criteria
These are outcomes that can be measured
1. A car can be created
2. A trip can be recorded for a given car
3. A summary (total distance travel, average) of trips can be requested
4. A car information can be edited
5. A basic working backup system is available
6. The user can easilly (name notation, documentation) underdstand the commands
7. Installation is **simple**, it does not require additional software, one step process
8. A car information can be deleted

9. The application can be uninstalled

Design
---------
### First sketch of system
![CarRental](System.jpg)
**Fig. 1** This diagram shows the main components of the minimal rental app.
It includes the input/output and main action

### Table for test plan

Development
--------
### 1. Script for installation
The script below creates the folder structure for the application
```.sh
#!/bin/bash

#This progrsm creates the folder structure for the minimal rental app

echo "Starting installation"
echo "Installing in the desktop (default). Press enter"
read
cd ~/Desktop

#create app folder
mkdir RentalCarApp

cd RentalCarApp

mkdir database
mkdir scripts
echo "Installation complete successfully"

```
This script meets the requirement of the client for a simple installation,
however, it could be simplified so that the user does not need to execute the program by typing ``bash install.sh``

### 2. Script for uninstallation
This script will delete the currently installed folders
```.sh
#!/bin/bash

#This program deletes the currently installed folders

echo "Starting uninstalling"
echo "Press enter to uninstall"
read
cd ~/Desktop

#delete app folder

cd ~/Desktop
rm -R RentalCarApp

echo "uninstallation complete successfully"

```
This script meets the requirement of the client for a simple installation and uninstallation. h
However, it could be simplified so that the user does not need to execute the program by typing bash install.sh

### problem solving
1. How to detect if a word's length is odd or even
```.sh
if [ $len%2 -eq 0 ]
```
2. How to create an uninstall program
```.sh
rm -R AppFolder
```
### Developing the action Create new car
This process involves the inputs _,_,_,_, and the outputs:
The following steps describe the algorithm
1. Get the inputs as arguments `$1,$2,$3,$4`
2. check number of arguments (4) `$#`
3. Store new car inside `maincarfile.txt`
4. Create file for recording trips as plate.txt
`echo "Lxq912 nissan 2000 8" >> maincarfile.txt`
`echo " " > plate.txt`

```.sh
#!/bin/bash

#This program creates a car given four arguments
#License Maker Model Passengers

if [ $# -ne 4 ]; then
	echo "Error with the number of arguments"
	echo "Enter License Maker Model Passengers"
	exit
fi

#number of arguments is correct, continue
license=$1
maker=$2
model=$3
pp=$4

#this creates a new line in the file maincarfile.txt inside CarRentalApp
echo "$license $maker $model $pp" >> ../Database/maincarfile.txt
echo "" > ../Database/$license.txt

bash frame2 "Installation Completed"

```
### Developing the action Record
1. Get the arguments (2) and check
2. check that the car exist (check if a file exists in bash)
* test license.txt
* -f license.txt
3. add a new line to the file license.txt
4. End

*line to = >>

```.sh
#!/bin/bash

#This program records a trip in the file of a car provided
if [ $# -ne 2 ]; then
	echo "Error with the number of arguments"
	echo "Enter license distance"
	exit
fi
km=$2
license=$1
#check if file exist
if [ ! -f "$license.txt" ]; then
	echo "Car does not exist"
	exit
fi
echo "$km" >> $license.txt
bash frame2 "Trip recorded successfully"
```

### Developing Backup Files
There are two methods for backing up the data, one being copying the database to another folder on the desktop, and another being copying the files into a USB stick

#### Option 1 (Desktop)
This code backs up the data to a seperate folder on the desktop
```.sh
#!/bin/bash
# This program creates a backup of the database folder in the app folder

# Starting
echo "Backup starting"

# Navigate to the desktop to create a new folder (backup/)
cd ~/desktop/
# If theres already a folder called "backup", it is removed
rm -r backup
mkdir backup
# Creats subfolder (backup/dataBase/)
cd backup
mkdir dataBase

# Copies all (*) the files from the dataBase folder 
# to the new folder (backup/) and subfolder (backup/dataBase/)
cp ~/desktop/RentalCarApp/dataBase/* ~/desktop/backup/dataBase/
```

#### Option 2 (USB)
This code is for backing up to a USB
```.sh
# Save to a usb stick

echo -n "What is your USB stick called? "
read usbName

cd /Volumes/%usbName/
# If theres already a folder called "backup", it is removed
rm -r backup
mkdir backup
# Creats subfolder (backup/dataBase/)
cd backup
mkdir dataBase

# Copy files to USB stick
cp ~/desktop/RentalCarApp/dataBase/* /Volumes/$usbName/backup/dataBase/
```
### Developing the Summary files
This code gives the user a summary of the distance driven by a single car. We can split
```.sh
#!/bin/bash
#This is an example script that solves the smaller problem for the action summary
#Read a txt file line by line
#Split a line by spaces
#Add thw first word in the line
License=$1
FILE="../Database/$License.txt"

#Saves the total km
totalkm=0

#Reads the text file line by line
while read line
do
  #bash splits a line by spaces
  for km in $line
  do
    #add all the km
    ((totalkm=$km+$totalkm))
    break
  done
done < $FILE

#4 show very nicely of the total km traveled
bash frame2 "Total km traveled is $totalkm"
```

### Developing Help files
We will be using man pages to create a help file, almost all UNIX like oses comes preinstalled with man pages. It is a document processing system developed by AT&T for the Unix operating system.
Below is the code created to explain the create.sh action:
```.sh
.TH man 6 "29 Oct 2019" "1.0" "create man page"
.SH NAME
create \- Creates a new car
.SH SYNOPSIS
bash create [license] [model] [color] [passengers]
.SH DESCRIPTION
create is a bash program that allows to create a new car in the database
.SH AUTHOR
Irvin Fang
```
Evaluation
-----------
Test 1: A car can be created and stared in the database
For this purpose we will create the file testCreate.sh. This is called software testing

The **first** test is to check for the file
```.sh
#!/bin/bash

#This file checks if the action create successfully addsa new car.

#step 1: navigate to the folder containing the create.sh file
cd ../scripts/
if [ -f "create" ]; then
        echo "File exists, test will start now"
else
        echo "File create.sh doesn't exist. Test Failed"
fi
```
This file checks all the criteria.
The option -f in the if function checks for a file in the working folder


The **Second** step is to use the create script to create a new car, in this example, I will be using TXM901 Nissan red 9 as an example. bash create.sh TXM901 Nissan red 9

The **Third** step is to check if the .txt file was created inside the database folder with the license number
```.sh
#step 2: Use the create script to record a new car TXM901 nissan red 9
bash create TXM901 nissan red 9

#step 3: check that a txt file was created inside the database folder with
#the license number
cd ../Database
if [ -f "TXM901.txt" ]; then
        echo "Test One: File with the license place created successfully. passe$
else
        echo "Test one: file with license number not found: failing"
fi
```
The **Fourth** step is to check if the last line of the mainCarFile.txt is "TXM901 nissan red 9"
```.sh
#Step 4: Check if the last line of the mainCarFile.txt is "TXM901 nissan red 9"
# Saves the last line of mainCarFile.txt into the variable lastline
lastline=$( tail -n 1 mainCarFile.txt )

# Checks if the last line is equal to the test case
if [ "$lastline" == "TXM901 nissan red 9" ]; then
    echo "Test completed successfully. File created, and information added to mainCarFile.txt"
else
    echo "Test failed. No TXM901 in mainCarFile.txt"
fi
```
*lastline=$( tail -n 1 mainCarFile.txt ) is used to save and store the last line of any text file into a string.



