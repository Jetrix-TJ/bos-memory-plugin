---
description: Answer a question from BOS Memory, citing the memories used
argument-hint: "<question>"
---

Answer from BOS Memory: $ARGUMENTS

Call recall with the question (and get_context if it is about a task or the people in it). Answer
only from what comes back, citing each memory as memory:<id>. If memory has nothing on it, say so
plainly and do not guess. When done, call report_use with the memories you used, and put what
memory lacked in outcome.missed.
