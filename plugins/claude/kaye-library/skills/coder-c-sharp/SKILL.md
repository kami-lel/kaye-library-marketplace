---
name: coder-c-sharp
description: 'Writes, edits, and reviews C# code under a fixed house style: brace placement and XML documentation comments.'
when_to_use: Use for any C# code work, requests for C#, mentions of .NET.
metadata:
  version: 1.5.1
paths:
- '**/*.cs'
---

## Brace Style
- opening `{` on the **same line** as the declaration
- closing `}` on its **own line**
## Coder C Sharp
Writing code based on [Coder](#coder)
Documentation: Use XML comments (`/// <summary>...</summary>`) to document functionality and provide examples wherever helpful.
### {[Claude:Skill] Usage}
Invoke `coder` skill via `Skill` tool.