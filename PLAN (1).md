# TripSync – Project Plan & Brainstorm

This is our starting point for the project. Nothing here is final, it's just so we all have the same idea of what we're building and what order to do it in. If you think something should change, bring it up in the group chat or edit this file and let everyone know.

> **Legend:**
> ✅ = done  |  ⬜ = still to do  |  ❓ = something we need to figure out / ask the prof

---

## 1. What we're building (quick recap)

A system where a group of friends can:
- Create a trip and invite each other to it
- Add accommodations, transportation, and activities
- See a day-by-day itinerary of the whole trip
- Record expenses and who paid for them
- Split expenses equally or with custom amounts
- See who owes who and record paybacks
- Search activities and see how much was spent by category
- Ask an AI questions about the trip in plain English (e.g. *"How much do I still owe everyone from the Portugal trip?"*)

---

## 2. Things we need to figure out first ❓

We shouldn't write any code until we know these:

- ❓ **Which database do we have to use?** (MySQL, PostgreSQL, SQLite, Oracle…?) Ask the prof or check the course outline.
- ❓ **Which programming language?** (Python, Java, JavaScript…?) Same thing, check if it's required or our choice.
- ❓ **Does it need a user interface?** Could be a website, a desktop app, or just a command-line menu. A command-line menu is the simplest if they don't care.
- ❓ **How is the AI part supposed to work?** Are we allowed to use an API like Claude or ChatGPT? Is there a budget or does the course give us keys?
- ❓ **What's due for each assignment?** Make a list of deadlines so we know what each assignment actually needs from us (see Section 8).

---

## 3. The plan in steps

### Step 1 – Requirements & ER Model (Assignment 1)
- ✅ Write the requirement specifications document
- ✅ Define entity types and attributes
- ✅ Define relationship types (degree, multiplicity, attributes)
- ⬜ Draw the ER diagram in UML notation (the notation from Unit 3)
  - Tools we could use: draw.io (free), Lucidchart, or dbdiagram.io
  - Remember: `{PK}` for primary keys, `/` for derived attributes, `[0..*]` for multi-valued, dashed line for relationship attributes, a diamond for the ternary **Books** relationship
- ⬜ Save the final diagram as a PNG/PDF in `docs/`

### Step 2 – Turn the ER model into tables (relational schema)
This is where the ER diagram becomes actual tables. Rough idea of what we'll have:

| Table | What it comes from | Notes |
|---|---|---|
| `User` | User entity | `phoneNumber` is multi-valued, so it probably needs its own table (`UserPhone`) |
| `Trip` | Trip entity | `/duration` and `/totalCost` are derived, so we **don't store them**, we calculate them in queries |
| `TripMember` | ParticipatesIn relationship (*:*) | Holds `userID`, `tripID`, `role`, `joinDate` |
| `Accommodation` | Accommodation entity | Has `tripID` as a foreign key |
| `Activity` | Activity entity | Has `tripID` as a foreign key |
| `Transportation` | Transportation entity + Books relationship | Needs `tripID` and `bookedBy` (userID), plus `bookingDate`, `confirmationNumber`. ❓ Double-check how the prof wants ternary relationships mapped |
| `Expense` | Expense entity | Has `tripID` and `paidBy` (userID) as foreign keys |
| `ExpenseParticipant` | SharesIn relationship (*:*) | Holds `expenseID`, `userID`, `shareAmount` |
| `Payment` | Payment entity | Has `payerID`, `recipientID`, and `tripID` as foreign keys |

- ⬜ Write out every table with its columns, data types, primary keys, and foreign keys
- ⬜ Check the tables for normalization (probably covered later in the course)
- ⬜ Decide on rules like: what happens to a trip's expenses if the trip is deleted? (`ON DELETE CASCADE`?)

### Step 3 – Create the database
- ⬜ Install whatever database we end up using
- ⬜ Write a script that creates all the tables (`schema` file)
- ⬜ Write a script that fills the tables with fake test data (`sample data` file)
  - Idea: make a fake "Portugal trip" with all 5 of us, a few hotels, flights, activities, and expenses. That way we can test everything with the same example the assignment uses.

### Step 4 – Write the queries (the main features)
Each feature from our functional specs becomes one or more queries. Order is roughly easiest → hardest:

