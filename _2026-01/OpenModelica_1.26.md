---
title: OpenModelica 1.26.3 and new developments
author: "Adeel Asghar, Francesco Casella, Martin Sjölund [Open Source Modelica Consortium](https://www.openmodelica.org/)"
category: "vendor"
---
Summary: 
- OpenModelica 1.26.0 was released in winter 2025, followed by a series of bug-fix releases 1.26.1, 1.26.2, and 1.26.3 which addressed some GUI issues and improved overall stability.
- A new version 4.0.0 of the OMPython interface to OpenModelica was released in October 2025, with a patch release 4.0.1 issued in April 2026.
- The next release 1.27.0 of OpenModelica is planned for May 2026.
- AI comes to OMEdit: MCP server integration

#### Main highlights of OpenModelica 1.26.3
- OMEdit now allows to **load and save** models and packages with **syntax errors** during code development.
- **Improved sizing of parameter editing dialogs** in OMEdit, for better user experience.
- OpenModelica now implements **`break` to [remove modifiers](https://specification.modelica.org/maint/3.6/inheritance-modification-and-redeclaration.html#removing-modifiers-break) and for [selective model extension](https://specification.modelica.org/maint/3.6/inheritance-modification-and-redeclaration.html#selective-model-extension)**.
- OpenModelica now implements **less restrictive rules for the use of conditional components**, as specified in the [draft of the next Modelica Language Specification](https://specification.modelica.org/master/class-predefined-types-and-declarations.html#conditional-component-declaration).
- **Improved operation of debugging features in OMEdit**: the generation of Equation Operations in the Equation-Based Debugger is now activated by default and it is also possible to activate profiling at runtime after running a model for the first time.
- Improved handling of **large result files** in OMEdit.
- Old **deprecated and poorly supported solvers were removed from the runtime** - [gbode](https://openmodelica.org/doc/OpenModelicaUsersGuide/latest/solving.html#gbode) should be used instead.
- A new solver strategy was implemented in GBODE, which drastically reduces the number of iterations of the nonlinear solver in the implicit integration methods at each stage, while preserving the same accuracy of the solution. This makes it competitive with DASSL and IDA on models with many events. See the discussion in [#14089](https://github.com/OpenModelica/OpenModelica/issues/14089), [#14022](https://github.com/OpenModelica/OpenModelica/issues/14022).
This can be activated with flags `-gbnls=internal`, `-gberr=embedded`.
- Many improvements and fixes to FMI export, in particular regarding the generation of external events upon discrete variable input changes in FMI-ME.

For more details, see the full [1.26.0 release notes](https://github.com/OpenModelica/OpenModelica/releases/tag/v1.26.0).

#### OMPython 4.0.1 released

The new 4.0.0 version of the [OMPython](https://github.com/OpenModelica/OMPython) interface to OpenModelica was released on Oct 20, 2025, with substantial improvements over the previous version , see the [release notes](https://github.com/OpenModelica/OMPython/releases/tag/v4.0.0). A patch release [4.0.1](https://github.com/OpenModelica/OMPython/releases/tag/v4.0.0) followed in April 2026.

#### Next release OpenModelica 1.27.0

The next release of OpenModelica is planned for May 2026.

#### AI comes to OMEdit: MCP server integration

We're excited to share that the upcoming release will ship with a built-in MCP (Model Context Protocol) server integrated into the OMEdit GUI.
This lets AI assistants — anything that speaks MCP, your own local agents or cloud services — work directly inside your modeling session: reading the active model, editing it, running simulations, and inspecting results, all while you watch it happen in OMEdit.

##### What the MCP server can do today

The current prototype already supports several common modeling tasks:
- Diagram and icon editing, including connections and drawing shapes.
- Listing and setting a component's parameters.
- Simulation and re-simulation — simulate a class with its default settings, or re-simulate efficiently by tweaking parameters and start-values without rebuilding the executable.
- Awareness of the GUI state — ask which model or plot is currently active, and for multimodal models fetching the content of a digram or plot as an image.
- For when other tools don't exist: reading and writing Modelica code directly.

In practice this means you can ask an assistant things like "add a resistor in parallel with R1 and re-simulate with R2 = 50 Ω" or "minimize overshoot in this PI controller" and watch the changes appear in OMEdit.

##### We want to hear from you

This is just a start, not the finished article. Before we lock down the next batch of functionality exposed via MCP, we'd really like to hear how you are thinking about combining AI with your Modelica work:

* What workflows do you want to automate or accelerate?
* What functionality would unlock a real use case for you?
* Where do you see AI fitting into teaching, debugging, library development, or industrial modeling pipelines?

##### Help shape an AI benchmark for Modelica

Alongside the MCP work, we're putting together a benchmark suite of Modelica tasks that an AI can attempt directly and that can be auto-graded. This will allow us to recommend the models that are capable of Modelica modeling, and what parts they excel in.
If you have ideas for tasks worth including — anything from "build this small model from a spec" to "diagnose why this simulation fails" to "tune these parameters to match this reference output" — Martin Sjölund would love to hear from you by email.

Your input now will directly shape what ships next.

Download OpenModelica from: [https://openmodelica.org](https://openmodelica.org)
