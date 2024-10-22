# MindMap User Guide

MindMap is a desktop app for managing patient contacts and session logs, optimized for use via a Command Line Interface (CLI) while still having the benefits of a Graphical User Interface (GUI). If you can type fast, MindMap can get your patient management tasks done faster than traditional GUI apps.

## Table of contents

- [Quick start](#quick-start)
- [Features](#features)
  - [Viewing Help](#viewing-help)
  - [Adding a Patient](#adding-a-patient)
  - [Listing all Patients](#listing-all-patients)
  - [Editing a Patient](#editing-a-patient)
  - [Locating patients](#locating-patients)
  - [Deleting a Patient](#deleting-a-patient)
  - [Clearing all Patients](#clearing-all-patients)
  - [Adding a Session Log](#adding-a-session-log)
  - [Listing Session Logs](#listing-session-logs)
  - [Exiting the program](#exiting-the-program)
  - [Saving the data](#saving-the-data)
- [Frequently Asked Questions (FAQ)](#frequently-asked-questions-faq)
- [Known Issues](#known-issues)
- [Command Summary](#command-summary)

## Quick start

1. Ensure you have Java 17 or above installed on your computer.
2. Download the latest `.jar` file from [here].
3. Copy the file to the folder you want to use as the home folder for your MindMap.
4. Open a command terminal, `cd` into the folder where you placed the `.jar` file, and run the following command:java -jar addressbook.jar
5. A GUI similar to the one below should appear in a few seconds. Note that the app contains some sample data.
6. Type the command in the command box and press Enter to execute it. For example, typing `help` and pressing Enter will open the help window.

## Overview of commands supported

- `list` : Lists all patients
- `add` : Adds a new patient
- `edit` : Edits the attributes of an existing patient
- `delete` : Deletes the selected patient
- `find` : Filters the list of patients based on a keyword
- `clear` : Deletes all contacts
- `exit` : Exits the app
- `addlog` : Adds a new session log for an existing patient
- `logs` : Shows all the logs of a single patient
- `help` : Provides a URL to the user guide

Refer to the [Features](#features) below for details of each command.

## Features

### Notes about the command format:

- Words in `UPPER_CASE` are parameters to be supplied by the user.
- e.g., in `add n/NAME`, `NAME` is a parameter which can be used as `add n/John Doe`.
- Items in square brackets are optional.
- e.g., `n/NAME [t/TAG]` can be used as `n/John Doe t/friend` or as `n/John Doe`.
- Items with `…​` after them can be used multiple times, including zero times.
- e.g., `[t/TAG]…​` can be used as `(i.e. 0 times), t/friend, t/friend t/family`, etc.
- Parameters can be in any order.
- e.g., if the command specifies `n/NAME p/PHONE_NUMBER`, `p/PHONE_NUMBER n/NAME` is also acceptable.
- Extraneous parameters for commands that do not take parameters (such as `help`, `list`, `exit`, and `clear`) will be ignored.
- e.g., if the command specifies `help 123`, it will be interpreted as `help`.

If you are using a PDF version of this document, be careful when copying and pasting commands that span multiple lines, as space characters surrounding line-breaks may be omitted when copied over to the application.

### Viewing help: `help`

Shows a message explaining how to access the help page.

- **Format**: `help`

### Adding a person: `add`

Adds a person to the address book.

- **Format**: `add n/NAME p/PHONE_NUMBER e/EMAIL a/ADDRESS [t/TAG]…​`

- **Tip**: A person can have any number of tags (including 0).

- **Examples**:
  `add n/John Doe p/98765432 e/johnd@example.com a/John street, block 123, #01-01`
  `add n/Betsy Crowe t/friend e/betsycrowe@example.com a/Newgate Prison p/1234567 t/criminal`


### Listing all persons: `list`

Shows a list of all persons in the address book.

- **Format**: `list`

### Editing a person: `edit`

Edits an existing person in the address book.

- **Format**: `edit INDEX [n/NAME] [p/PHONE] [e/EMAIL] [a/ADDRESS] [t/TAG]…​`

- **Details**:
- Edits the person at the specified `INDEX`.
- The index refers to the index number shown in the displayed person list.
- The index must be a positive integer (1, 2, 3, …​).
- At least one of the optional fields must be provided.
- Existing values will be updated to the input values.
- When editing tags, the existing tags of the person will be removed (i.e., adding of tags is not cumulative).
- You can remove all the person’s tags by typing `t/` without specifying any tags after it.

- **Examples**:
  `edit 1 p/91234567 e/johndoe@example.com edit 2 n/Betsy Crower t/`


### Locating persons by name: `find`

Finds persons whose names contain any of the given keywords.

- **Format**: `find KEYWORD [MORE_KEYWORDS]`

- **Details**:
- The search is case-insensitive (e.g., `hans` will match `Hans`).
- The order of the keywords does not matter (e.g., `Hans Bo` will match `Bo Hans`).
- Only the name is searched.
- Only full words will be matched (e.g., `Han` will not match `Hans`).
- Persons matching at least one keyword will be returned (i.e., OR search).

- **Examples**:
  `find John find alex David`


### Deleting a person: `delete`

Deletes the specified person from the address book.

- **Format**: `delete i/<IDENTITY_NUMBER>`

- **Details**:
- Deletes the person with the specified Identity Number.
- The identity number must be 9 characters long.

- **Examples**:
  `delete i/S1234567A`


### Adding a Session Log: `addlog`

Adds a session log entry for the patient.

- **Format**: `addlog i/[IDENTITY_NUMBER] l/[DATE]|[ENTRY]`

- **Examples**:
  `addlog i/S1234567A l/2023-09-12|First session, discussed progress`


### Listing Session logs: `logs`

Lists all logs of a specific patient.

- **Format**: `logs i/[IDENTITY_NUMBER]`

- **Examples**:
  `logs i/S1234567A`


### Exiting the program: `exit`

Exits the program.

- **Format**: `exit`

### Saving the data

MindMap data is saved in the hard disk automatically after any command that changes the data. There is no need to save manually.

### Editing the data file

MindMap data is saved automatically as a JSON file at `[JAR file location]/data/addressbook.json`. Advanced users are welcome to update data directly by editing the data file.

- **Caution**: If your changes to the data file make its format invalid, MindMap will discard all data and start with an empty data file at the next run. Hence, it is recommended to take a backup of the file before editing it.

### Archiving data files [coming in v2.0]

Details coming soon...

## FAQ

**Q**: How do I transfer my data to another computer?  
**A**: Install the app on the other computer and overwrite the empty data file it creates with the file that contains the data of your previous MindMap home folder.

## Known Issues

- When using multiple screens, if you move the application to a secondary screen and later switch to using only the primary screen, the GUI will open off-screen. The remedy is to delete the `preferences.json` file created by the application before running the application again.
- If you minimize the Help Window and then run the `help` command (or use the Help menu or the keyboard shortcut F1) again, the original Help Window will remain minimized, and no new Help Window will appear. The remedy is to manually restore the minimized Help Window.
- Error not shown when addcommand when Log format is incorrect (e.g., `/l date → no entry`).

## Command summary

| **Action**           | **Format, Examples**                                                                  |
|----------------------|---------------------------------------------------------------------------------------|
| Add                  | `add n/NAME p/PHONE_NUMBER i/IdentityNumber e/EMAIL a/ADDRESS [t/TAG]…​`               |
|                      | e.g. `add n/James p/98765432 e/johnd@example.com a/John street block 123 #01-01`     |
| List                 | `list`                                                                                |
| Edit                 | `edit INDEX [n/NAME] [p/PHONE_NUMBER] [e/EMAIL] [a/ADDRESS] [t/TAG]…​`                 |
|                      | e.g. `edit 1 p/91234567 e/johndoe@example.com`                                       |
| Find                 | `find KEYWORD [MORE_KEYWORDS]`                                                        |
|                      | e.g. `find John`                                                                     |
| Delete               | `delete i/IDENTITY_NUMBER`                                                            |
|                      | e.g. `delete i/S1234567A`                                                            |
| Add Session Log               | `addlog i/IDENTITY_NUMBER l/[DATE]\[ENTRY]`                                                             |
|                      | e.g. `addlog i/S1234567A l/2024-10-10\The session lasted 5 minutes`                                                       |
| List Session Logs    | `logs i/IDENTITY_NUMBER`                                                              
||e.g. `logs i/S1234567A`
| Exit                 | `exit`                                                                                |
|| e.g. `exit`







