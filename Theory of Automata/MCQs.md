
### **Section 1: Mathematical Foundations & Formal Languages**

1. What is the fundamental building block of formal languages?  
A) Turing Machines  
B) Graphs  
C) Sets  
D) Trees  

1. Which mathematical concept represents all ordered pairs (a,b) where a∈A and b∈B? A) Union  
B) Intersection  
C) Cartesian Product  
D) Complement  

1. According to the abstract computational machine hierarchy, which model is the most powerful?  
A) Finite Automaton (FA)  
B) Pushdown Automaton (PDA)  
C) Turing Machine (TM)  
D) Context-Free Grammar (CFG)  

1. In a tree used for derivation (parse tree), what does the root node represent?   
A) The start symbol of the grammar  
B) A terminal symbol  
C) The empty string  
D) A dead state  

1. What is the definition of an Alphabet (Σ) in formal languages?  
A) An infinite set of strings  
B) A finite non-empty set of symbols  
C) A sequence of variables  
D) A collection of regular expressions  

1. What is the key difference between Kleene Star (Σ*) and Positive Closure (Σ+)?   
A) Σ* includes the empty string (λ), while Σ+ never includes it.  
B) Σ+ includes the empty string (λ), while Σ* never includes it.    
C) Σ* is finite, while Σ+ is infinite.  
D) There is no difference between the two operations.  

1. The operation of writing a string *w* backwards is known as: 
A) Concatenation  
B) Intersection  
C) Reverse (wR)  
D) Complement  

### **Section 2: Regular Expressions (RE)**

8. A Regular Expression (RE) is formally defined as:  
A) A formal notation for describing a context-free language.   
B) A formal notation for describing a regular language using symbols and operators.  
C) A machine with an infinite stack.  
D) A set of production rules.  

9. In Regular Expressions, what does the operator `r?` signify?   
10. A) 1 or more repetitions of r  
B) 0 or more repetitions of r  
C) Exactly one r  
D) 0 or 1 of r (Optional)  

1.  Which Regular Expression represents all strings over {a,b} starting with 'a'?   
A) (a+b)*a  
B) a(a+b)*  
C) a*b*  
D) (a+b)*a(a+b)*

1.  Which of the following best describes the language accepted by the Regular Expression `(a+b)*ab`?  
A) All strings starting with 'ab'  
B) All strings with exactly two 'a's  
C) All strings ending in 'ab'  
D) All strings of even length  

### **Section 3: Finite Automata (FA, NFA, TG)**

12. A Deterministic Finite Automaton (DFA) is formally defined as a 5-tuple. What does the transition function δ map?   
A) Q × Σ → Q  
B) Q × Γ → Q  
C) Q → Δ  
D) Q × Σ → Δ  
 
13. In DFA design, what is a "dead state"?   
A) The start state  
B) An accepting state  
C) A non-accepting state that loops on all inputs  
D) A state with no incoming transitions  

14. How does a Transition Graph (TG) relax the rules of a standard DFA? 
A) It requires exactly one transition per symbol.
B) It allows edges to be labeled with strings and can have multiple or zero transitions.
C) It incorporates an infinite stack.
D) It produces output for every input symbol.

15. [cite_start]Under what condition does a Nondeterministic Finite Automaton (NFA) accept an input string? [cite: 114, 115]
A) If all computation paths reach a final state.
B) If at least one computation path reaches a final state.
C) If it loops infinitely.
D) If it visits the start state twice.

16. [cite_start]A transition on an NFA that moves without consuming any input symbol is called: [cite: 111]
A) A dead transition
B) A λ-transition (lambda-transition)
C) A stack pop
D) An output generation

17. [cite_start]In a Generalized Transition Graph (GTG), what are the edges labeled with? [cite: 117]
A) Only single symbols
B) Only the empty string (λ)
C) Regular Expressions
D) Push and Pop operations

18. [cite_start]If an automaton accepts an input string exactly when the last state visited is in F, this is called: [cite: 335]
A) Acceptance by empty stack
B) Acceptance by final state
C) Kleene's acceptance
D) Nondeterministic acceptance

### **Section 4: Kleene's Theorem & Automata with Output**

19. [cite_start]Kleene's Theorem states that a language is Regular if and only if: [cite: 121]
A) It can be recognized by a Turing Machine.
B) It can be parsed by a Context-Free Grammar.
C) It can be described by a Regular Expression.
D) It has an even number of symbols.

20. [cite_start]When converting a Regular Expression into a Finite Automaton using Thompson's construction for Union (r+s), how are the sub-machines connected? [cite: 126]
A) By concatenating their final states.
B) By creating a new start state with λ-transitions to both machines.
C) By removing their start states.
D) By adding a loop on the original start state.

