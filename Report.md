# CIS468 Project Report - Auto Tagger Todo-List DB

Zekai Lin
Summer 2025

# 1 Introduction

As the advanced of the NLP, during the learning of the course, NLP may deeply change the way of how people interact with computers. Specifically speeking, as the mature of NLP and related workflow, intead of fill in tables, AI maybe able to understanding the requirement of the user, so that user can achieve their goal, by just talking.The context of the this project is try to disign an potentially more convinient way of human computer interface. This project called `Auto Tagger Todo-List`, it approaches to build up an workflow of:
 
- accepting user's input with an paragraph description of an thing they would like to do.

- Named Entity Recognition (NER) Database Builder
Identify names, places, dates, and organizations in texts or other documents, and transform the information into a
database as an **Todo List** backend

- auto labeling in given tags (classifier)
add labels to corresponding db item while saving to the db with ranges of words(sports, cook, video game, and etc),

- save the feedback from the user and managed to self-implemented

This project should be potentially act as an front end to easily fits popular scheduling apps' interface to improve the efficiency of the human computer interface.

# 2 Workflow Design and C

The initial tager and extractor service is provided by the trained model.

Initial Input: 
    The user will give an initial input of the a thing want to remember [complete]
    The initial input with the current time will be sent to the NER exctractor [complete]

NER Recognition:
    for analysis the actual time and the special Named identities. [complete]
    letting user to check and provided answer, if model made mistakes [todo]

Tag Allocation:
    A list of tag should be saved in the Database and managed by user, easily [todo]
    Allocat the tag for given input ( text, and list of several tags ) [complete]
    Allow user to fix the taging if there are errors [complete]

Log as Data Set for Model Further Training
    The result of each request will be saved for further implement for NLP models [complete]
    Periodically train the NER Recognition & Tag Allocation [todo]


# 3 Results

Generally Speaking, all of the codes functioning correctly, there is no fatal error eccurs. 

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

## 4 Review & Further Improve

    Generally speaking, the urgent part of this project is the project management or self-scheduling. I failed to schedule the workload wisely. Otherwise, further more functionality will be achieved.

    Besides, the trained model is not commonly correct. Further training may improve the correctness of the gise.

    For example, I originally expect the time extration can transfor the time of the day 

    todo: add duration field to the modification the time model, to save duration of the event
    todo: Failed to recognize, and consider all of the time expressions
        {'original_text': 'Meet John at Google HQ tomorrow from 3pm to 5pm for product launch', 'event_time': '2023-10-16 14:30', 'persons': ['Meet John'], 'organizations': [], 'events': [], 'other_nouns': ['product', 'launch']}
    todo: Better logic of the time recognition is required
        {'original_text': 'I need to double check TA with my final before the end of today', 'event_time': None, 'persons': [], 'organizations': [], 'events': [], 'other_nouns': ['end', 'today']}

    Last but not least, if more time is spent in understanding the model, and data structure design.

## 4 Conclusion

    It was a great project enble me to have an general view. But I underestimate my produces and makes me into trouble. But I know really know what my elders and peers is talking about, when they giving a lot AI related words.


## 5 References

