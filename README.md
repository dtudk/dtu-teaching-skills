# Teaching skills for use for DTU students

A (hopefully) course agnostic teaching guide that
helps students use AI in a seamless and guided fashion.


## Installation

### Claude

```bash
claude plugin marketplace add dtudk/dtu-teaching-skills
claude plugin install students@dtu-teaching-skills
#claude plugin install teachers@dtu-teaching-skills
```


## Workflows

### Teacher

How a teacher prepares a course repository so the student skills can use it.
Weeks should be condensed in order, since `/dtu-create` reads the
`AI_CONDENSED.md` files of earlier weeks as prior knowledge.

```mermaid
flowchart TD
    A[Create course repository] --> B["Write /README.md<br/>course description and scope"]
    B --> C["Add a WeekXX/ folder per week (01-13)"]
    C --> D["Add material<br/>WeekXX/Lectures/*.pdf<br/>WeekXX/Labs/ exercises"]
    D --> E{"Need to steer<br/>what is read?"}
    E -- yes --> F["Add WeekXX/INDEX.md (AI instruction)<br/>and/or WeekXX/README.md (week context)"]
    E -- no --> G
    F --> G["Install 'teachers' plugin<br/>and run /dtu-create WeekXX"]
    G --> H["Agent proposes: prior-knowledge files,<br/>content files and output file"]
    H --> I{"Teacher accepts<br/>the plan?"}
    I -- no, adjust --> H
    I -- yes --> J["Agent writes WeekXX/AI_CONDENSED.md"]
    J --> K{"Review: learning objectives<br/>correct and in scope?"}
    K -- no --> L["Edit AI_CONDENSED.md by hand<br/>or adjust material / INDEX.md and re-run"]
    L --> K
    K -- yes --> M{"More weeks?"}
    M -- "yes, next week" --> D
    M -- no --> N[Commit and share the repository with students]
```


### Students

How and when a student uses the skills in the `students` plugin during a week.
Each skill reads the course `README.md` and the `WeekXX/AI_CONDENSED.md` files.
Saved assessments (`WeekXX/AI_ASSESSMENT_YY.md`) let the other skills adapt to
what the student already knows.

```mermaid
flowchart TD
    A["Start of a week<br/>(after lectures / reading)"] --> B{"Know where you stand<br/>on this week's objectives?"}
    B -- "no / unsure" --> C["/dtu-assess<br/>7-10 questions, no hints"]
    C --> D["Summary: good / average / lacking objectives<br/>and a suggested learning order"]
    D --> E["Save as WeekXX/AI_ASSESSMENT_YY.md"]
    E --> F
    B -- yes --> F{"What do you<br/>want to do?"}

    F -- "understand a lecture<br/>or concept" --> G["/dtu-discuss<br/>open discussion, one question at a time"]
    F -- "start or continue<br/>a coding exercise" --> H["/dtu-code WeekXX<br/>you make the decisions,<br/>agent writes skeleton code"]
    F -- "get feedback on<br/>code you wrote" --> I["/dtu-review WeekXX<br/>discussion of your code<br/>against the learning objectives"]

    G -- "knowledge gap found" --> G2["Digress to an earlier week<br/>or re-run /dtu-assess"]
    G2 --> F
    G --> J
    H --> I
    I -- "rework the code" --> H
    I --> J{"Comfortable with<br/>this week?"}
    J -- no --> F
    J -- "yes, check yourself" --> C2["/dtu-assess again<br/>(prior results skip mastered objectives)"]
    C2 --> K["Next week"]
    J -- yes --> K
```
