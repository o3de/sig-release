# O3DE 22.10.0 Feature List
**Status:** In Progress

The suggested "Top 3" items to highlight (see below for the details) are

 1. 
 2. 
 3. 

The general theme of this release is "TBD".

**sig-build**
* The Project Manager will now utilize Visual Studio 2022+ for project builds if it is installed. Going foward, Project Manager will always build on the highest version of Visual Studio detected in the local environment https://github.com/o3de/o3de/pull/11449

**sig-content**
* AssetProcessor now shows the time spent analyzing and processing assets on a per-asset and builder basis. These metrics will aid improving AssetBuilder throughput, tracking performance over time, and identify areas of asset processing that require more focus.
* AssetProcessor now supports sharing pre-processed assets via network shared drives in its new asset server cache mode. Teams can use this mode to reduce the cost of processing assets on individual machines by sharing processed files across a network.
* Improvements to the underlying hot reload framework that improve the reliability of dynamic asset reloading in the editor.
* Intermediate assets adds a powerful new asset category to the asset pipeline allowing AssetBuilders to be chained together to increase reusability and break processing into smaller parts for reduced reprocessing time.
* New 3rd Person Template. This template allows a user to start a new project with an animating model, a base character controller, a base white boxed level, camera follow from the 3rd person perspective, and base physics interactions. In addition, custom scripts are included to show user input management, trigger collider interactions, and a smooth camera follow technique. Custom source materials also show how simple materials are built.
* Gem Creation Wizard: A user can now create a gem utilizing a UX flow removing the need to manually edit the gem JSON file. Note: a user can still manually edit the gem JSON file if needed.
* Remote Projects: A user can now utilize the Project Manager to download projects from remote sources by providing a URL to that source.
* Remote Templates: A user can now utilize the Project Manager to download templates from remote sources by providing a URL to that source.
* The Project Manager now displays the engine name and version number each project is registered with. The Project Manager now displays the current engine version in the title bar.
* Script Canvas Architecture update that provides a framework to embed ScriptCanvas functionality in places other than Entity / Component system via the ScriptCanvas Component. The new architecture introduces a set of classes that handle a small part of the ScriptCanvas runtime. The highest level class is the ScriptCanvas::Executor which is now used by the ScriptCanvas::RuntimeComponent. The ScriptCanvas::Executor is also used by the new ScriptCanvasEditor::Interpreter, which is a class that allows developers to embed user access to ScriptCanvas functionality any where in the editor.
* Writing C++ Script Canvas nodes is now a lot easier! We have deprecated node generics (a set of C++ macros) in favor of using AzAutoGen to produce libraries of functions or standalone nodes. We have consolidated the autogen semantics for Script Canvas grammar nodes and nodeables. We removed the concept of Script Canvas node libraries, anytime you write a node it gets registered automatically. It is no longer necessary to manually reflect or register Script Canvas nodes.
* The O3DE editor viewport now comes with a new effect to help show both selected entities (using an outline effect) as well as helping you know what Prefab you're editing by applying a screen effect to everything not in focus.

**sig-core**
* New feature that allows users to dynamically spawn prefabs at runtime using Lua scripting.

**sig-docs-community**

**sig-graphics-audio**


**sig-network**
* Added an optional TypeValidatingSerializer which will raise an assert when serialization results in a type or variable name mismatch to aid debugging of networking serialization issues.
* The Network TargetManagement Gem adds support for tools and applications in O3DE that need a network connection to share information or to support debugging. An example of this would be the O3DE Editor connecting to Lua IDE to debug Lua scripts.
* Unified Network Spawner Pipeline - unifies the networking spawning pipeline with the non-network spawnable system. This is mostly an under-the-hood improvement but reduces the complexity of networked entity spawning.

**sig-operations**

**sig-platform**

**sig-security**

**sig-simulation**
* A series of fixes and improvements to the animation import process.
* O3DE now supports root motion extraction to making bringing in models from DCC tools such as Mixamo easier than ever before.
* The O3DE Motion Matching Gem is ready for experimental use. See https://www.o3de.org/blog/posts/blog-motionmatching/ for more details.
* O3DE now ships with support for navigation using the excellent Recast/Detour navigation library. You can now create a navmesh in your scene and see your characters path-find from one point to another.
* The ragdoll authoring experience has been completely overhauled to make setting up colliders and joint limits a breeze. We now provide joint limit auto-fitting and manipulator support for fine-grained adjustments for both colliders and joint limits.
* The way physics material assets are stored and used have been completely updated. The physics material library asset has been removed and we now support individual physics material assets, much like render materials and other assets in O3DE. This makes working with physics materials much easier and more consistent.
* The performance of the Terrain system has seen significant performance improvements for both editing and runtime/rendering.  It can now handle 16km x 16km worlds and beyond at high framerates.

**sig-testing**

**sig-ui-ux**

> Written with [StackEdit](https://stackedit.io/).
