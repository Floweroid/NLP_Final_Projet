# Final Project: Auto Tagger Todo-List DB Version 2

> - Course: CIS 468: Nature Language Process 
> - Semester: Summer 2025
> - Student: Zekai Lin 
> - Date: Aug.9 2025

## Introduction

This project implements an intelligent todo-list system that automatically extracts entities and assigns relevant tags to user tasks using Natural Language Processing (NLP) techniques.

## Features

**Automatic Tagging**: Classifies todos into categories using zero-shot classification

**Entity Recognition**: Extracts persons, organizations, and event times using spaCy NER

**Persistent Storage**: SQLite database for saving todo records

**Time Parsing**: Smart time detection with dateparser library

**Interactive CLI**: User-friendly command-line interface



## Usage

### Checking Online:

[AutoTager (Google Drive Colab) ](https://colab.research.google.com/drive/14PPYnla4JV2Hx4NyXgV3okiu_RSSfx8G?usp=drive_link)


[Project Report](https://docs.google.com/document/d/1lCpltj8ZyvBaGT_qEkmrTGdMkzAHBK8j_JdrDlmmgWQ/edit?usp=sharing)

### Installation 

Copy the file to the colab and run all the code blocks

### Options:
1. Add new todo item: Describe your task and the system will automatically analyze and tag it
2. View history: Browse previously saved todo items with their metadata
3. Exit system: Close the application

### Sample Output:

## Sample Comversation

``` shell
Mounted at /content/drive/
Loaded model: en_core_web_lg

=== Auto-Tagging Todo System ===
1. Add new todo item
2. View history
3. Exit system
Please select an option: 1

=== 2025-08-08 23:06:48 EDT-0400 ===


--- Step 1: Enter Todo Description ---
Please describe what you plan to do: I plan to go play with my younger brother Bob

=== 2025-08-08 23:07:30 EDT-0400 ===


--- Step 2: Confirm Description ---
Your input: I plan to go play with my younger brother Bob
Is this description correct? (y/n): y

=== 2025-08-08 23:07:34 EDT-0400 ===


--- Step 3: Auto Analysis ---
Device set to use cpu

--- Named Entity Recognition Results ---
Event Time: Not detected
Persons: Bob

--- Tag Classification Results ---
Supported tags: sports, cooking, gaming, work, study, shopping
Predicted tags: sports, gaming

--- Step 4: Confirm Results ---
Are the results correct? (y-correct/n-revise/c-cancel): y

=== 2025-08-08 23:08:07 EDT-0400 ===


--- Processing Complete ---
Todo item saved successfully! Record ID: 1
Content: I plan to go play with my younger brother Bob
Time: 2025-08-08 23:08:07 EDT-0400
Tags: sports, gaming

=== 2025-08-08 23:08:07 EDT-0400 ===


=== Auto-Tagging Todo System ===
1. Add new todo item
2. View history
3. Exit system
Please select an option: 2

=== 2025-08-08 23:08:10 EDT-0400 ===


Found 1 historical records:

ID: 1
Creation Time: 2025-08-08 23:08:07 EDT-0400
Content: I plan to go play with my younger brother Bob
Predicted Tags: sports, gaming
Persons: Bob

=== 2025-08-08 23:08:10 EDT-0400 ===


=== Auto-Tagging Todo System ===
1. Add new todo item
2. View history
3. Exit system
Please select an option: 3

=== 2025-08-08 23:09:03 EDT-0400 ===

Thank you for using our system. Goodbye!
```


## Workflow Overview
**User Input:** Describe your todo item

**Entity Extraction:**
Detect persons, organizations, and time references
Parse relative time expressions (e.g., "tomorrow at 3pm")

**Tag Classification:**
Assign relevant tags from predefined categories
Uses zero-shot classification with BART-large model

**Storage:** The final result will been saved to SQLite database of the Google Drive

**History View:**Retrieve and review past todo items

## Data Structure
Todo records contain:

- Original text description
- Creation timestamp
- Predicted tags (e.g., sports, work, study)
- NER results:
    - Event time
    - Persons
    - Organizations
    - Events
    - Sample Output

```json
{
  "original_text": "Meet John at Google HQ tomorrow at 3pm for product launch",
  "creation_time": "2023-08-15 14:30:45 EDT-0400",
  "candidate_labels": [
    "sports",
    "cooking",
    "gaming",
    "work",
    "study",
    "shopping"
  ],
  "predicted_tags": [
    "work"
  ],
  "ner_results": {
    "event_time": "2023-08-16 15:00",
    "persons": [
      "John"
    ]
  }
}
```

## System Components

**Database Manager** (DatabaseManager):

Initialize an sqliteDB file in given google drive path, Handle SQLite database operations
Stores todo records with original text, tags, and entities

**NER Extractor (EnhancedNERExtractor):**

Extracts named entities using spaCy
Processes time expressions with dateparser
Identifies persons, organizations, and events

**Event Tagger (EventTagger):**

Classifies text using zero-shot learning
Supports multi-label tagging
Configurable confidence threshold

**Commend line UI (TodoApp):**

Commandline User Interface accepting Keyboard Input & give feedback

## Dependencies
    spaCy (with en_core_web_lg model)
    Transformers (Hugging Face)
    dateparser
    SQLite3

    pytz














