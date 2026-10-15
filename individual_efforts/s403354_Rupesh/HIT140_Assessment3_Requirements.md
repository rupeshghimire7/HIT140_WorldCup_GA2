# HIT140 Assessment 3 — What it is and how it is marked

Source: the Assessment 3 page, the Project Brief, the grading rubric and the lecturer's replies on the question board (all from your screenshots and files). A few screenshots were cut off, so check the places marked **(check)** on Learnline.

---

## 1. The basics

| | |
|---|---|
| Unit | HIT140 Foundations of Data Science |
| Assessment | Assessment 3: Group Project Report |
| Weight | 50% of the unit |
| Due | **15 October 2026, 14:00 ACST (Darwin time)**. That is **15:30 in Sydney**. |
| Group | 4 students, the same group as Assessment 2. No individual submissions. |
| Scope | **Objective 2 only.** Objective 1 was assessed in Assessment 2 and is not part of the report. |
| Tools | All analysis and charts must be done in **Python**. Excel is allowed only for preparing raw datasets. Data wrangling and all other analysis must be in Python. |

---

## 2. The project brief

The topic is **FIFA World Cup 2026**. The matches have just ended, and there is team-level and player-level data on three websites:

- FIFA official website (World Cup 2026 statistics)
- The Stats Don't Lie (World Cup 2026 page)
- FBref

**Using other websites:** allowed, but only if you can justify that the three recommended sites cannot give you the crucial information you need. For pre-tournament information the lecturer said looking beyond the three sites is a reasonable approach. The lecturer also agreed that Transfermarkt (squad market values) makes sense in this case.

---

## 3. Objective 2: the two linear regression tasks

Your team does **two related but different** linear regression tasks.

### Linear Regression 2.1: goal difference

- Predict the **goal difference between the two teams** in a World Cup 2026 match.
- Dataset: **104 rows**, one per actual match.
- **Exactly 8 explanatory variables** (not counting any ID column).
- You decide what the variables are and collect the data.

### Linear Regression 2.2: goals scored by a team

- Predict the **number of goals scored by one team** in one match.
- Dataset: **208 rows**, one per team per match (two rows per match).
- **Exactly 8 explanatory variables** (not counting any ID column).
- You decide what the variables are and collect the data.

### Rules for both

1. **Every explanatory variable must be known before the match.** Example: shots on target in the match cannot be used to predict that match's result.
2. **At most 4 explanatory variables can be shared** between 2.1 and 2.2.
   - Lecturer's example: 2.1 can have 4 unique variables plus 4 shared. 2.2 can have 4 unique variables plus the same 4 shared. That gives **12 unique variables** in total.
   - A challenge for strong students is to come up with **16 unique variables** across the two models.
3. Both are **multiple** linear regression models, because each has 8 explanatory variables. Each model has **one response variable** (the thing being predicted).
4. Whether the *same underlying statistic* used in different forms (for example a difference in 2.1 and a raw value in 2.2) counts as "shared" was asked by a student. **(check)** The lecturer's full reply was cut off in the screenshot.

### Lecturer's clarifications (from the question board)

**Choosing variables and EDA**
- First nominate candidate variables using logic and common sense. Then run EDA (for example scatter plots or Pearson correlation) to check whether each variable really relates to the response.
- Running EDA takes extra effort and critical thinking, so it is **required for Credit or above**.

**Training and testing**
- Comparing predicted values with the **true FIFA 2026 values** to evaluate the model is correct.

**First-match missing values**
- Teams with no earlier match have no history. The lecturer's view: carefully choosing pre-tournament statistics gives more insight than imputing, because imputation can reinforce existing patterns in the data and add bias.

**Competing algorithms (High Distinction)**
- Linear regression is only one of many regression models. Others (non-linear, ensemble) are available in **scikit-learn**.
- First build the linear regression as taught in class, **then compare** it with other regression types. This needs extra independent research, which is why it is an HD requirement.

---

## 4. What to submit

