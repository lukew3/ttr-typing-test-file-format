# typingTestRecord
A standard for saving and replaying typing tests. 

## About
The file is structured in json format. The top fields are: `ttrVersion`, `metadata`, and `data`. `ttrversion` contains a string stating the version of ttr used to generate this file. `metadata` contains information about the test, such as who took it, when they took it, what software was used, and what type of test it was. `data` contains an array of event objects, each which has a time, event, and if the event added a letter, a letter field will be included.

## Event types
| type | meaning |
|------|---------|
| 0 | Test start |
| 1 | Correct letter |
| 2 | Incorrect letter | 
| 3 | Submit Correct Word |
| 4 | Submit Incorrect Word |
| 5 | Go back a letter |
| 6 | Go back a word |
| 7 | Delete an entire word | 
| 8 | Test end |