| Feature | What the query needs to do | Difficulty |
|---|---|---|
| Create trip / invite members | `INSERT` into `Trip` and `TripMember` | Easy |
| Add bookings | `INSERT` into `Accommodation`, `Transportation`, `Activity` | Easy |
| Record an expense | `INSERT` into `Expense`, then one row per person in `ExpenseParticipant` | Easy |
| Search activities | `SELECT` with `WHERE` on date or location | Easy |
| Total trip cost | `SUM` of expenses for one trip | Easy |
| Spending by category | `SUM` + `GROUP BY category` | Medium |
| Itinerary | Combine accommodations, transportation, and activities into one list sorted by date/time (probably `UNION`) | Medium |
| Equal split | Divide the amount by the number of people, then insert each share | Medium |
| Record a repayment | `INSERT` into `Payment` | Easy |
| **Who owes who** | See the formula below | **Hard** |

**How we could calculate balances (brainstorm):**

For each person on a trip:
```
balance = (what they paid for expenses)
        − (their shares of expenses)
        + (payments they sent)
        − (payments they received)
```
- Positive balance → the group owes them money
- Negative balance → they owe money
- Zero → they're settled up

Example: I pay $100 for dinner split between 4 people. My balance = 100 − 25 = **+75**. Everyone else = 0 − 25 = **−25**. If Romy pays me back $25, her balance goes to **0** and mine goes to **+50**.

- ⬜ Test this formula with our sample data by hand first before writing it as a query
- ❓ Do we just show each person's overall balance, or do we need "Panos owes Rebecca $X" for each pair? The pair version is harder, so start with overall balance

### Step 5 – The program / interface
- ⬜ Once we know the language, connect it to the database
- ⬜ Build a simple menu (e.g. "1. Create trip, 2. Add expense, 3. View balances…")
- ⬜ Each menu option runs one of the queries from Step 4

### Step 6 – AI feature
Basic idea of how it could work:
1. User types a question like *"What are we doing on August 27?"*
2. We send the question + a description of our tables to an AI
3. The AI writes a SQL query
4. We run the query and show the answer (or send the results back to the AI so it can answer in a normal sentence)

- ⬜ Figure out which AI API we can use ❓
- ⬜ Write a description of our database for the AI (table names, columns, what they mean)
- ⬜ **Safety:** only let the AI run `SELECT` queries, so it can't delete or change our data
- ⬜ Test it with the three example questions from the project outline

### Step 7 – Testing & final report
- ⬜ Test every feature with the sample data
- ⬜ Screenshots of everything working
- ⬜ Final write-up / presentation (whatever the prof asks for)

---

## 4. Possible folder structure (once we start coding)

```
tripsync/
├── README.md
├── docs/            → plan, assignment docs, ER diagram
├── database/        → schema (create tables) + sample data scripts
├── queries/         → SQL for each feature
└── src/             → program code (language TBD)
```
We don't need to make all of these folders now, just add them as we get there.

---

## 5. Who does what (draft)

We can switch this around, but roughly we can split it by area so no one is stuck on the same thing:

| Area | People |
|---|---|
| ER diagram + relational schema | ⬜ |
| Database setup + sample data | ⬜ |
| Queries (trip + booking features) | ⬜ |
| Queries (expense + balance features) | ⬜ |
| AI feature | ⬜ |
| Testing + report | Everyone |

---

## 6. How we'll use GitHub (keep it simple)

- Always **pull** before you start working: `git pull`
- Write clear commit messages, like `"Add Expense table to schema"`, not `"stuff"`
- Don't push anything with passwords or API keys in it ❗
- If two people are editing the same file, tell the group chat first so we don't overwrite each other's work

---

## 7. Open questions list (add to this!)

- ❓ Which DBMS and language are required?
- ❓ Is a UI required or is command-line okay?
- ❓ How does the prof want ternary relationships (Books) mapped to tables?
- ❓ Do balances need to be per-pair ("who owes who") or just per-person?
- ❓ Can we use a paid AI API or is there a free option?
- ❓ Do we need to support different currencies? (We're saying **no** for now to keep it simple)

---

## 8. Deadlines

| Assignment | What's due | Date |
|---|---|---|
| Assignment 1 | Requirement specifications document | ⬜ |
| Assignment 2 | ⬜ | ⬜ |
| Assignment 3 | ⬜ | ⬜ |
| Final project | ⬜ | ⬜ |
