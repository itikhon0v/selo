# Selo

**Selo** (noun): the outside, surface, outer layer, or boundary (e.g., skin, bark, peel, shell) — *Toki Pona*

## Status: Active Development

Selo is currently in active development. Features and syntax may change as the project evolves. Key milestones are:

- [ ] Stage I
  - [x] Specification:
    - [x] Syntax;
    - [x] Rules
    - [x] Guiding Principles
  - [ ] Core components (In-progress):
    - [x] Lexer
    - [ ] AST (In-Progress)
    - [ ] Parser
    - [ ] Serializer
    - [ ] Evaluator
- [ ] Stage II
  - [ ] CLI
    - [ ] Convert to/from JSON
    - [ ] Optimize/Resolve Selo configs
    - [ ] Check for errors
  - [ ] LSP
    - [ ] Diagnostics
    - [ ] Auto completion
    - [ ] Optimization/Resolution
  - [ ] Bindings:
    - [ ] Go
    - [ ] Python
    - [ ] JavaScript

## What is Selo?

**Selo** is a minimalistic configuration language inspired by Lua, but designed specifically for modularity and scalability in configuration setups. Its design is centered around:

- **Tables**: The primary data structure.
- **Variables**: For reuse and flexibility.
- **Inheritance**: Enabling extensibility and modularity.

### Purpose

Selo aims to:

- **Reduce repetition** in configuration files.
- **Simplify configuration** management.
- Enable **scalable setups** for complex use cases.

## Core Principles

### Simplicity

Minimal syntax with a single data structure: tables.

### Clarity

Predictable, readable, and concise configurations.

### Security

Scoped variables and immutability prevent unintended side effects.

## Why Selo?

### Highlights

- **Variables**: Define once, reuse anywhere.
- **Inheritance**: Extend and customize existing tables.
- **Simplicity**: Readable, flexible, and intuitive.

### Comparisons

| Language | Strengths & Weaknesses                           |
| -------- | ------------------------------------------------ |
| **JSON** | Lacks comments and is verbose.                   |
| **YAML** | Prone to ambiguity and indentation errors.       |
| **TOML** | Lacks inheritance and deep nesting.              |
| **Selo** | Combines simplicity, extensibility, and clarity. |

## How to Selo?

Selo works by 4 simple rules, providing a clear and intuitive framework for organizing configurations.

### 1. Everything is a table

Tables are the foundation of Selo's syntax:

```selo
key = "value",

list = { "item_1", "item_2", "item_3" },

nested = {
  key = "nested_value"
}
```

### 2. Language-Agnostic Data Types

Selo supports basic data types, making it intuitive for humans to write and easy for machines to parse.

- **`nil`**: Represents undefined or missing values.
- **`boolean`**: `true` or `false`.
- **`integer`**: Whole numbers, e.g., `42`.
- **`big_integer`**: Numbers with `_` for readability, e.g., `1_000_000`.
- **`float`**: Floating-point numbers, e.g., `3.14`.
- **`scientific_float`**: Scientific notation, e.g., `1.23e4`.
- **`string`**: Includes quotes and escape sequences.
- **`escape_sequences`**: Supports special characters like `\n` (newline), `\t` (tab), and Unicode (`\u{1F600}`).

### 3. Closest Value Wins

Selo resolves values using the nearest definition:

#### Overrides

```selo
key = "value_1",
key = "value_2" -- Last definition wins: "value_2".
```

#### Inheritance

```selo
base = {
  key = "base_value"
},

derived = {
  base,
  key = "overridden_value" -- Overrides "base_value".
}
```

#### Scoping

```selo
scoping = {
  key = "outer_value", -- Level 1
  inner = {
    key = "inner_value" -- Level 2
  },
  resolved = key -- Nearest scope takes precedence: "outer_value"
}
```

### 4. Inheritance and Immutability

Inheritance in Selo allows configurations to be extended without modifying the base:

```selo
base = {
  flavor = "vanilla",
  toppings = { "sprinkles" }
},

derived = {
  base,
  flavor = "chocolate" -- Overrides "vanilla".
},

extended = {
  derived,
  toppings = { "nuts", "caramel" } -- Base remains unchanged.
}
```

## Where to Selo?

Selo might work as a perfect configuration language for various scenarios, such as server setups, application configuration, CI/CD pipeline management, and modular infrastructure design. For example, in server setups, Selo's inheritance feature allows you to define a base configuration for common settings and extend it for individual environments like production or staging:

```
staging_config = {
    server = "staging.example.com",
    db = "example.com",
    captcha = false,
    port = 8080,
},

production_config = {
    staging_config,
    server = "production.example.com",
    captcha = true
}
```

## License

Selo is distributed under the [Apache 2.0 License](LICENSE). Contributions are welcome!

