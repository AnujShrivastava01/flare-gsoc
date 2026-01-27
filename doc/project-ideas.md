# Project Ideas
*FLARE @ Google Summer of Code 2026*

This document lists examples of projects that would be great for GSoC 2026 contributors.
The list doesn't include everything - feel free to identify your own idea and propose it!

All of our project ideas revolve around reverse engineering tools.
That is, we want to improve the lives of malware analysts through novel techniques and automation.
To succeed with any of these examples, you should have a basic familiarity with reverse engineering or a strong desire to learn.

Our tools are used by thousands of analysts to identify, describe, and stop malware.

Briefly:
- [capa](https://github.com/mandiant/capa) identifies the capabilities in executable files, such as "installs a service" or "downloads data via HTTP".
  - enhance static analysis
  - enhance dynamic analysis
- [FLOSS](https://github.com/mandiant/flare-floss) automatically deobfuscated protected strings in malware.
  - extract language specific strings (.NET, Swift, Zig, ...)
  - QUANTUMSTRAND
- [GoReSym](https://github.com/mandiant/GoReSym) is a Go symbol parser that extracts program metadata (such as CPU architecture, OS, endianness, compiler version, etc), function metadata, filename and line number metadata, and embedded structures and types.

## capa: Native Script Analysis Support

*size*: large, estimated 350 hours

*difficulty*: hard

*mentors*: [@mike-hunhoff](https://github.com/mike-hunhoff), [@Maijin](https://github.com/Maijin), [@larchchen](https://github.com/larchchen)

Current static analysis tools often struggle with scripting languages, relying on fragile regular expressions that are easily evaded. As adversaries increasingly "Live off the Land" using scripts, the need for robust, structural analysis is critical.

This project aims to extend the **capa** engine to natively support static analysis of scripting languages by integrating **Tree-sitter**. By moving beyond byte-sequence matching to Abstract Syntax Tree (AST) analysis, we can detect capabilities in interpreted languages with the same fidelity capa currently provides for PE, ELF, and .NET binaries.

**Deliverables**

* **Core Integration**: Integrate the `tree-sitter` parser library into capa's Python architecture.
* **Backend Development**: Develop a new analysis backend that traverses the AST to extract features (function calls, variable usage, structure) rather than using regex.
* **Language Support**: Implement initial support for \*Nix/Cloud languages (focusing on Bash and Python) or Windows (PowerShell).
* **Rule Verification**: Create a set of capa rules to demonstrate and test the new capability against real-world samples.

**Required Skills**

* Strong proficiency in Python3.
* Understanding of compilers, parsers, or Abstract Syntax Trees (AST).
* Familiarity with `tree-sitter` is a major plus.
* Knowledge of scripting languages (Bash, Python, or PowerShell).
* Basic understanding of Git and malware analysis concepts.

## capa: Automated Rule Generation Agent

*size*: large, estimated 350 hours

*difficulty*: medium to hard

*mentors*: [@mike-hunhoff](https://github.com/mike-hunhoff), [@Maijin](https://github.com/Maijin)

Mandiant’s [capa](https://github.com/mandiant/capa) is the industry standard for identifying capabilities in executable files. However, the volume of new malware variants and requested rules in our issue tracker often exceeds the capacity of human analysts. Keeping the ruleset up-to-date manually is challenging against the velocity of new threat techniques.

This project aims to develop an autonomous **capa agent** that functions as a "virtual contributor." The agent will automate the heavy lifting of rule creation by parsing GitHub Issues or analyzing raw samples, generating valid YAML rules using Large Language Models (LLMs), and crucially verifying them against the official capa linter and test runner before submission. The system adheres to a Human-in-the-Loop (HITL) philosophy: the agent does the engineering and testing, but human maintainers retain control over the final merge via Pull Requests.

**Deliverables**

* **Agent Core & Triggers**: Develop the agent logic using Google ADK to handle "Reactive" triggers (parsing GitHub Issues for context/samples) and "Proactive" triggers (scanning daily feeds).
* **Generation & Grounding**: Implement the LLM integration (e.g., Gemini) to write rules, using RAG or tool use (Google Search) to verify API definitions and shell commands.
* **Validation Loop**: Build a robust self-correction loop where the agent runs the `capa` linter and test runner, parsing error logs to fix syntax errors automatically *before* a human sees the code.
* **Automated PR Workflow**: Create the logic to package verified rules and submit them as formatted Pull Requests to `mandiant/capa-rules`, including test results in the PR description.

**Required Skills**

* Strong proficiency in Python.
* Experience with LLMs, Agents, or Prompt Engineering.
* Basic understanding of malware analysis and the capa rule format (YAML).
* Familiarity with Git, GitHub Actions, or CI/CD pipelines.

## capa: Enhance Static Analysis

_size_: medium to large

_difficulty_: medium

_mentors_: [@mike-hunhoff](https://github.com/mike-hunhoff)

This initiative focuses on advancing the static analysis capabilities of capa. Key research areas include improving program analysis to effectively distinguish between library/runtime code and programmer-written logic, allowing capa and similar tools to prioritize the program's most significant components. Furthermore, integrating AI at various stages of the analysis could provide significant enhancements.

**Deliverables**:

* Assess the current performance and functionality of capa
* Brainstorm and pinpoint specific areas for potential improvement
* Develop, validate, and provide documentation for all implemented enhancements
* Stretch Goal: Explore and build AI-driven analysis to bolster results

**Skill Requirements**:

* Strong proficiency in Python programming
* Fundamental knowledge of malware analysis
* Competency with tools like IDA Pro, Ghidra, Binary Ninja, or vivisect
* Practical experience using Git and GitHub


## capa: Enhance Dynamic Analysis

_size_: medium to large

_difficulty_: medium

_mentors_: [@mike-hunhoff](https://github.com/mike-hunhoff)

This project's goal is to improve capa's dynamic analysis functionality (i.e. VMRay sandbox runs). Potential improvements include filtering out sandbox noise, improving capa's extraction and matching algorithms, enhancing existing rules, etc. Applying AI analysis could also be part of this project.

**Deliverables**:

- Review and evaluate current capa functionality and performance
- Identify and brainstorm areas of improvement
- Implement, test, and document improvements
- Stretch goal: research and develop AI analysis to enhance capa results

**Required Skills**:

- Solid Python programming skills.
- Familiarity with dynamic (and static) analysis of malware.
- (Optional: Familiarity with VMRay sandbox analysis results).
- Experience with Git and GitHub.


## FLOSS: Extract Language Specific Strings (.NET, Swift, Zig, ...)

_size_: large, estimated 350 hours

_difficulty_: medium

_mentors_: [@mr-tz](https://github.com/mr-tz)

_link_: [https://github.com/mandiant/flare-floss/issues/718](https://github.com/mandiant/flare-floss/issues/718)

Various programming languages embed the constant data, like strings, used within executables in different ways. Most tools, like strings.exe, just look for printable character sequences. This doesn't work well for files compiled from Go or Rust.

Here we propose to extend FLOSS to include a framework to extract language specific strings from executables. After identifying the language, a specific extractor can use specialized logic to pull out the strings embedded into a program by the author. When possible, the extractor should indicate library and runtime-related strings. For example, the extractor may parse debug information to recognize popular third party libraries and annotate the related strings appropriately.

Today, FLOSS automatically deobfuscates protected strings found in malware. Better categorization of its output would make its users more efficient. Extracting language-specific strings would make FLOSS more useful and manifest success as the default tool used by security analysts.

**Deliverables**

- Enhance existing Go and Rust string extraction
- Develop language identification module
  - Initial focus on .NET
  - Consider also Swift, Zig, …
- Research language string embeddings and create extractor code
  - We can share existing knowledge and code to bootstrap this
- Identify strings related to runtime and library code for targeted programming languages
- Extend standard output format and render results

**Required Skills**

- Medium knowledge of Python 3
- Basic understanding of reverse engineering (focus: Windows PE files)
- Experience with .NET or Swift (internals) is a plus, but not required
- Interest in malware analysis with focus on static analysis
- Basic understanding of Git


## FLOSS: QUANTUMSTRAND

_size_: large, estimated 350 hours

_difficulty_: medium

_mentors_: [@mr-tz](https://github.com/mr-tz)

_link_: [https://github.com/mandiant/flare-floss/issues/943](https://github.com/mandiant/flare-floss/issues/943)

Extend FLOSS to use the rendering techniques pioneered by QUANTUMSTRAND.

QUANTUMSTRAND is an experiment that augments traditional strings.exe output with context to aid in malware analysis and reverse engineering. For example, we show the structure of a file alongside its strings and mute/highlight entries based on their global prevalence, library association, expert rules, and more.

FLOSS is a tool that automatically extracts obfuscated strings from malware, rendering the human-readable data in a way that enables rapid reverse engineering.

We propose to extend FLOSS to use the techniques pioneered by QUANTUMSTRAND to highlight important information while muting common and/or analytically irrelevant noise. The project will provide an opportunity to dig into the PE, ELF, and/or Mach-O file formats, finding ways to make technical details digestible. If successful, FLOSS will continue to be the tool that malware analysts turn to when triaging unknown files.

**Deliverables**

- Research
  - Review Quantumstrand functionality
  - Evaluate most useful features for integration into FLOSS
- Identify and Propose Improvements
  - Suggest improvements for the user interface and experience
  - Review and enhance string tagging databases
  - Discuss ideas with mentors and FLOSS user community
- Implementation
  - Implement improved functionality
  - Work on a GUI to interactively display FLOSS results
- Evaluation and Knowledge Sharing
  - Test improvements and gather feedback from users
  - Write blog post about experience and project achievements

**Required Skills**

- Solid knowledge of Python 3
- Basic understanding of reverse engineering / malware analysis
- Basic understanding of Git
- Experience or interest with file formats such as PE, ELF, and/or Mach-O
- Experience or interest in user interface and/or user experience design


## GoReSym: Project in Scope

_mentors_: [@stevemk14ebr](https://github.com/stevemk14ebr)
