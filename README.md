# typingTestRecord
A open standard for saving and replaying typing tests. 

## Structure
The file is structured in json format. 
The top level fields are: 
* [`ttrVersion`](#ttrversion)
* [`metadata`](#metadata)
* [`data`](#data)
* [`signature`](#signature)

### ttrversion
Contains a string stating the version of ttr used to generate this file. Ex: `"ttrversion": "0.0.1"`

### metadata
Contains information about the test, such as who took it, when they took it, what software was used, and what type of test it was. 
* `username` - The name of the user who completed the test
* `software` - The software used to record the test
* `time` - An integer representing the [epoch time](https://www.epochconverter.com/) when the test was started
* `prompt` - The text that the user was prompted to type
* `language` - The language that the test was conducted in
* `mode` - The mode of the test
  * Common modes are `time`, `words`, `quote`
* `length` - The length of the test
  * For time modes, length could be `60s` (60 seconds), `15s`, `5m` (5 minutes)
  * For word modes, length could be `10w` (10 words), `50w`, `2s` (2 sentences), `3p` (3 paragraphs)
* `extras` - An array of strings representing extra features that are not common enough to have their own fields.
  * Examples include: "stop on word", "expert difficulty", "funbox mirror"
* `stats` - Statistics about the test, recorded after the test was completed
  * `wpm` - The words per minute
  * `raw` - Raw words per minute
  * `accuracy` - Percent of characters typed correctly
  * `consistency` - Consistency of typed keys
  * `time` - Time spent typing
  * `characters` - List of integers counting number of correct, incorrect, extra, and missed characters

### data
Contains an array of event objects, each which has a time, event, and if the event added a letter, a letter field will be included.
* `time` - An integer representing the time that the event occurred in milliseconds from the beginning of the test
* `event` - An integer that represents the event that occurred. See [event types table](#event-types) below
* `letter` - The letter that was typed at this time. Field only exists if the event was a correct or incorrect letter

#### Event types
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

### signature
The pgp signature of the test. Assigned by the test's software providers, the signature can be checked against the provider's public key to test if the file truly came from the stated provider and contains no false data
