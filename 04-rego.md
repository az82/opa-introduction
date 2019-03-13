# An Introduction to the Rego Language

## What is Rego?

Rego is a declarative logic programming language that was inspired by Prolog.
In contrast to imperative or functional languages, you create rules that constrain results.

## Basic Types

### Scalars

Basic types:

- String
- Integer
- Float
- Boolean
- Reference

```rego
name = "Andreas"
answer = 42
pi = 3.14
allowed = true
nullRef = null
piRef = pi
```

### Composite Values

Composite types:

- Array
- Set
- Object

```rego
fib := [0, 1, 1, 2, 3, 5, 8]
roles := {"developer", "admin"}
userAz := { "name": "Andreas", "roles": roles }

fib[4]
fib[_]

roles[1] # undefined
roles[x]

userAz.name
```

## Rules as a Key Concept

Everything in Rego is a rule. Rules follow a simple format: `HEAD BODY*`

```rego
pi=3.14
can_pigs_fly { pi = 4 }
```

If `BODY` is omitted, it defaults to `{true}`

```rego
override = true {true}
can_pigs_fly { override }
```

Statements in rules are ANDed:

```rego
allow {true;false}
```

Multiple bodies are ORed:

```rego
allow {true;false}{true}
```

Remember, everything is a rule:

```rego
y { x = 5 }
y
# -> true, because the rules allow a configuration where `x=5`
x = 2
y
# -> false, because y can't be 2 and 5 at the same time
```

## See also

- Prolog on Wikipedia:[en.wikipedia.org/wiki/Prolog](https://en.wikipedia.org/wiki/Prolog)