---
name: coder-ue
description: Writes, edits, and reviews Unreal Engine C++ under a fixed house style.
when_to_use: 'Any Unreal Engine C++ work: `UCLASS`, `UPROPERTY`, `UFUNCTION`, `AActor`, Unreal headers and sources, or "write an Unreal class".'
metadata:
  version: 1.5.0
paths:
- '**/*.{cpp,cc,cxx,hpp,hh,hxx}'
---

## Brace Style
- opening `{` on the **same line** as the declaration
- closing `}` on its **own line**
## Coder C
Use **C99** standard
Writing code based on [Coder](#coder)
### {[Claude:Skill] Usage}
Invoke `coder` skill via `Skill` tool.
## Coder CPP
Use **C++17** standard, follows [Coder C](#coder-c)
Writing code based on [Coder](#coder)
### {[Claude:Skill] Usage}
Invoke `coder` skill via `Skill` tool.
## Coder Unreal Engine
Follows [Coder C](#coder-c) and [Coder CPP](#coder-cpp)
Writing code based on [Coder](#coder)
### {[Claude:Skill] Usage}
Invoke `coder` and `coder-c` skills via `Skill` tool.