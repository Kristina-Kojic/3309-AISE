# TripSync Plan

## What we're building

An app for friends travelling together. It lets the group:

- make a trip and invite each other
- add hotels, flights, trains, and activities
- see a day-by-day schedule of the trip
- track who paid for what and split costs
- see who owes who, and record paybacks
- see how much the trip cost, and on what
- ask an AI questions like "How much do I still owe everyone from the Portugal trip?"

## How to use this file

Each step has a short list of tasks. Your name is at the start of each task.
When you finish one, change `[ ]` to `[x]` and push.
The dates are our own goals. We'll change them once we know the real due dates.

---

## Step 1: Get set up (by Oct 2)

Why: we need to know what tools we're using before we build anything.

- [ ] Kristina: make the GitHub repo and invite everyone (Sep 30)
- [ ] Everyone: add your GitHub username to the README and push it, to check git works (Oct 1)
- [ ] Anyone: ask the prof which database and language to use, whether we need a real UI, and what AI we can use (Oct 3)
- [ ] Anyone: write the real due dates at the bottom of this file (Oct 2)
- [ ] Everyone: pick our tools based on the prof's answers (Oct 2)

---

## Step 2: Draw the ER diagram (by Oct 9)

Why: the diagram is our blueprint. It's much easier to fix a drawing than a finished database.

- [ ] Everyone: submit Assignment 1 (add Panos and Abhay's IDs first)
- [ ] Romy: draw the 7 entities and their attributes in draw.io (Oct 6)
- [ ] Panos: draw the 10 relationships with their multiplicities (Oct 7)
- [ ] Everyone: check the diagram matches our Assignment 1 doc (Oct 8)
- [ ] Romy: save the diagram in the repo (Oct 9)

---

## Step 3: Plan the tables (by Oct 16)

Why: a database stores tables, so we turn the diagram into a list of tables before writing any code.

- [ ] Panos: list every table and its columns (Oct 13)
- [ ] Romy: pick a data type for every column, e.g. money, date, text (Oct 14)
- [ ] Panos: write the rules, e.g. "an amount can't be negative" (Oct 15)
- [ ] Everyone: agree on the final tables (Oct 16)

---

## Step 4: Build the database (by Oct 23)

Why: we need fake data to test with, and the right answers to compare against.

- [ ] Romy: write the code that creates all the tables (Oct 19)
- [ ] Kristina: add a fake "Portugal 2026" trip with all 5 of us, plus hotels, flights, activities, expenses, and paybacks (Oct 21)
- [ ] Rebecca: work out by hand what each person owes and what the trip cost. This is our answer key (Oct 23)

---

## Step 5: Write the features (by Nov 6)

Why: this is the main part of the project. Each feature is a database query.
Start with the easy ones and save balances for last.

- [ ] Kristina: create a trip and add people to it (Oct 27)
- [ ] Kristina: add hotels, transport, and activities to a trip (Oct 28)
- [ ] Abhay: search activities by date or by city (Oct 28)
- [ ] Panos: add an expense and split it equally or by custom amounts (Oct 30)
- [ ] Panos: record a payback between two people (Oct 30)
- [ ] Abhay: total trip cost and spending per category (Oct 31)
- [ ] Romy: the day-by-day trip schedule (Nov 3)
- [ ] Rebecca: how much each person owes or is owed (Nov 5)
- [ ] Everyone: check every feature against the answer key (Nov 6)

---

## Step 6: Build the program (by Nov 16)

Why: users can't type database code, so we make a simple menu that runs the features for them.
Each person builds the menu options for the features they wrote in Step 5.

- [ ] Rebecca: connect the program to the database, and make the main menu (Nov 10)
- [ ] Kristina: trips and bookings options (Nov 13)
- [ ] Romy: trip schedule option (Nov 13)
- [ ] Panos: expenses and paybacks options (Nov 14)
- [ ] Rebecca: balances option (Nov 15)
- [ ] Abhay: cost report and search options (Nov 15)

---

## Step 7: Add the AI (by Nov 23)

Why: it uses everything else, so it goes last.

- [ ] Abhay: set up the AI and keep the key off GitHub (Nov 17)
- [ ] Abhay and Romy: write a plain-English description of our tables for the AI (Nov 18)
- [ ] Abhay: make the AI turn a question into a query and show the answer. It should only be able to read data, never change it (Nov 21)
- [ ] Abhay: test the 3 example questions from the project outline (Nov 23)

---

## Step 8: Finish up (by Nov 30)

Why: if we can't show it working, it doesn't count.

- [ ] Rebecca: write "how to run it" in the README (Nov 25)
- [ ] Kristina: try running it on a fresh laptop using only the README (Nov 26)
- [ ] Everyone: screenshot the features you built (Nov 27)
- [ ] Everyone: final report or demo (Nov 30)

---

## Who's doing what

- Rebecca: repo, answer key, balances, database connection, main menu, README
- Kristina: questions for prof, fake data, trips and bookings, fresh laptop test
- Romy: ER diagram entities, data types, creating the tables, trip schedule
- Panos: ER diagram relationships, table list and rules, expenses and paybacks
- Abhay: search, cost reports, the AI

---

## Real due dates

- Assignment 1:
- Assignment 2:
- Assignment 3:
- Final project:

---

More detail on any step is in ROADMAP.md.
