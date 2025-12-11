# Physics Problem Restructuring Task

You are restructuring a physics problem JSON to separate FUNDAMENTAL FORMULAS from PROBLEM-SOLVING STEPS.

## What FORMULAS should contain:

ONLY fundamental formulas that come from concepts - the formulas that help you solve problems BEFORE modifying them for use in a specific problem. These are principle-type formulas one should memorize.

Examples of GOOD fundamental formulas:
- F = ma (Newton's second law)
- a_c = v²/r (centripetal acceleration)
- T = 1/f (period-frequency relation)
- v = 2πrf (linear speed from frequency)
- KE = ½mv² (kinetic energy)
- p = mv (momentum)
- τ = Iα (torque and angular acceleration)
- W = Fd cosθ (work)
- 1 J = 1 kg·m²/s² (unit definition if needed)

Examples of BAD formulas (these are problem-specific modifications - if you didn't know the problem you'd ask "what the hell does that even mean"):
- "½ (M + m) v'² ≥ (M + m) g (2ℓ)" - meaningless without problem context
- "0 = m_b v_b + m_r v_r" - this is conservation of momentum applied to specific masses
- "m₁v₀ = (m₁ + m₂)v_c" - this is momentum conservation for a specific collision

If multiple formulas are needed to solve the problem (like F=ma AND a unit conversion like 1J = 1kg·m²/s²), then ALL of those fundamental formulas should be included in the formulas array.

## What STEPS should contain:

The steps show the FULL problem-solving process in this order:

### Step 1: Start with the formulas and variables
- State which fundamental formula(s) will be used
- Example: "We will use the centripetal acceleration formula: a_c = v²/r"

### Step 2: Define variables by values given in the problem
- Assign the numerical values from the problem to the variables
- Example: "Given: m = 150 g = 0.150 kg, r = 0.600 m, f = 2.00 rev/s"
- If a problem provides a mass and a unit value, write "m = 10 kg"

### Step 3: Substitute scalars (numbers) for the variables
- First substitute the numerical values into the formula
- Example: "Substituting: a_c = v²/r where we need v first"

### Step 4: If a variable equals another variable or expression, show that substitution
- Sometimes m = another variable or multiple variables like (m + M)
- Example: "Total mass m_total = m + M = 0.150 kg + 2.00 kg = 2.15 kg"

### Step 5: Substitute symbols for numbers in the fundamental formula
- Show the formula with all numbers plugged in
- Example: "a_c = (7.54 m/s)² / (0.600 m)"

### Step 6: Show the algebraic steps for solving
- Show the arithmetic/algebra to get the final answer
- Example: "a_c = 56.85 m²/s² / 0.600 m = 94.7 m/s²"

If multiple formulas are needed, show the steps of using each one in sequence.

## Your Task:

1. Read the input problem JSON file at: /Users/kevintong/Documents/phys120/quiz/subagent_work/problem_XXX_input.json
2. Identify which formulas in correctFormulas are truly FUNDAMENTAL (memorizable physics principles from concepts)
3. Any formula that is problem-specific should be REMOVED from correctFormulas and converted into STEPS
4. Rewrite the steps array to follow the order above:
   - Start with formulas and variables
   - Define variables by values from the problem
   - Substitute scalars for numbers
   - Substitute symbols for numbers in fundamental formula
   - Show algebraic steps for solving
5. Output the corrected JSON

## Output Format:

Save your output to: /Users/kevintong/Documents/phys120/quiz/subagent_work/problem_XXX_output.json

The JSON structure:
```json
{
  "problem": "...(keep original)...",
  "source": "...(keep original)...",
  "sourceFile": "...(keep original if exists)...",
  "chapter": "...(keep original)...",
  "image": "...(keep original if exists)...",
  "variables": [...(keep original)...],
  "correctFormulas": [
    {
      "name": "Descriptive name of fundamental formula",
      "formula": "The fundamental formula like F = ma"
    }
  ],
  "steps": [
    {
      "explanation": "What this step does",
      "notations": "The mathematical notation showing the work"
    }
  ]
}
```

IMPORTANT: Make sure you preserve all fields from the original (problem, source, sourceFile, chapter, image if exists, variables). Only modify correctFormulas and steps.
