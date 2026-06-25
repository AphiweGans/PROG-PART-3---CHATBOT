# PROG-PART-3---CHATBOT

## Introduction

The proliferation of cybercrime, including phishing, ransomware, and identity theft, has increased the need for accessible tools that promote cybersecurity literacy among non-technical users. This project addresses that need through the design and implementation of a conversational software agent — referred to throughout this document as "the chatbot" — capable of engaging users in cybersecurity education through natural dialogue, task management, and gamified assessment.

The chatbot was developed across three incremental parts. Part 1 established baseline conversational capabilities, including keyword recognition and predefined response generation. Part 2 extended this functionality with sentiment detection and a memory and recall mechanism, allowing the system to personalise interactions based on previously disclosed user information. Part 3, documented in this report, introduces four further modules that increase the system's practical utility and interactivity.

In accordance with the assessment brief, the application is implemented exclusively as a graphical user interface using C# and the WPF framework. No console-based interaction is provided, as the specification stipulates that a console submission for this part of the assessment receives a mark of zero.

##  System Requirements and Prerequisites

The following software components are required to build and execute the application:


Visual Studio 2022 or later, configured with the .NET Desktop Development workload
.NET 6 (or a later compatible runtime)
A local or remote instance of MySQL Server
The MySql.Data NuGet package, referenced within the project

## Module 1: Task Assistant with Reminders

3.1 Purpose

The task assistant module enables users to create, monitor, and manage cybersecurity-related tasks (for example, "Enable two-factor authentication") within the conversational interface. All task records are persisted in a relational database to ensure continuity between sessions.

3.2 Functional Description

Users initiate task creation through natural-language commands such as:


Add task - Review privacy settings
New task - Update my passwords


Upon receipt of such a command, the chatbot confirms the action, prompts the user to specify an optional reminder, and commits the resulting record to the tasks table. Subsequent commands permit the user to retrieve, complete, or delete existing tasks, with each operation reflected immediately in the underlying database.

## Database Schema

sqlCREATE TABLE tasks (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    description TEXT,
    reminder_date DATE,
    reminder_timeframe VARCHAR(100),
    is_completed BOOLEAN DEFAULT FALSE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

3.4 Illustrative Interaction

User:    Add task - Review privacy settings
Chatbot: Task added with the description "Review account privacy settings to
         ensure your data is protected." Would you like a reminder?
User:    Yes, remind me in 3 days.
Chatbot: Got it! I'll remind you in 3 days.

3.5 Supported Commands

CommandResulting ActionAdd task - [title]Creates a new task recordShow tasks / View my tasksRetrieves and displays all stored tasks, including title, description, reminder, and completion statusMark task [title] as completeUpdates the corresponding record's completion statusDelete task [title]Removes the corresponding record from the database

3.6 Interface Elements

The task assistant is presented as a dedicated panel within the main application window, comprising a styled list of task records and three control buttons — Add Task, Mark Complete, and Delete Task — styled consistently with the application's visual theme.

## Cybersecurity Knowledge Assessment (Quiz)

4.1 Purpose

This module reinforces the user's cybersecurity literacy through an interactive, scored assessment, providing immediate corrective feedback for each response.

4.2 Functional Description

A bank of more than ten questions is maintained in-memory as a List<QuizQuestion> object; no database persistence is required for this module. Questions are presented individually, in either multiple-choice or true/false format, and span the following subject areas:


Phishing
Password security
Safe browsing practices
Social engineering
Two-factor authentication
Ransomware


Following each response, the system indicates whether the answer was correct and provides a concise explanatory note reinforcing the underlying concept. Upon completion of the assessment, a cumulative score is presented alongside a corresponding evaluative message.

4.3 Illustrative Question

Question: What should you do if you receive an email asking for your password?
A) Reply with your password
B) Delete the email
C) Report the email as phishing
D) Ignore it

Chatbot: Correct! Reporting phishing emails helps prevent scams.

4.4 Scoring Criteria

Score RangeFeedback Message10–12 correct"Great job! You're a cybersecurity pro!"6–9 correct"Good effort! Keep practising to stay safe online."0–5 correct"Keep learning to stay safe online!"

## Initiating the Assessment

The quiz may be initiated through any of the following user inputs: Start quiz, Play quiz, Quiz me, Test my knowledge.

4.6 Interface Elements

The assessment is rendered within a dedicated panel or child window, displaying the question number, question text, response controls, a running score, and progress indication. Correct and incorrect responses are differentiated through colour-coded feedback. Upon completion, a summary screen displays the final score together with an option to restart the assessment.
