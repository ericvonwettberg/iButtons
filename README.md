# iButtons
Code for processing iButton data loggers

The iButton Programs, written almost entirely by Manny Dacosta, are a set of Matlab programs, scripts and functions generated in order to process data collected by iButtons.
What follows are the set of commands that are required to process iButton data into a compact useable form.

1) Load iButton Data
	command: LoadiButtonData
% The raw iButton data files must first be loaded into Matlab. Use this program to load the Thermochron and Hygrochron data. Note: the files must be in '.csv' format
% and have the following naming scheme: [site]_[location]_[sensortype(#)].csv
% It generates a set of save files for humidity and temperature with the following naming scheme: iButton[type]Data_[date].mat



2) Correct iButton Data (For Hygrochron iButtons only)
	command: CorrectiButtonData
% The humidity data loaded into Matlab will need to be corrected using calibration standards. The corrections include: temperature correction, humidity correction,
% temperature compensation and saturation drift compensation. The output data will merge temperature and humidity readings from the same iButton, and it will contain
% all steps of the correction process. The program will require humidity and temperature data from the Load iButton Data program having the following naming scheme:
% iButton[type]Data_[date].mat. Calibration standards will required in order to perform the calculations. The file that conatins these standards should be of format
% '.csv' and contain the following columns of information (with headers): [Site] [Location] [Sensor] [Device Address] [Line1] [Line2]
% A corrected save file is output with the following naming scheme: iButtonHTData_[date].mat



- At this point the user may skip to step 4 if there is not enough data, or no desire, to generate site average data. After any of the following steps, the data may
	be exported to excel. See step *.


3) Determine Site Average Values
	command: DetermineSiteAverage
% A site-wide average of all sensor readings can be generated. Sensor data from Thermochron and Hygrochron sensors are averaged separately due to differing degrees of
% precision between the two types of temperature sensor. The expected input for this program have the following naming scheme: iButton[type]Data_[date].mat where the
% two expected types are T or HT. The output is an iButtonAData_[date].mat file. If a site did not have multiple sensor data available then a iButtonALeftovers_[date].mat
% file is created which includes this data. **Need to go in and have iDataExtract adjust for loss of power



4) Sort iButton Data
	command: SortiButtonData
% The data is sorted into time-of-day arrays (morning,day,....). The user is asked to load a file: iButton[type]Data_[date].mat Where type is either A for the site
% averaged data or T/HT for the original data files. The iButtonALeftovers_[date].mat file may also be selected, if it exists. The ouput is a iButtonSData_[date].mat
% file that contains the data sorted by time-of-day.



5) Determine Daily, Weekly and Monthly Interval Averages for the Data
	command: DetermineIntervalAverages
% This program will only recognize data SORTED by time-of-day, held in iButtonSData_[date].mat file. Three tables are generated for each set of data with the calculated
% averages at a daily, weeklky and monthly inteval. The output is a file iButtonIData_[date].mat




*) Exporting Table Data to Excel
	command: TableFileProgram
% Write tables to .csv files using table properties to generate file name.

EXTRAS
- Rename raw .csv data files from iButtons
    command: RenameiButtonDataFile
% Renames .csv data files from iButtons to a format that can be used by the Load iButton Data program.

- Correct raw iButton data files
    command: DataCorrection
% Takes in .csv files and changes the standard comma based point-decimal system, for non-whole numbers, to the US period based form.
% This is necessary as the .csv (comma seperated values) file system mistakes the decimal-point comma for a delimiter.

- Extract Data for ANOVA
    command: iDataMatrix / iDataSMatrix
% The tables containing the data to be extracted must be loaded to the workspace first. 
% Extracts data from data tables for use in ANOVA calculations. Two versions exist, for sorted and non-sorted data.

- Determine minimum temperatures and points of interest
    command: DeterminePoI
% Determines minimum temperature for average Thermochron and Hygrochron data, this includes overall-site, night, day and monthly mins. It also determines the number of
% values below a certain threshold (a Point of Interest), including overall-site, night, day and monthly counts.

- Histograms
 command: 

If there are any further questions in regards to the use of these programs questions may be sent to edaco001@fiu.edu
- Manny D.

%v1.0