Submit **one .zip file** on Learnline containing four things:

| # | Item | Details |
|---|---|---|
| 1 | **Group report** | One Word file (.docx). **Maximum 4 pages**, A4, single-spaced, **10 pt font**, including the title and names with student IDs. No table of contents, list of figures or reference list (they earn no marks). No minimum length. |
| 2 | **Code link** | A **.txt** file with one URL to a OneDrive / GitHub / BitBucket repository holding **all Python files and the dataset** used. |
| 3 | **Turnitin originality report** | A copy of the report from the provided Turnitin link. |
| 4 | **AI Usage Declaration Form** | The signed form (template: *AI Usage Declaration Form v2.docx*), signed by **all** team members. |

Other points:
- Email submissions are not accepted.
- Do not submit multiple documents. One submission per team.
- **Optional:** extra supporting material that helps address the rubric.
- **Late penalty:** CDU late policy applies. Separately, a missing or incomplete AI form costs **5% of the total assessment mark for each calendar day late**, and makes the submission incomplete.

### What the report should contain (lecturer's guidance)

- There is **no required format**, but at least an opening **Introduction** and a **Conclusion** are recommended. Everything in between is up to you, as long as it gives the details needed to mark it against the rubric.
- Most important: **explain why and how you chose your explanatory variables**, and explain the **linear regression results**.
- **Python code does not go in the report.** It goes in the repository.
- The 4-page limit is **per group**, not per member.

---

## 5. Marking criteria (rubric)

| Criterion | Weight |
|---|---|
| Linear Regression 2.1 | **35%** |
| Linear Regression 2.2 | **40%** |
| Original Reporting Quality | **10%** |
| Collaboration and Documentation | **15%** |
| **Total** | **100%** |

### Linear Regression 2.1 and 2.2 (same wording for both)

| Grade | Mark range | What is needed |
|---|---|---|
| **High Distinction** | 85–100% | Everything in Distinction, **plus** creativity, flair, exceptional originality and scientific rigour. **Competing algorithms are systematically evaluated and compared, followed by recommendations.** Excellent, creative and original data visualisations that support effective data storytelling. |
| **Distinction** | 75–84% | Everything in Credit, **plus** a systematic modelling approach supported by **extensive experiments**. The optimisation of the model is effective and gives an **appreciable improvement** in performance. Strong evidence of mastery of **all descriptive, inferential and EDA techniques** taught in the unit. EDA is systematic, used well and improves the model. Visualisations are systematic, well justified and support the EDA and the modelling. |
| **Credit** | 65–74% | Everything in Pass, **plus** in-depth analysis of model and feature performance. Appreciable attempts to optimise the model through **feature engineering and/or data transformation**. EDA is comprehensive, relevant, informative and useful, showing a broad range of EDA skills from the unit. Professional-quality visualisations that are accurate and precise, with no errors. |
| **Pass** | 50–64% | Precisely addresses the modelling task. The dataset is relevant and meets the requirements. The choice of linear regression technique is appropriate. **Basic cross-validation** is applied. Some errors may be present. Correct but basic interpretation of results. EDA is attempted. |
| **Fail** | 0–49% | No results, or results that do not address the objective, or are irrelevant, incomplete, illogical, incorrect or incoherent. |

### Original Reporting Quality (10%)

| Grade | Mark range | What is needed |
|---|---|---|
| **High Distinction** | 85–100% | Effectively communicates the practical and scientific rigour of the work, including its method. Shows intimate knowledge of the domain, a solid technical grasp and critical thinking. |
| **Distinction** | 75–84% | Thoughtful report with an exceptional grasp of the problem and strong interpretive skills. |
| **Credit** | 65–74% | Excellent technical style without too much jargon. Results are relevant, correct and fairly comprehensive. Discussion shows a good grasp of the problem and good interpretation. |
| **Pass** | 50–64% | Appropriate basic report structure. Conclusions are clearly tied to the modelling and analysis and address the main objective. Results and discussion are generally relevant but feel lacking. |
| **Fail** | 0–49% | Illogical or incoherent writing, hard to follow, full of spelling or grammar errors, unfit for a professional setting. |

