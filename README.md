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

### Developing the action Record
1. Get the arguments (2) and check
2. check that the car exist (check if a file exists in bash)
3. add a new line to the file license.txt
4. End

*line to = >>

Evaluation
-----------



