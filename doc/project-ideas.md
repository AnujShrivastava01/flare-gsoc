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


## capa: enhance static analysis

_size_: medium to large

_difficulty_: medium

_mentors_: [@mike-hunhoff](https://github.com/mike-hunhoff)

This initiative focuses on advancing the static analysis capabilities of capa. Key research areas include improving program analysis to effectively distinguish between library/runtime code and programmer-written logic, allowing capa and similar tools to prioritize the program's most significant components. Furthermore, integrating AI at various stages of the analysis could provide significant enhancements.

**Deliverables**:

- Assess the current performance and functionality of capa
* Brainstorm and pinpoint specific areas for potential improvement
* Develop, validate, and provide documentation for all implemented enhancements
* Stretch Goal: Explore and build AI-driven analysis to bolster results

**Skill Requirements**:

* Strong proficiency in Python programming
* Fundamental knowledge of malware analysis
* Competency with tools like IDA Pro, Ghidra, Binary Ninja, or vivisect
* Practical experience using Git and GitHub


## capa: enhance dynamic analysis

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


## FLOSS: extract language specific strings (.NET, Swift, Zig, ...)

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


## GoReSym: Recover Golang Structure Tags and Interface Methods in GoReSym

**Mentors:** @stevemk14ebr, @jaeyoungkimG  
**Difficulty:** Easy to Medium  
**Project Repo:** [https://github.com/mandiant/GoReSym](https://github.com/mandiant/GoReSym)  

### Description
GoReSym is a Go symbol parser that extracts program metadata, function information, and embedded structures/types from Go binaries. It is widely used by reverse engineers to analyze stripped Go binaries and reconstruct type definitions.

Currently, GoReSym recovers structure fields but fails to extract **structure tags** (e.g., `` `json:"name"` ``) and **interface method names**. These tags are critical for understanding how data is serialized (JSON, XML) and how the application interacts with databases or external APIs. The goal of this project is to implement the parsing logic required to recover these missing metadata fields and include them in GoReSym's JSON output.

### Task Details
The contributor will need to:
1.  **Analyze Existing Parsers:** Study how GoReSym currently extracts `StructField` information by looking at the code adapted from the Go runtime (specifically `objfile` and type parsing logic).
2.  **Implement Tag Extraction:** Add logic to read the tag string associated with struct fields. This involves understanding the internal memory layout of Go types.
3.  **Implement Method Name Extraction:** Add logic to recover method names for Interface types.
4.  **Update Output:** Modify the JSON serialization to include these new fields.
5.  **Testing:** specific test cases involving structs with various tags and interfaces to ensure accurate recovery across different Go versions.

### Recommended Skills
*   **Go (Golang):** Intermediate knowledge.
*   **Reverse Engineering:** Basic understanding of binary formats (PE, ELF, Mach-O) and memory layouts.
*   **Go Internals:** Familiarity with how Go stores type metadata (`moduledata`, `pclntab`) is helpful but can be learned during the project.

### Resources
*   **Issue Discussion:** [GoReSym Issue #37](https://github.com/mandiant/GoReSym/issues/37) (contains references to similar implementations).
*   **Reference Implementation:** [goretk/gore type parsing](https://github.com/goretk/gore/blob/3009b3909f08fa910e5a93d893bb66117f3628f9/type2.go#L149)
