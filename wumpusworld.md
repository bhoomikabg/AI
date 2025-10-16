# Wumpus World

``` python
  import itertools

# Define propositional symbols
symbols = ['P11', 'P12', 'P21', 'P22', 'B11', 'B12']

# Knowledge Base (KB) as Python functions
def KB_func(values):
    P11 = values['P11']
    P12 = values['P12']
    P21 = values['P21']
    P22 = values['P22']
    B11 = values['B11']
    B12 = values['B12']

    # KB statements
    s1 = not B11                           # ~B11
    s2 = B12                               # B12
    s3 = (not B11) or (not P12 and not P21) # ~B11 -> (~P12 & ~P21)
    s4 = B12 == (P11 or P22)              # B12 <-> (P11 | P22)
    s5 = not P11                           # ~P11

    return s1 and s2 and s3 and s4 and s5

# Take user input for query
query_input = input("Enter your query (e.g., P22, P12, ~P21): ").strip()

def query_func(values):
    # Parse simple query like P22 or ~P22
    if query_input.startswith('~'):
        return not values[query_input[1:]]
    else:
        return values[query_input]

# Generate truth table
print("\nTruth Table:\n")
print(" | ".join(f"{s:^5}" for s in symbols) + " || KB True? | Query True?")
print("-" * 70)

kb_true_rows = []
for vals in itertools.product([False, True], repeat=len(symbols)):
    values = dict(zip(symbols, vals))

    kb_holds = KB_func(values)
    query_val = query_func(values)

    if kb_holds:
        kb_true_rows.append(values)
        print(" | ".join(f"{str(values[s]):^5}" for s in symbols) +
              f" ||  ✅ True   |   {query_val}")
    else:
        print(" | ".join(f"{str(values[s]):^5}" for s in symbols) +
              f" ||  False   |   {query_val}")

# Check entailment
entailed = all(query_func(v) for v in kb_true_rows) if kb_true_rows else False

print("\n" + "="*70)
if entailed:
    print(f"✅ KB entails {query_input}")
else:
    print(f"❌ KB does NOT entail {query_input}")
print("="*70)
```

# output:

