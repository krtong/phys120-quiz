# Physics Problem Restructuring Task

You are restructuring a physics problem JSON to separate FUNDAMENTAL FORMULAS from PROBLEM-SOLVING STEPS, and adding a SOLUTION field.

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

Each step has TWO fields:
- **explanation**: Written text describing what we're doing and why (full sentences OK)
- **notations**: PURE MATHEMATICAL NOTATION ONLY (no sentences, minimal words)

### CRITICAL: Notation vs Explanation

The "notations" field should contain ONLY mathematical expressions, symbols, and equations. NO full sentences.

**BAD notations (DO NOT DO THIS):**
- "We will use the work formula: W = Fd cosθ, where F is the force magnitude..."
- "Since block A descends by distance L and the blocks are connected..."
- "The gravitational force on block B is F_g = m₍B₎g pointing downward"
- "Initial energy: PE_initial = m₍B₎gh (taking ground as reference)"
- "Numerator: 2(6.0 kg)(9.8 m/s²)(2.5 m) = 294 kg·m²/s²"

**GOOD notations (DO THIS):**
- "W = Fd cosθ"
- "d = L"
- "F_g = m₍B₎g, θ = 180°"
- "PE_initial = m₍B₎gh"
- "2(6.0)(9.8)(2.5) = 294"

**Acceptable short labels in notations:**
- "Given: m = 5 kg, v = 10 m/s"
- "F_net = ma => a = F/m"
- Multiple equations: "v = 2πrf, a_c = v²/r, F = ma"

**Move these to explanation field instead:**
- "We will use..."
- "Since..."
- "The force is... pointing downward"
- "Therefore..."
- "where X is the..."
- Any full sentence

### Step Structure:

**Step 1: State the formulas**
- Explanation: "We use the work formula and kinetic energy formula"
- Notations: "W = Fd cosθ, KE = ½mv²"

**Step 2: Define given values**
- Explanation: "Define the known values from the problem"
- Notations: "Given: m = 5 kg, F = 20 N, d = 3 m, θ = 0°"

**Step 3-N: Show the work**
- Explanation: "Substitute values into the work formula"
- Notations: "W = (20 N)(3 m)(cos 0°) = (20)(3)(1) = 60 J"

## What SOLUTION should contain:

The solution field is a SINGLE TEXT STRING of PURE MATH showing the complete derivation. NO written explanations - just equations flowing logically.

**GOOD solution:**
```
W = Fd cosθ
F_g = m₍B₎g, d = L, θ = 180°
W = m₍B₎g · L · cos(180°)
W = m₍B₎g · L · (-1)
W = -m₍B₎gL
```

**BAD solution (don't do this):**
```
We will use the work formula: W = Fd cosθ
The gravitational force on block B is F_g = m₍B₎g pointing downward
Since the displacement is upward, θ = 180°
Therefore W = -m₍B₎gL
```

Format using \n for line breaks. Each line should be an equation or mathematical step.

## Your Task:

1. Read the input problem JSON file at: /Users/kevintong/Documents/phys120/quiz/subagent_work/problem_XXX_input.json
2. Identify which formulas in correctFormulas are truly FUNDAMENTAL (memorizable physics principles from concepts)
3. Any formula that is problem-specific should be REMOVED from correctFormulas and converted into STEPS
4. Rewrite the steps array:
   - Put written descriptions in "explanation"
   - Put ONLY math/symbols in "notations"
5. Add a "solution" field with PURE MATH derivation (no sentences)
6. Output the corrected JSON

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
      "explanation": "Written description of what this step does (sentences OK here)",
      "notations": "Pure math only: F = ma, a = 5 m/s²"
    }
  ],
  "solution": "Formula\nSubstitution\nSimplification\nAnswer"
}
```

IMPORTANT:
- Make sure you preserve all fields from the original (problem, source, sourceFile, chapter, image if exists, variables). Only modify correctFormulas and steps, and ADD the solution field.
- Use \n for line breaks in the solution string (not actual newlines)
- Use proper Unicode characters for superscripts (² not ^2), subscripts, Greek letters, etc.
- NOTATIONS = MATH ONLY. EXPLANATION = WORDS.
