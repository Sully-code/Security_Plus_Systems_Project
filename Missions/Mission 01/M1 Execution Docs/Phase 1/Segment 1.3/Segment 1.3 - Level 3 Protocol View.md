# **Driving Question:** "What address does the phone actually use, and how is it assigned?"

## **My Initial Mental Model:**

- _(yours — step 1 of the Execution Workflow: what IP does your phone have once that authentication succeeded, where did it come from, is it globally routable, where did it land, and what address does Google actually see?)_

### **Initial Model Accuracies**

|My Guess|Real Engineering Parallel|
|---|---|
|_(pending AI validation)_||

#### **Acronym Glossary — Initial Model Accuracies Table**

- _pending_

### **Corrections to Initial Model**

|My Words|Accurate Framing|Why It Matters for Sec+|
|---|---|---|
||||

##### **Quick Reference — [name set when content exists]**

*(CONDITIONAL — commit only if 2+ corrections share an axis worth comparing
side-by-side. If no distillation emerges, delete this heading and table entirely.)*

| [Axis col 1] | [Axis col 2] | [Axis col 3] |
| --- | --- | --- |
| *[row]* | *[row]* | *[row]* |

##### **The Actual Flow (Simplified)**

*(MANDATORY whenever the segment traces a chronological process — 1.3 requires it.)*

1. *[Step — plain language]*
2. *[Step — plain language]*
3. *[Step — plain language]*

**Key insight for Security+:** *[One sentence — the transferable principle this flow
demonstrates, tied to the segment's mapped requirements (1.2-F, 2.3-C, 4.1-A).]*

##### **Technical Reference (Full Terminology)**

- _pending_

---

## **Systematic Mental Model:**

[[Mission 01 Passport]] Section 6 (System Architecture)

|Abstraction Level|Name|Focus|Security+ Relevance|
|---|---|---|---|
|Level 0|Human View|Phone → Internet → Google → Webpage|3.2-A (Infrastructure scope)|
|Level 1|Major System View|Components + data flow|Multiple (trust boundaries concept)|
|Level 2|Network Architecture|gNodeB, RAN, Carrier Core details|4.5-A/C (Controls placement)|
|==Level 3==|==Protocol View==|==HTTPS → TLS → TCP/IP → Physical==|==1.4-A/B (Crypto timing)==|
|Level 4|Infrastructure View|Actual hardware/components|1.1-G (Physical controls)|
|Level 5|Evidence View|What proves it happened (logs, captures)|4.9-A/B (Data sources)|

## **Products:**

- _Addressing architecture artifacts (Artifacts 5–6) — added when accepted_

## **Knowledge Check:**

### Quiz — Segment 1.3 "Understood" Requirements

- _Quiz added at segment closure, per the 1.2 lesson: diagram/auth artifacts first, then quiz, then snapshot._

## **Security+ Prelab Snapshot**

[[Sub-requirements Matrix]]

|Requirement|Status|Why|Evidence|
|---|---|---|---|
|**1.2-F** Authorization|_(pending quiz)_|||
|**2.3-C** Mobile device vulnerabilities|_(pending quiz)_|||
|**4.1-A** Secure baselines|_(_pending quiz)_|||

---

Phase 1.4: [[Segment 1.4 - DNS Resolution Architecture]]

---

Notes on scaffold choices, so you know the rationale behind every cell: **Plan name left blank** — 1a/1b in 1.2 emerged from your answers, not mine, so the frame names when your mental model exists. The lead framing ("composite" frame: what you hold vs. what Google sees) is a hypothesis, not a frame I'm imposing on the table. This maps to the production schedule row for segment 1.3: the addressing work maps to 1.2-F (Authorization), 2.3-C (Mobile device vulnerabilities), 4.1-A (Secure baselines) — mapping col counts held: accuracies 2 cols, corrections 3 cols, systematic table 4 columns with ==highlighted== row, snapshot stays 4 columns (Requirement/Status/Why/Evidence).

Your move, per the workflow: the initial mental model for addressing — including the sub-questions from the production schedule (is it globally routable, what addresses exist at different layers, where NAT occurs, how assignment happens). No look-ups first; rough bullets.