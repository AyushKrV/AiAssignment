AI Assignment 1 - Classical Reasoning System
============================================
Name     : Ayush Kumar Verma
Roll No. : M26MER011
GitHub   : https://github.com/AyushKrV/AiAssignment

SUBMISSION CONTENTS
-------------------
submission/
  reasoning_agent.ipynb  Complete implementation (translators, reasoning engine,
                         experiments, traces, submission generator)
  report.pdf             Report: representation, algorithms, experiments, traces
  submission.csv         Predictions in the format: id,label (True/False)
  README.txt             This file

APPROACH (SHORT)
----------------
Natural language -> regex translator -> facts + rules -> forward chaining -> True/False

* Translator: the context is split into "Facts:" and "Rules:". Each rule line is matched
  against five sentence templates and becomes a rule  A -> B. Sentences are normalised
  (lower-case, no trailing full stop, "the" dropped) and used as atoms.
* Reasoning engine: forward chaining to a fixpoint. A query is True if and only if its
  goal atom is derived. Negation is handled by negation as failure.
* No generative AI is used. Every label is produced by the classical reasoning engine.
* The same engine is also run on CounterBench and FOLIO (different translators) as a
  generality check.

RESULTS ON PUBLIC DATA (from the notebook)
------------------------------------------
RuleTaker    98.3% (983/1000)   total reasoning time 0.07 s
CounterBench 96.0% (960/1000)   total reasoning time 0.08 s
FOLIO        61.3% (614/1001)   total reasoning time 0.06 s

HOW TO RUN
----------
Requirements: Python 3, pandas, and the Hugging Face "datasets" package (the last one is
only needed for the public-data experiments).

1. Open reasoning_agent.ipynb in Jupyter or Google Colab and run the cells in order.
   - If the public datasets cannot be downloaded, the experiment cells are skipped
     and the engine and submission cells still work.
   - Section 4 prints accuracy and inference time for each public dataset.
2. To generate predictions for a test file, go to section 7 ("Generate submission.csv"),
   set TEST_PATH to the test file (.csv, .tsv, .json, .jsonl or .parquet) and run
   that cell. It finds the context, statement and id columns by name, writes
   submission.csv with columns id,label, and prints the number of rows and the total
   inference time.

NOTE ON submission.csv
----------------------
The submission.csv in this folder was generated from the 3001 public examples
(ids ruletaker_0 ... ). Re-run section 7 on the test file to produce the final
predictions.
