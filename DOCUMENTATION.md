```py
# Code Documentation

## Overview
This project is a Python console-based application that simulates an open source software project. It manages contributors, tracks issues, performs data analysis, and generates output files such as reports and CSV files.

---

# -------------------------------
# Contributor Management
# -------------------------------

contributors = []

for i in range(4):
    name = input("Enter contributor name: ")
    role = input("Enter role: ")
    language = input("Enter programming language: ")
    commits = int(input("Enter number of commits: "))
    country = input("Enter country: ")

    contributor = {
        "name": name,
        "role": role,
        "language": language,
        "commits": commits,
        "country": country
    }

    contributors.append(contributor)

# This section collects contributor data from the user and stores each contributor
# as a dictionary inside a list. It tracks name, role, programming language,
# number of commits, and country.


# -------------------------------
# Issue Tracking System
# -------------------------------

issues = []
issue_ids = set()

for i in range(5):
    issue_id = input("Enter issue ID: ")

    while issue_id in issue_ids:
        issue_id = input("Duplicate ID! Enter a new issue ID: ")

    issue_ids.add(issue_id)

    issue = {
        "id": issue_id,
        "type": input("Enter type (Bug/Feature): "),
        "priority": input("Enter priority: "),
        "status": input("Enter status: "),
        "reporter": input("Enter reporter name: ")
    }

    issues.append(issue)

# This section manages issues using a list and ensures unique issue IDs using a set.
# Each issue contains type, priority, status, and reporter information.


# -------------------------------
# Priority Analysis
# -------------------------------

priority_count = {}

for issue in issues:
    priority = issue["priority"]
    priority_count[priority] = priority_count.get(priority, 0) + 1

# This part counts the number of issues for each priority level using a dictionary.


# -------------------------------
# Grouping Issues by Status
# -------------------------------

status_group = {}

for issue in issues:
    status = issue["status"]
    if status not in status_group:
        status_group[status] = []
    status_group[status].append(issue)

# This groups issues based on their status such as Open, In Progress, or Resolved.


# -------------------------------
# Set Operations
# -------------------------------

reporters = set(issue["reporter"] for issue in issues)
contributors_names = set(c["name"] for c in contributors)

common_users = reporters.intersection(contributors_names)

# This compares contributors and reporters using sets to identify users who both
# contribute and report issues.


# -------------------------------
# File Handling
# -------------------------------

import os

folder = "open_track"
os.makedirs(folder, exist_ok=True)

with open(f"{folder}/project_report.txt", "w") as file:
    file.write("Project Report\n")
    file.write(str(contributors))

# This creates a folder and writes contributor data into a text file.


# -------------------------------
# CSV Export
# -------------------------------

with open(f"{folder}/issues.csv", "w") as file:
    file.write("ID,Type,Priority,Status,Reporter\n")
    for issue in issues:
        file.write(f"{issue['id']},{issue['type']},{issue['priority']},{issue['status']},{issue['reporter']}\n")

# This exports issue data into a CSV file format.


# -------------------------------
# Urgent Issue Detection
# -------------------------------

urgent = [i for i in issues if i["priority"] in ["Critical", "High"]]

# This identifies urgent issues based on priority level using list comprehension.
