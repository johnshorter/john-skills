# Python newcomer traps

The specific mistakes that show up in a new lab member's first Python. Each one with the
symptom and the fix.

## Mutable default arguments

```python
def add(x, acc=[]):   # WRONG: the list is created once and shared across calls
    acc.append(x); return acc
```
The default is evaluated once at definition. Use `None` and build inside:
```python
def add(x, acc=None):
    if acc is None: acc = []
    acc.append(x); return acc
```

## Aliasing versus copying

`b = a` for a list, dict, or numpy array binds a second name to the same object. Mutating
`b` mutates `a`. Copy when you mean a copy: `b = a.copy()` (numpy/pandas), `list(a)`,
`copy.deepcopy` for nested structures. A numpy slice is a *view*, not a copy.

## pandas chained assignment

```python
df[df.x > 0]['y'] = 1   # WRONG: assigns into a temporary, may silently do nothing
```
Use `.loc`:
```python
df.loc[df.x > 0, 'y'] = 1
```

## `is` versus `==`

`is` tests identity (same object), `==` tests value. Use `==` for numbers and strings. Use
`is` only for `None`, `True`, `False`. `a == None` works but `a is None` is correct.

## Integer and float surprises

`/` is float division, `//` is floor division. `0.1 + 0.2 != 0.3`; compare floats with a
tolerance (`math.isclose`), never `==`. Beware integer overflow does not happen in Python
ints but does in numpy fixed-width dtypes.

## Paths

Use `pathlib.Path`, not string concatenation. `Path(base) / "sub" / "file.txt"` is portable;
`base + "/sub/" + name` breaks across systems and doubles separators.

## Unseeded randomness

Any shuffle, split, sample, or model init without a seed is not reproducible. Create one
generator (`rng = np.random.default_rng(seed)`) and thread it through.

## Mutating while iterating

Removing items from a list inside a `for item in list:` loop skips elements. Iterate over a
copy (`for item in list[:]:`) or build a new list with a comprehension.

## Notebook state

Out-of-order cell execution produces results that cannot be reproduced by running top to
bottom. Restart-and-run-all before trusting a notebook result, and move anything real into
`src/`.
