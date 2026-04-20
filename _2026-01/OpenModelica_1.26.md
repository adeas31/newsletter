---
title: OpenModelica 1.26.0
author: "Adeel Asghar, Francesco Casella, Martin Sjölund [Open Source Modelica Consortium](https://www.openmodelica.org/)"
category: "vendor"
---

OpenModelica 1.26.0 was released in winter 2025 and was followed by a series of bug-fix releases 1.26.1, 1.26.2, and 1.26.3 which addressed issues and improved overall stability.

#### Main highlights
- OMEdit now allows to **load and save** models and packages with **syntax errors**.
- **Improved sizing of parameter editing dialogs** in OMEdit.
- OpenModelica now allows to **use `break` to [remove modifiers](https://specification.modelica.org/maint/3.6/inheritance-modification-and-redeclaration.html#removing-modifiers-break) and for [selective model extension](https://specification.modelica.org/maint/3.6/inheritance-modification-and-redeclaration.html#selective-model-extension)**.
- OpenModelica now implements **less restrictive rules for the use of conditional components**, as specified in the [draft of the next Modelica Language Specification](https://specification.modelica.org/master/class-predefined-types-and-declarations.html#conditional-component-declaration).
- **Improved operation of debugging features in OMEdit**: the generation of Equation Operations in the Equation-Based Debugger is now activated by default and it is also possible to activate profiling at runtime after running a model for the first time.
- Improved handling of **large result files** in OMEdit.
- Old **deprecated and poorly supported solvers were removed from the runtime** - [gbode](https://openmodelica.org/doc/OpenModelicaUsersGuide/latest/solving.html#gbode) should be used instead.

#### OpenModelica Compiler (OMC)

Selective model extension was introduced in [#11381](https://github.com/OpenModelica/OpenModelica/issues/11381).

New, [less restrictive rules](https://github.com/modelica/ModelicaSpecification/pull/3556) that are now defined for conditional components in the draft version of Modelica 3.7 were implemented in [#12888](https://github.com/OpenModelica/OpenModelica/issues/12888).;
basically, it is now possible to refer to conditionally defined components outside of connect statements, as long as they are actually defined.

The new front end has been further improved with [25 issues resolved](https://github.com/OpenModelica/OpenModelica/issues?q=is%3Aissue%20milestone%3A1.26.0%20label%3ACOMP%2FOMC%2FFrontend%20state%3Aclosed%20-reason%3Anot-planned%20-reason%3Aduplicate%20).

Regarding backend work, [12 issues](https://github.com/OpenModelica/OpenModelica/issues?q=is%3Aissue%20state%3Aclosed%20milestone%3A1.26.0%20label%3A%22COMP%2FOMC%2FBackend%22%20-reason%3Anot-planned) were fixed in the currently used backend.

The work on the development of the new backend continued, with [31 issues](https://github.com/OpenModelica/OpenModelica/issues?q=is%3Aissue%20state%3Aclosed%20milestone%3A1.26.0%20label%3A%22COMP%2FOMC%2FNew%20Backend%22%20-reason%3Anot-planned%20-reason%3Aduplicate) fixed.
Recall that the new backend, which is a lot more efficient in particular when handling arrays, is still under development and experimentally available with the [`--newBackend`](https://openmodelica.org/doc/OpenModelicaUsersGuide/latest/omchelptext.html#omcflag-newbackend) compiler flag.

[13 issues](https://github.com/OpenModelica/OpenModelica/issues?q=is%3Aissue%20state%3Aclosed%20milestone%3A1.26.0%20-reason%3Anot-planned%20label%3ACOMP%2FOMC%2FCodegen) regarding code generation were also fixed.

Regarding the C runtime, a new solver strategy was implemented in GBODE, which drastically reduces the number of iterations of the nonlinear solver in the implicit integration methods at each stage,
while preserving the same accuracy of the solution; see also the discussion in [#14089](https://github.com/OpenModelica/OpenModelica/issues/14089), [#14022](https://github.com/OpenModelica/OpenModelica/issues/14022).
This can be activated with flags `-gbnls=internal`, `-gberr=embedded`; only works with single-rate at the moment, but will be extended to multi-rate integration in the next release.

Old poorly supported and deprecated solvers (see [#9191](https://github.com/OpenModelica/OpenModelica/issues/9191) were finally removed from the runtime. They are replaced by better implemented algorithm available within the [GBODE](https://openmodelica.org/doc/OpenModelicaUsersGuide/latest/solving.html#gbode) solver.

Overall [21 issues](https://github.com/OpenModelica/OpenModelica/issues?q=is%3Aissue%20milestone%3A1.26.0%20label%3ACOMP%2FSimRT%2FC%20state%3Aclosed%20-reason%3Anot-planned%20) regarding the runtime were addressed.

#### Graphical Editor OMEdit

OMEdit 1.26.0 provides several new features:
- It is now possible load and save models and packages with syntax errors. Until all errors are fixed, the code can be edited in text mode, with a direct mapping on the file system; then, it can be saved and re-loaded with the standard Modelica view, see [#13663](https://github.com/OpenModelica/OpenModelica/issues/13663).
- Much better sizing of parameter input dialogs. Lenghty comments in drop-down menus are now displayed in tooltips, avoiding the need of excessively wide parameter input windows, see [#11721](https://github.com/OpenModelica/OpenModelica/issues/11721).
- Improved operation of debugging features: the generation of Equation Operations in the Equation-Based Debugger is now activated by default and it is also possible to activate profiling at runtime after running a model for the first time.
- Loading large result files in OMEdit is now much faster and more reliable.

Many OMEdit bugs were also fixed in this release. Overall, [39 issues](https://github.com/OpenModelica/OpenModelica/issues?q=milestone%3A1.26.0%20state%3Aclosed%20label%3ACOMP%2FGUI%2FOMEdit%20-reason%3Anot-planned%20is%3Aissue%20-reason%3Aduplicate) were addressed.

#### FMI export

CMAKE FMU export is now the default option. A critical bug was resolved about changes in discrete input variables, which did not generate events in FMI ME, see #13822.
Overall, [10  issues](https://github.com/OpenModelica/OpenModelica/issues?q=milestone%3A1.26.0%20label%3ACOMP%2FFMI%20state%3Aclosed%20-reason%3Anot-planned) regarding FMI export were addressed.

#### OMPython

OMPython 4.0.0 was released on Oct 20, 2025. See the [release notes](https://github.com/OpenModelica/OMPython/releases/tag/v4.0.0).

#### Next release

The next release is planned for Spring 2026. It will include improved handling of conditional connectors, along with GUI enhancements in OMEdit such as faster editing of large models and improved modifier management. Further improvements to FMI export are also planned.

##### AI comes to OMEdit: MCP server integration

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

This is the start, not the finished article. Before we lock down the next batch of functionality exposed via MCP, we'd really like to hear how you are thinking about combining AI with your Modelica work:

* What workflows do you want to automate or accelerate?
* What functionality would unlock a real use case for you?
* Where do you see AI fitting into teaching, debugging, library development, or industrial modeling pipelines?

##### Help shape an AI benchmark for Modelica

Alongside the MCP work, we're putting together a benchmark suite of Modelica tasks that an AI can attempt directly and that can be auto-graded. This will allow us to recommend the models that are capable of Modelica modeling, and what parts they excel in.
If you have ideas for tasks worth including — anything from "build this small model from a spec" to "diagnose why this simulation fails" to "tune these parameters to match this reference output" — Martin Sjölund would love to hear from you by email.

Your input now will directly shape what ships next.

Download it from: [https://openmodelica.org](https://openmodelica.org)
