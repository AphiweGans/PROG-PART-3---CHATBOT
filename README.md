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