21. [cite_start]What algorithm is used to convert an NFA into an equivalent DFA? [cite: 130]
A) Thompson's Construction
B) Chomsky Normal Form conversion
C) Subset Construction
D) Pumping Lemma

22. [cite_start]How is the output generated in a Moore Machine? [cite: 139]
A) The output depends on both the current state and current input.
B) The output is written on the transitions (edges).
C) The output depends on the current state only and is written at the states.
D) The output is pushed onto a stack.

23. [cite_start]In a Mealy Machine, what is the length of the generated output string relative to the input string? [cite: 148]
A) Input length + 1
B) Exactly the input length
C) Input length - 1
D) Double the input length

24. [cite_start]When converting a Moore Machine to a Mealy Machine, what is the primary structural change? [cite: 153, 154, 155]
A) The number of states must always double.
B) Output is moved from states to transitions.
C) A stack is added to the machine.
D) All non-accepting states are removed.

### **Section 5: Regular Language Properties & Pumping Lemma**

25. [cite_start]Which of the following is NOT a closure property of Regular Languages? [cite: 165, 166, 167, 168, 169, 170, 171, 172]
A) Union
B) Intersection
C) Reversal
D) Subset derivation

26. [cite_start]What is the primary purpose of the Pumping Lemma? [cite: 175]
A) To prove that a language is Context-Free.
B) To prove that a language is Regular.
C) To prove that a language is NOT Regular.
D) To minimize the states of a DFA.

27. [cite_start]In the Pumping Lemma statement for string w = xyz, what condition applies to the 'y' portion? [cite: 180]
A) |y| = 0
B) |y| ≥ 1
C) |y| > p
D) y must contain only the symbol 'a'

### **Section 6: Context-Free Grammars (CFG)**

28. A Context-Free Grammar (CFG) is represented as a 4-tuple G = (V, T, P, S). [cite_start]What does 'V' represent? [cite: 193, 194, 195]
A) Tape symbols
B) Terminals
C) Non-terminals (Variables)
D) Pushdown stack elements

29. [cite_start]What defines an Ambiguous Grammar? [cite: 212]
A) A grammar with λ-productions.
B) A grammar where some string has more than one parse tree.
C) A grammar that uses a Pushdown Automaton.
D) A grammar written in Chomsky Normal Form.

30. [cite_start]In a Leftmost Derivation, which non-terminal is replaced at each step? [cite: 204]
A) The rightmost non-terminal
B) Any random non-terminal
C) The leftmost non-terminal
D) Only the start symbol

31. [cite_start]In a CFG derivation, what is a "Sentential form"? [cite: 335]
A) A string consisting entirely of terminals.
B) A string consisting entirely of non-terminals.
C) An intermediate string containing a mix of terminals and non-terminals.
D) The final language output.

32. A Regular Grammar is defined by productions that are either Right-Linear or Left-Linear. [cite_start]Which of the following is a Right-Linear production? [cite: 218]
A) A → Ba
B) A → aB
C) A → BC
D) A → BCD

33. [cite_start]When simplifying a CFG, what must be done to remove a Unit Production (A → B)? [cite: 230, 231]
A) Add A → α for every B → α that is not a unit production, then remove the unit productions.
B) Replace all B's with λ.
C) Remove the start symbol.
D) Convert the grammar to a DFA.

34. [cite_start]Which of the following defines a "Nullable variable" in a CFG? [cite: 224, 335]
A) A variable that can derive a terminal string.
B) A variable reachable from the start symbol.
C) A variable that can derive the empty string (λ).
D) A variable that only produces other non-terminals.

35. [cite_start]When eliminating "Useless Productions" in a CFG, a variable must be both Reachable and what else? [cite: 233, 234, 235]
A) Nullable
B) Generating (able to derive a terminal string)
C) Context-Sensitive
D) Deterministic

36. [cite_start]Which of the following rules strictly adheres to Chomsky Normal Form (CNF)? [cite: 237]
A) A → aBc
B) A → λ
C) A → BC or A → a
D) A → Ba

### **Section 7: Pushdown Automata (PDA)**

37. [cite_start]What computational capability makes a Pushdown Automaton (PDA) more powerful than a Finite Automaton? [cite: 247]
A) An infinite tape
B) Nondeterministic transitions
C) An infinite stack
D) Regular expressions on edges

38. [cite_start]In the 7-tuple definition of a PDA, what does Γ (Gamma) represent? [cite: 249, 254, 255]
A) Start state
B) Input alphabet
C) Transition function
D) Stack alphabet

39. The transition notation for a PDA is often written as (state, input, stack_top) → (new_state, push_string). [cite_start]What does a "POP" operation conceptually do? [cite: 267, 268]
A) Replaces the top symbol with a new string.
B) Replaces the top symbol with λ (empty).
C) Moves the head to the right.
D) Adds the start symbol to the stack.

