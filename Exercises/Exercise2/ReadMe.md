# OOP Training

> This is the second of a set of exercises that follow the evolution of a program to manage renovation projects. This set is cumulative and will build upon previous exercises.

## Overview

For this exercise, you will append methods to your class library project. You will create a Console Application (.NET 6). You will code a Unit Tests project that will inform you if your work will meet specifications. 

### General Validation Rules

All validation is to be performed by throwing exceptions. Here are some general requirements.

- Exceptions must have meaningful error messages with keywords (ex: positive, minimum).
- Use indicated error messages where specified.
- Error messages must include details about the limits for acceptable values.
- Measurements must always be positive and non-zero numbers. Measurements are to in whole number increments (eg: 254) (all measures are in metric centimeters).
- All string information must contain text. Null, empty, and plain white-space text is not allowed. Sanitize your strings by trimming the leading and trailing whitespace.
- Use constants for minimum values.

### The `Wall`

Extend the `Wall` class by adding the following methods.

- Add **`Parse`** and **`TryParse`** methods to instantiate a Wall from a string. The string's format is expected to match the formatting of the `ToString()` method.
  - In the `Parse` method, throw a [`FormatException`](https://docs.microsoft.com/dotnet/api/system.formatexception?view=net-5.0) if the supplied string does not match the expected format.
  - In the `TryParse` method, explicitly return a `bool` indicating if the parsing was successful. The parameters for this method are to be a `string` and an `out` parameter for the `Wall` type.
- Add method **`DeleteOpening()`**
  - This method will remove an existing opening in the wall. 
- Add method **`ReplaceOpening(Opening opening)`**
  - This method will replace the opening in the wall. Ensure the opening meets the 90% validation on wall openings. Ensure a opening parameter was pass into the method. Use the `ArgumentNullException` message if the parameter is missing its value. Use `ArgumentException` for the 90% validation.

### The `Room`

Extend the `Room` class by adding the following method.

Add method `RemoveWall(string planid)` 

- This method will locate and remove the wall matching the parameter. If the parameter value is missing throw an `ArgumentNullException`. If the wall cannot be located, throw an `ArgumentException` message containing the supplied parameter in a string. Remove the wall if a matching wall exists.

### A Console I/O Driver : Program.cs

Create a new console project in your solution. Call this new project `RenoDriver`. This project will be used to test the reading and writing of various files. The program will read a CSV text, write a JSON file and read the written JSON file.

### Const FileNames

Create 3 const strings at the being of your program. These strings will be assigned the filename for your good csv file, good json file and your bad csv file. Use relative addressing to the position of the files in your RenoSystem folder relative to the location of your .exe file.

### Reading a csv routine

Create a text file (extension `.csv`) holding the comma-separated values for five good walls, one wall per line. At least: one wall must **not** have an opening, one wall must have a door opening and one wall must have a window opening. The other 2 walls can be created using your choice of data.

Example line: `Brd1,367,244,White,Window,100,120,12`

Create a void method which will receive 2 parameters representing a filename (string) and an instance of room. Read all the lines using the technique review in class by your instructor. Parse the read lines into individual walls using the `Wall.TryParse` method. Process **all** read lines and output **any/all parsed** exceptions. Add the valid walls to a new room.

#### Exception testing

Once you have the good 5 record CSV working, copy the file and intermix 3 bad records. One record will have a missing value (insufficent values on record). One record will have a bad value for the csv value (example a negative measurement). One record will have a duplicate wall planid. Rerun your program.

### Writing a JSON file
Create a method which receives a string representing the JSON filename and an instance of `Room`. The method returns nothing (void).

 Save the room information [formatted as JSON](https://docs.microsoft.com/dotnet/api/system.text.json.jsonserializer?view=net-5.0) to the JSON file (incoming parameter). Use your good data from your csv file to write out.

### Reading a JSON file
Create a method which receives a string representing the JSON filename and returns an instance of `Room`.

 Read the room information [formatted as JSON](https://docs.microsoft.com/dotnet/api/system.text.json.jsonserializer?view=net-5.0) from the `JSON` file you wrote. Return the Room data from the method. Display the Room data after returning from the read method.

 **HINT:** Remember to place the annotation `[JsonInclude]` in front of any public fields.

### Display Current Room
Use the supplied routine to display the contents of a Room. 

----

## Create Unit testing project

 Create a new unit testing project called `Ex2UnitTesting`. The following table indicates the unit test cases to create. Unit Test names are left up to you. The required tests are outlined in the following table. 

#### Unit Tests

 | Class item | Success/Fail | Specifications |
| ---- | --------- | ------------------- |
| DeleteOpening  | Success | Removes an opening from the Wall instance.   |
| DeleteOpening  | Fail | There is no opening in the Wall instance. Use ArgumentExpection().   |
| ReplaceOpening  | Success | Replaces an opening in the Wall instance. |  
| ReplaceOpening  | Fail | Missing opening instance parameter value (ArgumentNullException); 90% validation failure (ArgumentExpection) |  
| RemoveWall  | Success | Removes a wall from the Room instance | 
| RemoveWall  | Fail | Missing Wall instance parameter value (ArgumentNullException); PlanId not found (ArgumentExpection) | 


----

## Evaluation

> ***NOTE:** Your code **must** compile. Solutions that do not compile will receive an automatic mark of zero (0).*
> 
> If you are unable to get a portion of the assignment to compile or work, you should:
> - Comment out the  portion of code
> - Identify the reason for the commented portion (such *as does not compile* or *does not work cause an abort*)

Your assignment will be marked based upon the following weights. See the [general rubric](../../README.md#generalized-marking-rubric) for details.


| Earning | Weight | Deliverable/Requirement | Comment |
| ---- | --------- | ------- | ------------- |
|   | 3 | Wall Modifications |    |
|   | 3 | Room Modifications |    |
|   | 3 | Driver and File I/O |   |
|   | 1 | CSV Files of Walls |    |
|   | 5 | Unit tests |   |
|  | -4 | Other concerns and penalities (Unit Testing does not compile/run; commits reflect incremental development) max -4 |   |
| ---- | ----- | --------- |  ------ |
|   | **15** | **Total Weight** | ------ |
| ---- | ----- | --------- | ------ |


----

[Return to exercises](../../README.md)


