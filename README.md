# LLMLang: A Doctrine for a Truly LLM-Friendly Programming Language

## Repository: **llmlang-doctrine**

---

## Mission

**LLMLang** is a new programming language designed from the ground up to be optimally friendly for Large Language Models (LLMs) and code generation tools.  
This repository presents the founding doctrine: every contributor and ecosystem maintainer must adhere to these principles when developing the language, standard library, tools, or any infrastructure.

---

## LLM-Friendly Language Doctrine

### 1. Maximal Unambiguity and Formalism

- Every syntax element must have only one clear, explicit interpretation.
- For each task, there must be a single canonical way to express it—no syntactic "magic" or shortcuts.
- All operations must be explicit; implicit behaviors and hidden conversions are forbidden.

### 2. Standardization and Predictability

- All constructs must follow a uniform style (e.g., `call function args to result` for all function/method calls).
- New features must conform to the established patterns of the core language and standard library.
- Behavior must be consistent regardless of platform or context.

### 3. Explicit Data Flow

- All variables, struct fields, function results, and array values must be explicitly named and declared.
- Assignments always use a clear operator (such as `to`), never overloaded or ambiguous operators like `=`.
- No implicit global or hidden state; all data must be passed explicitly via parameters or named variables.

### 4. Easy Parsing and Generation

- Every language construct must be easily parsable by LLMs and automated tools.
- No overloaded operators or multi-purpose symbols.
- Any action should be expressible as a simple, single-purpose command or function.

### 5. Explicit and Simple Control Flow

- Only simple, canonical control structures (`if`, `loop`, `call`, `foreach`, etc.).
- All nesting must be explicit and stepwise; avoid complex nested expressions or closures.

### 6. Minimal Syntactic Noise

- No superfluous symbols or sugar: every character in the syntax serves a clear purpose.
- Syntax is chosen for machine clarity, not for human aesthetics.

### 7. Extensible Standard Library

- All new functions, structures, and modules must be specified according to the same rules as the language core.
- Extensions are always implemented as separate modules/files—never as hidden or magical features.

### 8. Machine-Readable Documentation

- All documentation and specifications must be structured to be as easily parseable by LLMs as by humans.
- For every language and library element, inputs, outputs, side effects, and constraints must be explicitly described.

### 9. Safety and Absence of Magic

- The language must not allow implicit state changes or side effects without explicit notation.
- No hidden contexts, closures, or non-obvious references.

### 10. The Machine is the Primary User

- All improvements or changes to the language, compiler, libraries, or tooling must be evaluated first from the perspective of LLMs and automated code generation, not just humans.
- Priority: minimize error risk for code generation, maximize ease of code analysis and auto-completion, ensure compatibility with static analysis and automated testing.

---

## Manifesto

> **LLMLang is a language where every operation has one, absolutely transparent and predictable form, and every part of the language is designed primarily for machines—not humans.**

All contributors must follow this doctrine and must not introduce anything that reduces the formality, unambiguity, or predictability of the language for LLMs and automated tools.

---

## Contributing

If you want to join the development or suggest enhancements, please open an issue or a pull request.  
Every proposed change must explicitly state how it aligns with the LLMLang doctrine.

---
