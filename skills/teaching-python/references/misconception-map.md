# Python misconception map

Each entry: how it shows up when a student holds it, and the demo that fixes it.

## Indentation is syntax
Symptom: random indentation, or an `IndentationError` they cannot read. They think spaces are
cosmetic.
Fix: show two versions of the same loop, one where the print is inside and one outside, run
both, let them see indentation change the behavior.

## Names versus values
Symptom: `b = a; b.append(1)` and they are surprised `a` changed.
Fix: draw two labels pointing at one box. Then show `b = a.copy()` pointing at a second box.

## Mutability
Symptom: expecting a function that takes a list to leave the caller's list untouched.
Fix: pass a list into a function that appends to it, print the caller's list after. Contrast
with an int, which does not change.

## `is` versus `==`
Symptom: `x == None`, or comparing strings with `is` and getting surprising results.
Fix: `1000 is 1000` can be False, `1000 == 1000` is True. Rule: `==` for values, `is None` for
None.

## Ranges and off-by-one
Symptom: `range(1, 10)` and they expect it to include 10; loops that miss the last element.
Fix: `list(range(1, 10))` printed, so they see the endpoint is excluded.

## List versus dict
Symptom: scanning a list with a loop to find a value that a dict lookup would give directly.
Fix: same task both ways, then time them on a large input.

## Integer versus float
Symptom: `5 / 2` surprising them, or float equality checks that fail.
Fix: show `/` versus `//`, then `0.1 + 0.2` printed to 17 digits.

## Scope
Symptom: expecting a variable set inside a function to exist outside it.
Fix: set a variable inside a function, try to print it outside, read the `NameError`.

## Truthiness
Symptom: `if x == True:`, or confusion about empty lists and strings in conditions.
Fix: show that `[]`, `""`, `0`, and `None` are falsy; write `if x:` not `if x == True:`.

## Out-of-order notebook cells
Symptom: a notebook that works for them but not on restart, because a variable was defined in
a cell they ran earlier and later deleted.
Fix: Restart and Run All in front of them, watch it break, teach it as a habit.
