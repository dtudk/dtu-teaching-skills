---
name: dtu-create
version: 1.0.0
description: Create a condensed topic overview of the lecture and other notes. Additionally creates specific learning objectives.
arguments: directory
allowed-tools: Bash(pdftotext *) Bash(pdfinfo *) Bash(cat *) Read Grep
---

Stop this skill if no arguments has been passed.


# Create condensed learning objectives with well explained details

The scope is to create a markdown file to be read and understood by a future AI agent
for understanding learning context.

You are allowed to read content from the root of the git repo.


## Instructions

Act as a teacher that reads content and condenses the content into a
brief markdown file with clear sections.

The course spans multiple lectures. The full course is described in @/README.md.
You may understand the full context by reading that.

The output should be focused on learning objectives and what the content
contains of fundamental knowledge.
You should **only** output content from files in the current $directory directory.

The default content may be found in the $directory/Lectures/ subfolder, and if not present
search for pdfs directly in the $directory folder (no subfolder search).
The teaching material includes a $directory/Labs/ folder which contains exercises which should
be used to understand the context of learning objectives, they are not necessarily
concept correct!
If there is an INDEX.md file, read this to know which files you should read.

The output should reflect the material, with no additional scope added
to the understanding.

Keep references to the course material such that the AI can refer directly to course
material.

The sections of the output markdown file:

1. Overview -- brief

  Mandatory.

  The overview scope of the current content, learning objectives and concepts.

2. Prerequisites -- as needed

  Optional.

  List the prerequisites to understand the learning objectives laid out that follows.

3. Detailed learning objectives and concepts that the student should know/learn.
  This could be a longer explanation, or 1-line descriptions.
  Ensure the content has enough description for another AI agent to parse and
  understand the learning objectives.


---

### Step 1: Determine the input/output files

Figure out which files you should restrict to be reading and understanding.

Also ask for the output file. This will by default be `/WeekXX/AI_CONDENSED.md`.
It is optional.

If the current folder equals `WeekXX` (with `XX` being a number in the range
of 1-13), then add
- `/WeekXX/README.md` if it exists, it adds context to this week.
- `/WeekXX/INDEX.md` if it exists, it tells which files it should read or omit.
- `/WeekXX/AI_CONDENSED.md`, only for lower `XX` values, files to the read in files.
  These contain prior weeks knowledge.
  They do not provide the content for the current weeks learning objectives
  but should be considered prior knowledge. Overlapping concepts should be
  cross-referenced.


---

### Step 2: Show what will be done

Before executing anything, describe what you will do.
Be brief.

1. Which files will you read that is the prerequisite student knowledge.
  The content can *still* be learning objectives in the content to condense.
  Determine what is still a learning objective and what should be understood
  as prior knowledge.
2. Which files you will read to create the condensed markdown file.
  The content of the output markdown file should focus on these files.
3. Which file will you write the output to.

Don't continue before the user has accepted.

---

### Step 3: Parse and create file

- Read the prerequisite files. Store these as prior knowledge.
- Then read the content files.
- Condense the content, and write it to the output file.

