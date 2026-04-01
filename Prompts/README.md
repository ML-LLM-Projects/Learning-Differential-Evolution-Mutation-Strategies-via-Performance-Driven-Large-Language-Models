This file includes the two prompts employed in the two main stages of the proposed framework.
The prompt in Stage 1 guides the LLM to generate new mutation operators by leveraging performance summaries of canonical DE strategies. It provides baseline results, a history of previously generated mutations, and implementation constraints, encouraging the model to propose novel, non-duplicated operators compatible with the DE framework. Through this iterative generation loop, candidates are evaluated and ranked, and the best-performing operator is selected as the baseline for the subsequent refinement stage.

## Generation Prompt (Stage 1)

```text
You are a world-class optimization researcher. 
Your goal is to design a new and superior mutation strategy for DE.

# I have tested several mutation strategies on 7 different 
FUNCTIONS, and I am sharing a COMPARATIVE SUMMARY AVERAGE FITNESS 
(Avg_Fitness):
{performance_summary}

The following table shows the mutations in each cycle. 
Do not repeat any of the ones that have already been generated.
{history}

Base your research on the following 7 mutations:
# Implementation of a Base Strategy (DE/rand/1):

{base1}
.
.
.

Your main goal is to generate a new and novel mutation. 

To do this, you must build upon the best-performing mutation 
from the history provided. 

The "best" one is defined as the entry with the minimum 
Avg_Fitness value. 

Take this strategy as your base and introduce a slight, 
creative modification to it.

Originality: The generated function must not have an 
identical formula or be a simple renaming of any function currently 
in the history.

Imports: The implementation must include `import numpy as np`.

Function Name and Signature (must be exactly):
def generated_mutation(i: int, population: np.ndarray, 
fitness: np.ndarray, F: float, low_b: float, 
high_b: float) -> np.ndarray:

Output Format: Do not include any text or explanation.
The output must be only the function code.
```

The prompt in Stage 2 iteratively refines the mutation operator obtained in Stage 1 by guiding the LLM to propose small modifications based on performance feedback. At each step, the model receives the current best operator and comparative results, generating improved variants that are evaluated and stored. This feedback-driven loop enables the model to reinforce beneficial changes and progressively enhance the operator’s performance.

## Refinement Prompt (Stage 2)

```text
You are a world-class optimization researcher. 
Your goal is to design a new and superior mutation strategy for DE.

# I have tested several mutation strategies on 7 different 
FUNCTIONS, and I am sharing a COMPARATIVE SUMMARY AVERAGE FITNESS 
(Avg_Fitness):
{performance_summary}

The following table shows the mutations in each cycle. 
Do not repeat any of the ones that have already been generated.
{history}

Base your research on the following 7 mutations:
# Implementation of a Base Strategy (DE/rand/1):

{base1}
.
.
.

Your main goal is to generate a new and novel mutation.

To do this, you must build upon the mutation strategy that performs 
BEST according to the COMPARATIVE RESULTS.

Here, "best-performing" is defined as the mutation that WINS in the 
per-function comparison (i.e., improves Avg_Fitness on the largest 
number of benchmark functions and shows fewer or smaller regressions).

Use the comparative summary to identify which mutation currently 
dominates the comparison.

Take this winning mutation as your base and introduce a small, 
targeted modification aimed at preserving its strengths while 
reducing its weaknesses.

Originality: The generated function must not have an identical formula 
or be a simple renaming of any function currently in the history.

Imports: The implementation must include `import numpy as np`.

Function Name and Signature (must be exactly):
def generated_mutation(i: int, population: np.ndarray, 
fitness: np.ndarray, F: float, low_b: float, 
high_b: float) -> np.ndarray:

Output Format: Do not include any text or explanation.
The output must be only the function code.
