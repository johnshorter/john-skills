---
name: teaching-python
description: >
  Teaching Python to students, from zero to productive. Use when preparing to teach Python,
  designing a Python lesson, exercise set, curriculum, or assessment, or onboarding someone to
  Python. For tutoring one learner live, use learn or teach. For talk delivery, use
  lecture-design. For exercise-directory scaffolding, use scaffold-exercises.
---

# Teaching Python

This is the pedagogy layer, not the craft layer. It captures how we teach Python here, for
students who mostly did not come to study programming.

It borrows two principles from the `learn` and `teach` skills and does not restate them:
storage strength over fluency (design for what they retain a month later, not what feels
smooth in the room), and desirable difficulty (retrieval practice, spacing, interleaving).
Read those skills for the general tutoring stance.

## The concept order

Teach in the order that keeps working memory small and builds the right mental model early.

1. **Run something first.** A three-line script that does a visible thing, before any theory.
   Motivation before mechanics.
2. **Values and variables.** Introduce the names-are-bound-to-objects model here. Most later
   confusion (aliasing, mutability, function arguments) is this idea not landing early.
3. **Core data types.** `int`, `float`, `str`, `bool`, and the difference between them.
4. **Lists and dicts.** The two workhorses. Dicts early, they are undertaught and central.
5. **Control flow.** `if`, `for`, `while`. Indentation as the grammar, not decoration.
6. **Functions.** Arguments, return values, scope. The unit of reuse.
7. **Files and data.** Reading a real file, then a dataframe. Now they can do their own work.
8. **Abstraction, only when motivated.** Comprehensions, then classes, introduced against a
   problem that makes them obviously better, never as a feature tour.

Resist teaching classes early. Bioscience students rarely need them in week one and they
crowd out the fundamentals.

## Preempt the misconceptions

The full map is in [references/misconception-map.md](references/misconception-map.md): what
each misconception looks like when a student has it, and the one demo that fixes it. Cover
the big ones deliberately rather than waiting for them to cause a bug: indentation as syntax,
names versus values, mutability, `is` versus `==`, ranges and off-by-one, list versus dict,
integer versus float, scope, truthiness, and the out-of-order-notebook-cell trap.

## Exercise design

- **One tangible win per exercise.** Small enough to finish, real enough to feel like progress.
- **Worked example, then apply.** Solve a *parallel* problem with the reasoning narrated, then
  ask them to apply the method to a different one. Never hand them the solution to their own
  assigned task.
- **Design for intuition, not just a passing grade.** An exercise a student can pass by pattern
  matching without understanding has failed. Ask them to predict output, find the bug, or
  explain why, not only to produce code.
- **Use their domain.** Sequences, counts, gene tables, dosages. Relevance carries motivation.
- **Retrieval and spacing.** Revisit earlier concepts in later exercises. Interleave problem
  types once they have the pieces.

## The teaching loop and the room

Run a lecture, then a hands-on lab, then homework that consolidates. In the lecture, live-code,
and make deliberate mistakes so they see debugging as normal, not shameful.

Expect a wide skill spread in one class. Give a clear core path everyone must finish and
optional extensions for the ones who race ahead, so nobody is bored or stranded.

## Assessment

Test whether they can read and debug code, not only write it from scratch. Reading and fixing
is closer to what they will actually do and harder to fake. Common exam pitfalls: questions
that reward memorized syntax over reasoning, and problems too large for the time given.

## Student environment

Setup should not eat week one. Start students on the lowest-friction option that works, then
graduate them. LAB CALL: whether students use Colab, local installs, or a shared notebook or
conda environment, and the exact first-day setup steps so nobody loses a session to
installation.
