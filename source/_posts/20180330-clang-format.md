---
title: Unify code style using clang-format
categories: Engineer
date: 2018-03-30 11:49:14
tags:
- productivity
---


### Introduction 

[ClangFormat](https://clang.llvm.org/docs/ClangFormat.html) describes a set of tools that are built on top of LibFormat. It can support your workflow in a variety of ways including a standalone tool and editor integrations.

### Installation

*Only for Ubuntu and macOS so far*

#### Ubuntu

```bash
sudo apt-get install clang-format
# sudo apt-get install clang-format-3.8
# (version 3.8 is what I get using the first command)
```

#### macOS

```bash
# Install homebrew
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)" < /dev/null 2> /dev/null
brew install clang-format
```

Check successful installation by

```bash
clang-format -help
```


### Configuration for IDEs/Editors

*Only for Ubuntu and macOS so far, based on Ubuntu*

<span style="background: yellow;">Use: /usr/local/bin/clang-format (if for macOS)</span>
#### [CLion](https://www.jetbrains.com/clion/download/#section=linux)

- Go to `File->Settingls->Tools->External Tools`, click `+`
- Fill the create tool as following and save
```
    Name: WHATEVER_YOU_LIKE
    Program: /usr/bin/clang-format-3.8 (/path/to/your/clang-format/executable/file)
    Arguments: --style=file -i $FileName$
    Working directory: $FileDir$
```
- Go to `Keymap`, assign a shortcut for `WHATEVER_YOU_LIKE`
- Put `.clang-format` file from the end of this article under the project root
- Save and restart CLion
- Go to any script page, use the shortcut you set and see the difference. (CLion saves the page automatically)

#### [Visual Studio Code](https://code.visualstudio.com/)

- Go to `Extentions` and install `C/C++`, `Clang-Format`
- Go to `File->Preferences->Settings`
- Put the following scripts under `USER SETTING`
```
    "C_Cpp.clang_format_path": "/usr/bin/clang-format-3.8" (/path/to/your/clang-format/executable/file),
    "C_Cpp.clang_format_style": "file",
    "C_Cpp.clang_format_fallbackStyle": "none",
    "editor.formatOnSave": true,
```
- Put `.clang-format` file from the end of this article under the project root
- Save and restart VSCODE
- Go to any script page, save it and see the difference

#### [Sublime](https://www.sublimetext.com/)

- Go to `Preferences->Package Control: Install Package`
- Install `Clang Format`
- Go to `Preferences->Package Settings->Clang Format->Setting-User`, set as following
```
    {
        "binary": "/usr/bin/clang-format-3.8" (/path/to/your/clang-format/executable/file),
        "format_on_save": true,
        "style": "Custom",
    }
```
- Go to `Preferences->Package Settings->Clang Format->Custom Style-User`, add .c`lang-format` content inside, need to make some modification. For example:
```
    {
        "Language": "Cpp",
        "TabWidth": 4,
        "AlignTrailingComments": "true",
        "UseTab": "Never",
    }
```
- Save and restart Sublime
- Go to any script page, save it and see the difference

#### My .clang-format example

```
Language: Cpp
BreakBeforeBraces: Attach
PointerAlignment: Right
TabWidth: 4
IndentWidth: 4
AccessModifierOffset: 0
ColumnLimit: 120
NamespaceIndentation: All
AlignTrailingComments: true
AllowAllParametersOfDeclarationOnNextLine: true
AlwaysBreakTemplateDeclarations: true
UseTab: Never
```

You can find all explanation about each variable in the [document](https://clang.llvm.org/docs/ClangFormatStyleOptions.html).
For CLion and VSCODE, you must create a file named .clang-format and copy the content into the file.


