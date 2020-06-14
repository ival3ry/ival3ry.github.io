---
title: '[Coding Style] Clang format fallback Style'
published: true
---

This clang format fallback style that I use in VS Code:
```clang
{
BasedOnStyle: Mozilla,
PointerAlignment: Right,
AlignConsecutiveMacros: true,
AlignConsecutiveDeclarations: true,
AlignConsecutiveAssignments: true,
AlignEscapedNewlines: Left,
AlignTrailingComments: true,
AllowShortBlocksOnASingleLine: Always,
AllowShortCaseLabelsOnASingleLine: true,
AllowShortIfStatementsOnASingleLine: true,
AllowShortLoopsOnASingleLine: true
}
```

### How to use?
Just copy-paste it to the 'C_Cpp: Clang_format_fallback Style' field.

#### References:
[Clang-Format Style Options](https://clang.llvm.org/docs/ClangFormatStyleOptions.html#clang-format-style-options)  