```shell
PS C:\Users\student> python -u "C:\Users\student\AppData\Local\Temp\tempCodeRunnerFile.python"
Enter your query (e.g., P22, P12, ~P21): P22

Truth Table:

 P11  |  P12  |  P21  |  P22  |  B11  |  B12  || KB True? | Query True?
----------------------------------------------------------------------
False | False | False | False | False | False ||  False   |   False
False | False | False | False | False | True  ||  False   |   False
False | False | False | False | True  | False ||  False   |   False
False | False | False | False | True  | True  ||  False   |   False
False | False | False | True  | False | False ||  False   |   True
False | False | False | True  | False | True  ||  ✅ True   |   True
False | False | False | True  | True  | False ||  False   |   True
False | False | False | True  | True  | True  ||  False   |   True
False | False | True  | False | False | False ||  False   |   False
False | False | True  | False | False | True  ||  False   |   False
False | False | True  | False | True  | False ||  False   |   False
False | False | True  | False | True  | True  ||  False   |   False
False | False | True  | True  | False | False ||  False   |   True
False | False | True  | True  | False | True  ||  ✅ True   |   True
False | False | True  | True  | True  | False ||  False   |   True
False | False | True  | True  | True  | True  ||  False   |   True
False | True  | False | False | False | False ||  False   |   False
False | True  | False | False | False | True  ||  False   |   False
False | True  | False | False | True  | False ||  False   |   False
False | True  | False | False | True  | True  ||  False   |   False
False | True  | False | True  | False | False ||  False   |   True
False | True  | False | True  | False | True  ||  ✅ True   |   True
False | True  | False | True  | True  | False ||  False   |   True
False | True  | False | True  | True  | True  ||  False   |   True
False | True  | True  | False | False | False ||  False   |   False
False | True  | True  | False | False | True  ||  False   |   False
False | True  | True  | False | True  | False ||  False   |   False
False | True  | True  | False | True  | True  ||  False   |   False
False | True  | True  | True  | False | False ||  False   |   True
False | True  | True  | True  | False | True  ||  ✅ True   |   True
False | True  | True  | True  | True  | False ||  False   |   True
False | True  | True  | True  | True  | True  ||  False   |   True
True  | False | False | False | False | False ||  False   |   False
True  | False | False | False | False | True  ||  False   |   False
True  | False | False | False | True  | False ||  False   |   False
True  | False | False | False | True  | True  ||  False   |   False
True  | False | False | True  | False | False ||  False   |   True
True  | False | False | True  | False | True  ||  False   |   True
True  | False | False | True  | True  | False ||  False   |   True
True  | False | False | True  | True  | True  ||  False   |   True
True  | False | True  | False | False | False ||  False   |   False
True  | False | True  | False | False | True  ||  False   |   False
True  | False | True  | False | True  | False ||  False   |   False
True  | False | True  | False | True  | True  ||  False   |   False
True  | False | True  | True  | False | False ||  False   |   True
True  | False | True  | True  | False | True  ||  False   |   True
True  | False | True  | True  | True  | False ||  False   |   True
True  | False | True  | False | True  | True  ||  False   |   False
True  | False | True  | True  | False | False ||  False   |   True
True  | False | True  | True  | False | True  ||  False   |   True
True  | False | True  | False | True  | True  ||  False   |   False
True  | False | True  | True  | False | False ||  False   |   True
True  | False | True  | True  | False | True  ||  False   |   True
True  | False | True  | True  | True  | False ||  False   |   True
True  | False | True  | False | True  | True  ||  False   |   False
True  | False | True  | True  | False | False ||  False   |   True
True  | False | True  | True  | False | True  ||  False   |   True
True  | False | True  | True  | True  | False ||  False   |   True
True  | False | True  | True  | True  | True  ||  False   |   True
True  | True  | False | False | False | False ||  False   |   False
True  | True  | False | False | False | True  ||  False   |   False
True  | True  | False | False | True  | False ||  False   |   False
True  | True  | False | False | True  | True  ||  False   |   False
True  | True  | False | True  | False | False ||  False   |   True
True  | True  | False | True  | False | True  ||  False   |   True
True  | False | True  | False | True  | True  ||  False   |   False
True  | False | True  | True  | False | False ||  False   |   True
True  | False | True  | True  | False | True  ||  False   |   True
True  | False | True  | True  | True  | False ||  False   |   True
True  | False | True  | True  | True  | True  ||  False   |   True
True  | True  | False | False | False | False ||  False   |   False
True  | True  | False | False | False | True  ||  False   |   False
True  | True  | False | False | True  | False ||  False   |   False
True  | True  | False | False | True  | True  ||  False   |   False
True  | True  | False | True  | False | False ||  False   |   True
True  | True  | False | True  | False | True  ||  False   |   True
True  | True  | False | True  | True  | False ||  False   |   True
True  | True  | False | True  | True  | True  ||  False   |   True
True  | True  | True  | False | False | False ||  False   |   False
True  | True  | True  | False | False | True  ||  False   |   False
True  | False | True  | True  | True  | True  ||  False   |   True
True  | True  | False | False | False | False ||  False   |   False
True  | True  | False | False | False | True  ||  False   |   False
True  | True  | False | False | True  | False ||  False   |   False
True  | True  | False | False | True  | True  ||  False   |   False
True  | True  | False | True  | False | False ||  False   |   True
True  | True  | False | True  | False | True  ||  False   |   True
True  | True  | False | True  | True  | False ||  False   |   True
True  | True  | False | True  | True  | True  ||  False   |   True
True  | True  | True  | False | False | False ||  False   |   False
True  | True  | True  | False | False | True  ||  False   |   False
True  | True  | True  | False | True  | False ||  False   |   False
True  | True  | True  | False | True  | True  ||  False   |   False
True  | True  | False | True  | True  | False ||  False   |   True
True  | True  | False | True  | True  | True  ||  False   |   True
True  | True  | True  | False | False | False ||  False   |   False
True  | True  | True  | False | False | True  ||  False   |   False
True  | True  | True  | False | True  | False ||  False   |   False
True  | True  | True  | False | True  | True  ||  False   |   False
True  | True  | True  | True  | False | False ||  False   |   True
True  | True  | True  | True  | False | True  ||  False   |   True
True  | True  | True  | True  | True  | False ||  False   |   True
True  | True  | True  | True  | True  | True  ||  False   |   True
True  | True  | True  | True  | False | False ||  False   |   True
True  | True  | True  | True  | False | True  ||  False   |   True
True  | True  | True  | True  | True  | False ||  False   |   True
True  | True  | True  | True  | True  | True  ||  False   |   True


======================================================================
✅ KB entails P22
======================================================================
```
