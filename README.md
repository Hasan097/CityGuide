# CityGuide

## WorkFlow
The genral work flow of the app is as follows:
1. App detects a beacons and its values i.e. Beacon ID, RSSI, etc.
2. The app reports the beacon ID to the server and then recieves the details of that beacon from the server
3. To avoid repetitiveness, each unique details are checked and written to a file within the app
4. Once all detected beacons are accounted for the app then reads the values of the listed beacons from the file
5. The beacon values are put in a number of variables to form a matrix which will be used for path finding
6. The matrix takes very little time to configure and once configured the user can ask the app for navigation
7. The user inputs the lable of their destination into the app and the app starts its path finding process
8. Once its found the best route the app then speaks to the user using TTS commands and guides them to the destination
9. Each beacon has a threshold which the app detects to make sure if it is within the beacons range
10. Once the destination is reached a destination flag is set and the app acknowledge and informs the user

## Beacon Data
NOTE: Any variable that is -10 is assumed to be a null value  
  
The database contains the details of the beaons as follows:
1. Beacon ID 
2. Group ID (Defines the group/building associated to that beacon)
3. Location Name
4. Others (Could be an alias or a paragraph about the said point of interest)
5. Number of sensors (How many beacons could one beacon be adjacent to)
6. Node (The node number is the variable that our path finding function will use to find the best route)
7. Threshold (Defines the proximity range of the beacon)
8. Direction
9. Level (The floor where the beacon is setup)
10. north, south, east, west, north east, north west, south east, south west, and their distances makes 16 variables
11. Each direction indicates a beacon, so if current beacon is 0 and there is beacon 1 to the north, the variable north will contain 1
12. North distance contains the distance in meters between the current beacon (0) and the one placed north (1)

## TTS
- There are two forms of TTS (Text To Speech) functions in the app. One is defined by the variable `talk` and the other is `speakout`.
- Most of the communication is done using `talk`
- Speach recognition part of the app is done using a combo of `talk` and `speakout`
- `talk` works when a function completes its job
- `speakout` can be used to provide an immediate response without having to wait for a function to end its task

## Funtions
A few functions to note:
- `searchingTime` implements a timer for searching locations and sets a list of all detected locations
- `searchResultAnnouncement` provides interactive vocal reponses to the user 
- `beaconSighting` is the function that helps detect beacons and make calls to the server for each beacon detected
- `loginFunc` helps connect to the server 
- `searchedFinish` function helps implement voice instructions to the app
- `evacuationMode` is used in case of evacuation emergency (Currently not implemented)
- `explorationMode` is used for free roam. Also mentions which point of interest or beacon is the closest
- `readFile` reads from the file that contains beacon values
- `indoorWayfinding` helps find the best route for indoor navigation
- `serverInquiry` Obtains the server details and sets the variables to the data
