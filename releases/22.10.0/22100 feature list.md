# O3DE 22.10.0 Feature List

**Status:** In Progress

The suggested "Top 3" items to highlight (see below for the details) are

 1.
 2.
 3.

The general theme of this release is "TBD".

## sig-build

* The Project Manager will now utilize Visual Studio 2022+ for project builds if it is installed. Going foward, Project Manager will always build on the highest version of Visual Studio detected in the local environment https://github.com/o3de/o3de/pull/11449

## sig-content

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
* Improved visualization for the rotation manipulator in the 3D viewport (rotation segment is now displayed).

## sig-core

* New feature that allows users to dynamically spawn prefabs at runtime using Lua scripting.

## sig-docs-community

## sig-graphics-audio
* Added a new Shadow Bias flag for parallax materials, to deal with shadow acne on parallax surfaces.
* Added min/max sliders to the pass tree debug tool to support trimming the color output for increased contrast of fine details. https://github.com/o3de/o3de/pull/9292.
* Added averages to the CPU Profiler https://github.com/o3de/o3de/pull/10253.
* Made the ImGui debug tools not disable the rest of the Editor.
* Added a Tga image loader instead of using QImage to load tga images. It handles more tga file formats. https://github.com/o3de/o3de/pull/11161.
* Switched to use tile resource for streaming images for DX12 backend. https://github.com/o3de/o3de.
* Removing default image pool budget caps. https://github.com/o3de/o3de/pull/11345.
* Added new Sky Atmosphere Component. https://github.com/o3de/o3de/pull/9649.
* Added new Stars Component. https://github.com/o3de/o3de/pull/8624.
* DiffuseProbeGrid components are now in a Gem. https://github.com/o3de/o3de/pull/10899.
* RayTracing performance improvements. https://github.com/o3de/o3de/pull/8945.
* Added "Affects GI" option to Lights. https://github.com/o3de/o3de/pull/9379.
* Added the Terrain mesh to the RayTracing scene. https://github.com/o3de/o3de/pull/10207.
* Added RHI CommandList submit range validation. https://github.com/o3de/o3de/pull/10504.
* Changed FindReflectionProbes to use the Visibility system. https://github.com/o3de/o3de/pull/9174.
* RHI OpenXr support for Vulkan backend. https://github.com/o3de/o3de/pull/10170, https://github.com/o3de/o3de/pull/9664.
* Added support for a mode that forces cpu to run in lockstep with gpu. https://github.com/o3de/o3de/pull/10604.
* Material component API improvements for getting and setting properties in Lua and script canvas.
* Material component and instance editor support for editing multiple selected entities.
* Reflected many RPI and RHI shader related types to edit and behavior context to support scripting and creating tools.
* Implemented support for editing shader variant lists, undo, and redo in shader management console.
* Added a settings dialog to material editor, shader management console, and similar tools for configuring common registry settings.
* Implemented autosave feature in material editor, shader management console, and similar tools. The autosave feature can be enabled from the tool’s settings dialog. Once autosave is enabled and configured, documents will be saved after users make modifications inside material editor.
* Updated the asset system, instance database, material component, and the thumbnail system to better support processing asset changes in the background and hot reloading materials as the auto saved from the material editor.
* Added support to open files by dragging and dropping into the material editor.
* Added support for saving custom window layouts in material editor and related tools.
* Experimental preview of material canvas, a node based, visual editor, combining features from material editor and script canvas for creating new material types and shaders.



## sig-network

* Multiple improvements to the client and server connection experience, including debug text to convey the current step in connection process, debug connection status messaging in game and new ImGUI menu options in the Launchers. See screenshots at https://github.com/o3de/sig-release/pull/86
* Added an optional TypeValidatingSerializer which will raise an assert when serialization results in a type or variable name mismatch to aid debugging of networking serialization issues.
* The Network TargetManagement Gem adds support for tools and applications in O3DE that need a network connection to share information or to support debugging. An example of this would be the O3DE Editor connecting to Lua IDE to debug Lua scripts.
* Unified Network Spawner Pipeline - unifies the networking spawning pipeline with the non-network spawnable system. This is mostly an under-the-hood improvement but reduces the complexity of networked entity spawning.

## sig-operations

## sig-platform
* Update Python from version 3.7.12 to 3.10.5. This will increase the window for support and security updates for Python to 2026 ([PEP 619](https://peps.python.org/pep-0619/)) as well as brings in many language and performance improvements over Python 3.7. See the [Python Update RFC](https://github.com/o3de/sig-platform/issues/54) for further details.

## sig-security

## sig-simulation

* A series of fixes and improvements to the animation import process.
* O3DE now supports root motion extraction to making bringing in models from DCC tools such as Mixamo easier than ever before.
* The O3DE Motion Matching Gem is ready for experimental use. See https://www.o3de.org/blog/posts/blog-motionmatching/ for more details.
* O3DE now ships with support for navigation using the excellent Recast/Detour navigation library. You can now create a navmesh in your scene and see your characters path-find from one point to another.
* The ragdoll authoring experience has been completely overhauled to make setting up colliders and joint limits a breeze. We now provide joint limit auto-fitting and manipulator support for fine-grained adjustments for both colliders and joint limits.
* The way physics material assets are stored and used have been completely updated. The physics material library asset has been removed and we now support individual physics material assets, much like render materials and other assets in O3DE. This makes working with physics materials much easier and more consistent.
* The performance of the Terrain system has seen significant performance improvements for both editing and runtime/rendering.  It can now handle 16km x 16km worlds and beyond at high framerates.

## sig-testing

* Material Editor test tools support for [python-based tests](https://www.o3de.org/docs/user-guide/testing/parallel-pattern/), expanding automated testing to more parts of O3DE. This helps O3DE contributors efficiently verify and improve the behavior of the Material Editor.
* [GitHub codeowners](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners) alias hints now output during python test failure. This helps O3DE contributors immediately know who to contact for support. Customers using O3DE's test framework will also see hints if their repo contains a codeowners file.


## sig-ui-ux

> Written with [StackEdit](https://stackedit.io/).