### Collaboration and Documentation (15%)

Only the top two levels were visible in the screenshot. **(check the lower levels on Learnline)**

| Grade | Mark range | What is needed |
|---|---|---|
| **High Distinction** | 85–100% | Proactively uses advanced features of teamwork platforms (for example GitHub, Trello, Monday) to improve task organisation, collaboration and communication. Updates documentation consistently and early, builds a culture of open communication in the team channel, and answers questions and concerns quickly. Uses clear, concise language so everyone knows progress, decisions and next steps. Keeps thorough, well-organised documentation of **all updates, decisions, progress checks, work reviews and individual contributions**. |
| **Distinction** | 75–84% | Open communication in the team channel and prompt answers to questions. Uses teamwork platforms (GitHub, Trello, Monday, etc.) effectively to improve task organisation and collaboration, and may explore more advanced features. Documents all updates, decisions, progress checks, work reviews and individual contributions in a clear, organised and easy-to-access way. |

---

## 6. Teamwork and individual marks

- Every member must do a fair share of the work, and every student must **clearly document their own contributions**.
- Failure to show satisfactory evidence of your contribution can mean **lost marks or not passing** the assessment.
- **Document the creative process only on the Microsoft Teams space set up by your campus lecturers.** Other platforms (WhatsApp, Facebook, Discord and so on) do not count as evidence unless the lecturers agreed in advance.
- Your activity on Teams is monitored and can be used to **adjust individual marks**. The lecturer can give different grades to different members.
- The group mark may be **withheld** if this requirement is not met by the due date.
- If unsure, ask your campus lecturer.

---

## 7. Originality, AI use and academic integrity

- Do not copy from other groups. Do not use contract cheating (providing it is a criminal offence in Australia).
- **Generative AI (Claude, ChatGPT, Gemini, DeepSeek and others) may be used** to brainstorm or to help with Python code, **but you must be able to show that you understand every part of your code and what it does.**
- **The report must be in your own words.** AI may only be used to **suggest an outline** or for **final proofreading**.
- All AI use must be **clearly acknowledged** in the signed AI Usage Declaration Form. The form needs:
  - a clear acknowledgement of generative AI use, and
  - a short reflection on how AI was used, with a **link to the AI conversation history** where applicable.
- Breaking the originality rules is a serious breach of academic integrity and can mean major loss of marks or **not passing the unit**.
- Related policies: CDU *Students – Breach of Academic Integrity Procedures* and the *Higher Education Assessment Procedures*.

---

## 8. Quick checklist

**Models**
- [ ] 2.1 dataset has 104 rows and exactly 8 explanatory variables
- [ ] 2.2 dataset has 208 rows and exactly 8 explanatory variables
- [ ] Every variable is known before the match
- [ ] No more than 4 variables shared between the two models
- [ ] Cross-validation applied (Pass)
- [ ] EDA used to choose and confirm variables (Credit and above)
- [ ] Feature engineering or data transformation tried (Credit)
- [ ] Extensive experiments with a clear improvement (Distinction)
- [ ] Other regression models compared, with recommendations (High Distinction)
- [ ] Clear, accurate, well-justified charts that tell the story

**Report**
- [ ] One .docx, A4, 10 pt, single-spaced, **4 pages or fewer**, including title, names and IDs
- [ ] Introduction and Conclusion included
- [ ] Explains why and how the variables were chosen, and explains the results
- [ ] No Python code inside the report
- [ ] Written in your own words

**Submission .zip**
- [ ] Report (.docx)
- [ ] .txt file with the repository link (all Python files and dataset)
- [ ] Turnitin originality report
- [ ] AI Usage Declaration Form signed by all members
- [ ] Submitted on Learnline before **14:00 ACST, 15 October 2026**

**Team**
- [ ] Everyone's contributions documented on the Microsoft Teams space