40. [cite_start]When converting a CFG to a PDA using the standard method, how many states are typically created? [cite: 271, 272]
A) 2 (start, working)
B) 3 (start, working, accept)
C) 5 (start, 3 working, accept)
D) Equal to the number of non-terminals

41. [cite_start]According to the standard algorithm for PDA to CFG conversion, the variable created takes the form: [cite: 279]
A) [A, B]
B) [p, A, q]
C) {q0, Z0}
D) (Q, Σ, Γ)

### **Section 8: Turing Machines (TM)**

42. [cite_start]What is the most powerful computational model according to the study hierarchy? [cite: 284]
A) Pushdown Automaton
B) Turing Machine
C) Generalized Transition Graph
D) Context-Free Grammar

43. [cite_start]In a Turing Machine transition δ(q, X) = (p, Y, D), what does 'D' denote? [cite: 294]
A) The symbol to write
B) The next state
C) The movement direction of the head (L or R)
D) The blank symbol

44. [cite_start]In a Turing Machine, the INSERT subprogram works by: [cite: 309, 310, 311]
A) Erasing the current tape cell.
B) Shifting tape content to insert a new symbol at the current position.
C) Moving the head infinitely to the left.
D) Emptying the stack.

45. [cite_start]The Church-Turing Thesis states that: [cite: 315, 316]
A) Every NFA can be converted to a DFA.
B) Any algorithm computed by a reasonable device can be computed by a Turing Machine.
C) Context-free languages are a subset of regular languages.
D) Grammars must be in Chomsky Normal Form to be computable.

46. [cite_start]In the Chomsky Hierarchy, what type of language does a Turing Machine recognize? [cite: 318]
A) Type 3 (Regular)
B) Type 2 (Context-Free)
C) Type 1 (Context-Sensitive)
D) Type 0 (Recursively Enumerable)



### **Answer Key**
1. **C** (Sets) 
3. **C** (Turing Machine) [cite: 34, 35]
2. **C** (Cartesian Product) [cite: 21, 22]
4. **A** (The start symbol of the grammar) [cite: 30, 31, 32]
5. **B** (A finite non-empty set of symbols) [cite: 39]
6. **A** (Σ* includes the empty string (λ), while Σ+ never includes it.) [cite: 52, 53, 55]
7. **C** (Reverse) [cite: 49, 50]
8. **B** (A formal notation for describing a regular language using symbols and operators.) [cite: 60]
9. **D** (0 or 1 of r) [cite: 62]
10. **B** (a(a+b)*) [cite: 65]
11. **C** (All strings ending in 'ab') [cite: 70]
12. **A** (Q × Σ → Q) [cite: 79, 84, 85]
13. **C** (A non-accepting state that loops on all inputs) [cite: 99]
14. **B** (It allows edges to be labeled with strings and can have multiple or zero transitions.) [cite: 106, 107, 108]
15. **B** (If at least one computation path reaches a final state.) [cite: 114, 115]
16. **B** (A λ-transition) [cite: 111]
17. **C** (Regular Expressions) [cite: 117]
18. **B** (Acceptance by final state) [cite: 335]
19. **C** (It can be described by a Regular Expression.) [cite: 121]
20. **B** (By creating a new start state with λ-transitions to both machines.) [cite: 126]
21. **C** (Subset Construction) [cite: 130]
22. **C** (The output depends on the current state only and is written at the states.) [cite: 139]
23. **B** (Exactly the input length) [cite: 148]
24. **B** (Output is moved from states to transitions.) [cite: 153, 154, 155]
25. **D** (Subset derivation) [cite: 165, 166, 167, 168, 169, 170, 171, 172]
26. **C** (To prove that a language is NOT Regular.) [cite: 175]
27. **B** (|y| ≥ 1) [cite: 180]
28. **C** (Non-terminals (Variables)) [cite: 193, 194, 195]
29. **B** (A grammar where some string has more than one parse tree.) [cite: 212]
30. **C** (The leftmost non-terminal) s31. **C** (An intermediate string containing a mix of terminals and non-terminals.) [cite: 335]
31. **B** (A → aB) 
32. **A** (Add A → α for every B → α that is not a unit production, then remove the unit productions.) 
33. **C** (A variable that can derive the empty string (λ).) 
34. **B** (Generating (able to derive a terminal string)) 
35. **C** (A → BC or A → a) 
36. **C** (An infinite stack) 
37. **D** (Stack alphabet) 
38. **B** (Replaces the top symbol with λ (empty).) 
39. **B** (3 (start, working, accept)) 
40. **B** ([p, A, q]) 
41. **B** (Turing Machine) 
42. **C** (The movement direction of the head (L or R)) 
43. **B** (Shifting tape content to insert a new symbol at the current position.)
44. **B** (Any algorithm computed by a reasonable device can be computed by a Turing Machine.) 