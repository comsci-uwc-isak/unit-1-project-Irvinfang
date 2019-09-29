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

Evaluation
-----------



