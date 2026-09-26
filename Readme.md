# Turing Machine Simulator

A Turing machine simulator implemented in **Python** to recognize a language over the alphabet `{a, b, c}`.

The machine accepts strings where the number of `a` symbols is exactly three times the combined number of `b` and `c` symbols:

```text
|w|a = 3 × (|w|b + |w|c)
```

The project models the transition function explicitly and provides a step-by-step visualization of the tape, head position, and current state during execution.

## Example Language

Accepted strings satisfy the relationship above.

Examples:

```text
aaab
aaaaaabb
```

Rejected examples include:

```text
aab
bbb
```

## How It Works

For each `b` or `c` encountered, the machine marks that symbol and searches the tape for three unprocessed `a` symbols.

Temporary symbols are used to track processed input:

- `x` marks processed `a` symbols
- `y` marks processed `b` and `c` symbols

Once all `b` and `c` symbols have been processed, the machine verifies that no unprocessed input symbols remain.

## State Machine

The implementation contains **11 states**:

- `q1` — initial scanning state
- `q2`–`q8` — tape traversal and symbol-marking states
- `q9` — final verification
- `q10` — accept state
- `q11` — reject state

The transition function is represented directly in Python:

```python
def delta(input_tuple: TuringInput) -> TuringOutput:
    ...
```

Python's `match-case` syntax is used to express transitions based on the current state and tape symbol.

## Implementation

The simulator uses:

- `Enum` for machine states and tape symbols
- `IntEnum` for head movements
- `NamedTuple` for transition inputs and outputs
- Python type hints
- Dynamic tape expansion
- Explicit accept and reject states

The simulated tape automatically expands when the head moves beyond its current boundaries.

## Step-by-Step Simulation

For each transition, the program displays:

- Current state
- Current tape contents
- Read/write head position

A maximum of 1,000 transitions is enforced to prevent a non-terminating execution from running indefinitely.

## Running the Simulator

### Requirements

Python 3.10 or newer is recommended because the implementation uses structural pattern matching.

Clone the repository:

```bash
git clone https://github.com/saw-cdt/turing-machine-simulator.git
cd turing-machine-simulator
```

Run:

```bash
python main.py
```

Enter a string containing only `a`, `b`, and `c`. Submit an empty input to exit.

## Example

```text
Input: aaab

State: q1
...
Result: accepted
```

## Concepts Demonstrated

This project provides a direct implementation of several theoretical computer science concepts:

- Turing machines
- Formal languages
- Transition functions
- State machines
- Tape-based computation
- Symbol marking
- Language recognition

The implementation intentionally models the machine at the transition level rather than replacing the recognition process with a direct arithmetic check.
