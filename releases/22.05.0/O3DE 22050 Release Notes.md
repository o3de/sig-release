# O3DE 22.05.0 Release Notes

O3DE 22.05.0 represents our first major release of 2022. This release has seen 1,417 submits that containing bug fixes, quality of life improvements, and feature additions. 
# Highlights for 22.05.0
* Asset Pipeline "User Defined Properties" Add support in Asset Processing to read in user defined properties (UDP) metadata from source assets. UDP can be assigned in content creation tools to store custom properties about hierarchy nodes such as mesh, light, and animation nodes etc to power asset generation workflows for O3DE. See https://docs.o3de.org/blog/posts/blog-udp/
* Character "Motion Matching Phase 2: Customized MM for a game/sim" Experimental release of the motion matching gem. Motion matching is a data-driven animation technique that synthesizes motions based on existing animation data and the current character and input contexts. An example prefab of a character which is controllable using a gamepad is provided with the gem. More details on the supported features and how things work internally can be found on the https://github.com/o3de/o3de/tree/development/Gems/MotionMatching  page.
* Atom "Gems can now inject custom passes to the render pipeline at runtime." Previously it was cumbersome for a Gem to introduce new passes to the render pipeline. Customers had to basically copy/paste the render pipeline or modify the existing assets. A new set of APIs is now available to facilitate customization of the render pipeline. https://github.com/o3de/o3de/wiki/Work-With-Passes-In-Gems. Example of Gems using these new APIs are Terrain, LyShine & TressFX.
* Atom "Simplified and improved re-usability of Material Types." Creating a new Material Type from another Material Type is a easy as referencing another *.materialtype json file and overriding the properties of interest. No need to copy/paste another Material Type anymore. See this RFC for details: o3de/sig-graphics-audio#16
* Networking "Player spawners" Provides an interface for determining what entity is spawned and where, when a user joins a session. Ownership of spawning a networked prefab now belongs to the game code that uses the Multiplayer Gem. A sample implementation of the spawner logic is provided for reference in the MultiplayerSample project. See: o3de/o3de#7060 and o3de/o3de-multiplayersample#106

# Other items of note in the 22.05.0 release
* Audio System "Improved Audio Controls Editor, including new connection properties for Audio Engines" For more information see https://github.com/o3de/o3de/pull/6480 and https://github.com/o3de/o3de/pull/6303
* Asset Pipeline "Prefabs as product of scene processing" Adds a new way to create prefabs by generating them during the asset pipeline's scene builder. 
* Asset Pipeline "Default prefab generation for scene files"	The Prefab gem will automatically create a default procedural prefab for each source scene asset (such as a STL or FBX file) if no scene manifest is discovered.
* Asset Pipeline "Enable community contribution for AssImp"	O3DE's AssImp integration now matches other 3rd party libraries for O3DE.   See https://github.com/o3de/3p-package-source/pull/75 for additional notes.
* Asset Pipeline "Product Dependency Performance Opportunity	Improvements to speed of Asset Processing." Full scan time for Automated Testing is down from ~2.5min to ~40 seconds See https://github.com/o3de/o3de/pull/6619
* Asset Pipeline	"Job Dependencies on Products"	Allows Asset Builders to provide a list of products they specifically depend on to better schedule and control create jobs flow in the Asset Processor. See https://github.com/o3de/sig-core/issues/28
* Character	"Atom Render Viewport for animation editor"	Initial release of the Atom Viewport for the animation editor. This improves performance significantly, the rendering in the animation editor is now comparable to what one would expect in-game, and the animation editor viewport is now consistent with other O3DE viewports. Note: The legacy OpenGL render viewport for the animation editor is now deprecated.
* Editor	"Generic DOM"	Core framework update to support the Document Property Editor.
* Game Objects	"Improved Script Canvas support for Spawning"	Previously, it was possible to spawn entities using Script Canvas, however, only one call to the SpawnableEntitiesManager was exposed to Script Canvas, which is the SpawnAllEntities call. This feature expands Spawnable API functionality for Script Canvas. It provides more fine-grained control over spawning workflow and spawnable lifecycle as well as better support for handling multiple prefabs.
* Game Objects	"Slice deprecation in automated testing"	The AutomatedTesting project has been converted to use prefabs for all tests (previously there were many that used the previous system, Slices). See Github issue https://github.com/o3de/o3de/issues/7006
* Physics	"Remove legacy timing/tick system"	The legacy tick/timer system has been completely removed and new timer for O3DE has been added. All systems have been updated to use the new timer. This serves as the foundation for future tick system updates and improvements. Previous smoothing logic was also removed.
* Physics	"Upgrade Physics Automated Tests"	All physics automated tests have been updated to use Prefabs instead of Slices (including PhysX, Cloth and Blast). All tests are using the new test framework (in most cases). Several are also now running in parallel.
* Prism	"Installer validation"	These tests verify that an installer build is valid. The automated tests verify that key binaries exist, that o3de.exe registers engine, create project succeeds, compile project succeeds, asset processor batch succeeds, editor runs, game launcher runs, uninstall succeeds and unregisters engine. Currently run as nightly for O3DE, though the tests are designed so anyone can plug these tests into their quality verification process. Added via https://github.com/o3de/o3de/pull/7834
* Scripting	"Revive the Mini Map"	Script Canvas now has a "mini map" feature that helps visualize and navigate graphs. Added via https://github.com/o3de/o3de/pull/6263
* Viewport "Camera	Editor View Bookmarks V1"	View Bookmarks MVP adds the ability to store local view transforms with level prefabs. It has been designed as a solid foundation to expand for all prefabs in the scene. The View Bookmark system aims to allow the user to store different view bookmarks for a root (level) prefab. These bookmarks can be stored locally (currently in the Settings Registry). In future they will be able to be shared in any prefab. More information available at  https://github.com/o3de/o3de/pull/7855 and https://github.com/o3de/o3de/pull/8400. The UX experience of the View Bookmarks MVP does not expose view bookmarks to the UI but this is planned for an upcoming release. Bookmarks can be set with Ctrl-<Function Key> and restored with Shift-<Function Key> (currently a maximum of 12 can be set per level).
* Viewport "Experimental Editor Mode Visual Feedback"	In order to make the experience of using the Viewport clearer and more intuitive, additional rendering functionality is being investigated to improve feedback and usability. Editor Mode Visual Feedback is at a very early stage and can be toggled on through the Settings Registry (`--regset=/Amazon/Preferences/EnableEditorModeFeedback=true`). Note: This feature is experimental and under active development. It is a proof of concept (POC) release and is not currently enabled by default. Please see https://github.com/o3de/o3de/pull/8235 for the initial PR and https://github.com/o3de/o3de/issues/3458 for future updates.
* Viewport "Prefabs Focus Mode Improvements"	A number of fixes and quality of life improvements have been added to Focus Mode Prefab editing. Now Ctrl-S will save the focused Prefab not the entire scene, Focus Mode breadcrumbs now have icons, the right-click context menu grouping has been improved, as well as a number of other small fixes and updates.
* Viewport	"Cursor wrap mode for manipulators was added with help from community member [Pollend](https://github.com/pollend). See [#5155](https://github.com/o3de/o3de/pull/5155) for more details. Note: This is currently an option in the Settings Registry (`--regset=/Amazon/Preferences/Editor/Manipulator/ManipulatorMouseWrapSetting=true`) and is off by default"
* Atom	"New Debug Rendering Level Component" There's a new level component that allows users to visualize and debug various aspects of the rendering, for example visualize the normals, show only diffuse or specular lighting, override certain properties for all materials in the scene, and more. 
* Atom "Pipeline Global Pass Attachment Reference" Users writing .pass files for rendering can now declare and reference attachments in a way that is global to the pipeline
* Atom	"Several usability and performance improvements for DiffuseProbeGrid"	
  * DiffuseProbeGrid Visualization - Displays individual probes and their raw irradiance values as spheres in the appropriate position in the level.
  * Scrolling DiffuseProbeGrid - Allows a DiffuseProbeGrid to be attached to the camera to apply Diffuse GI wherever the camera is located.
  * DiffuseProbeGrid NumberOfRaysPerProbe Setting - The number of rays cast by each probe in the grid can now be adjusted in the DiffuseProbeGrid properties.  This value can be set differently per-grid.
  * DiffuseProbeGrid Irradiance Query - Query the Diffuse GI at any position and direction in the levelImproved DiffuseProbeGrid blending when multiple grids overlap, and around the edges of a grid to blend with the global IBL cubemap.
* Atom	"New CubeMapCapture Component"  Captures a Diffuse or Specular convolved cubemap at any location in the level.
* Atom	"MSAA state is easier to enable/disable."	The MSAA state can now be changed in the MainRenderPipeline.azasset file by setting the MultisampleState/samples parameter.  Setting the samples to 1 will disable MSAA.
* Atom	"Several improvements to Diffuse GI and ReflectionProbe visual quality"	Several improvements to Diffuse GI and ReflectionProbe visual quality.
* White Box	"White Box support for Linux was added to O3DE with help from community member [Pollend](https://github.com/pollend). See [#4654](https://github.com/o3de/o3de/pull/5075) for more details."

# Feature Grid
 
 ## SIG-Build 

### Build Systems 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Github Pipelines | 🟢 Complete | 🟢 Complete | 🟢 Complete | 🟢 Stable | 🟢 Optimized | All  | <div>https://github.com/o3de/o3de/tree/development/.github</div> | https://www.o3de.org/docs/contributing/to-code/git-workflow/ | | |
| Jenkins Pipelines | 🟡 Active | 🟢 Complete | 🟢 Complete | 🟢 Stable | 🔵 In Progress | All  | <div>https://github.com/o3de/o3de/tree/development/scripts/build/Jenkins</div> | <div><div>https://github.com/o3de/sig-build/blob/main/AutomatedReview/JenkinsPipelineGuide.md</div></div> | | |
| Installer Builds | 🟢 Complete | 🟢 Complete | 🟢 Complete | 🟢 Stable | 🟢 Optimized | Windows Linux  | <div>https://github.com/o3de/o3de/tree/development/cmake/Platform/Windows</div><div><br></div><div><div>https://github.com/o3de/o3de/tree/development/cmake/Platform/Linux</div></div> | || | |
| Build Failure Analysis | 🟡 Active | 🟢 Complete | 🟢 Complete | 🔵 In Progress | 🔵 In Progress | All  | || <div><div>https://github.com/o3de/sig-build/blob/main/AutomatedReview/RootCauseRunbook.md</div></div> | | |
| Build Scripts | 🟡 Active | 🟢 Complete | 🟢 Complete | 🔵 In Progress | 🔵 In Progress | All  | <div><div>https://github.com/o3de/o3de/tree/development/scripts/build/Platform</div></div> | || | |
| Build Environments | 🟢 Complete | 🟢 Complete | 🟢 Complete | 🟢 Stable | 🟢 Optimized | All  | <div>https://github.com/o3de/o3de/tree/development/scripts/build/build_node/Platform</div> | || | |
| Build Metrics | 🟡 Active | 🟢 Complete | 🟢 Complete | 🔵 In Progress | 🔵 In Progress | All  | <div>https://github.com/o3de/o3de/tree/development/scripts/build</div> | || | |
| 3rd Party System | 🟡 Active | 🟢 Complete | 🟢 Complete | 🔵 In Progress | 🔵 In Progress | All  | <div>https://github.com/o3de/3p-package-source</div> | || | |
### Infrastructure 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Jenkins | 🟡 Active | 🟢 Complete | 🟢 Complete | 🔵 In Progress | 🔵 In Progress | All  | <div>https://github.com/o3de/o3de/tree/development/scripts/build/Jenkins</div> | <div>https://www.o3de.org/docs/contributing/to-code/git-workflow/</div> | | |
| Github | 🟢 Complete | 🟢 Complete | 🟢 Complete | 🟢 Stable | 🟢 Optimized | All  | <div>https://github.com/o3de/o3de/tree/development/.github</div> | || | |
| LFS | 🟢 Complete | 🟢 Complete | 🟢 Complete | 🟢 Stable | 🟢 Optimized | All  | || || | |
| License Scanning | 🟡 Active | 🟢 Complete | 🟢 Complete | 🔵 In Progress | 🔵 In Progress | All  | <div>https://github.com/o3de/o3de/tree/development/scripts/license_scanner</div> | || | |
## SIG-Content 

### Frameworks 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| AzToolsFramework | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All | || || | |
| Lua | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All | || https://www.o3de.org/docs/user-guide/scripting/lua/ | | |
| Prefabs | || || || || || || || || | |
| Qt for Python | || || || || || || || || | |
### Editor 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Asset Browser | 🟡 Active | 🔵 In-Design | ⭕ Not Required | 🟢 Stable | 🔵 In Progress | Windows Linux MacOS  | || || | |
| Framework | || || || || || || || || | |
| Localization | || || || || || || || || | |
| Undo / Redo | || || || || || || || || | |
| Asset Editor | 🔵 Backlogged | 🟠 Minimal | ⭕ Not Required | 🟢 Stable | 🔵 In Progress | Windows Linux MacOS  | || || | |
### Canvas Tools 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Graph Model | 🟡 Active | 🟠 Minimal | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | Windows Linux MacOS  | || || | |
| Graph Canvas | 🟡 Active | 🟡 Partial | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | Windows Linux MacOS  | || || | |
| Landscape Canvas | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | Windows Linux MacOS  | || || | |
### Project Manager 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Remote Projects | 🟡 Active | 🔵 In-Design | ⭕ Not Required | 🔵 In Progress | 🔵 In Progress | Windows Linux  | || || Still in early design  |
| Project versioning | 🟡 Active | 🔵 In-Design | ⭕ Not Required | 🔵 In Progress | 🔵 In Progress | Windows Linux  | || || Still in early design  |
| Template Management | 🟠 Planned | ❌ None | ⭕ Not Required | ❌ Unproven | ❌ Unsupported | Windows Linux  | || || | |
| Gem Creation Wizard | 🟠 Planned | ❌ None | ⭕ Not Required | ❌ Unproven | ❌ Unsupported | Windows Linux  | || || | |
| Remote Gems Improvements (URI vs URL) | 🟠 Planned | ❌ None | ⭕ Not Required | ❌ Unproven | ❌ Unsupported | Windows Linux  | || || | |
| Remote Gems (Initial) | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔵 In Progress | Windows Linux  | || || | |
### Scripting 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Expression Evaluation | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All | || || | |
| Script Canvas | 🟡 Active | 🟡 Partial | ⭕ Not Required | 🟠 Volatile | 🔴 Needs Testing | Windows Linux MacOS  | || https://www.o3de.org/docs/user-guide/scripting/script-canvas/ | | |
| Script Canvas Developer | 🟡 Active | 🟡 Partial | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | Windows Linux MacOS  | || || | |
| Script Events | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All | || https://www.o3de.org/docs/user-guide/scripting/script-events/ | | |
| Script Canvas Testing | 🟢 Complete | 🟡 Partial | ⭕ Not Required | 🟠 Volatile | 🟢 Optimized | Windows Linux MacOS  | || || Unit Testing framework in Script Canvas  |
| Lua Editor | 🟡 Active | 🟡 Partial | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | Windows Linux MacOS  | || https://www.o3de.org/docs/user-guide/scripting/lua/ | | |
### User Interface 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| LyShine (2D Render) | 🟡 Active | 🟢 Complete | 🟢 Complete | 🟢 Stable | 🔴 Needs Testing | Windows Linux MacOS  | || || | |
### Animation 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Animation Playback Control | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All  | || || | |
| Pose Blending | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All  | || || | |
| Animation Syncing | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All  | || || | |
| Motion Events | 🔵 Backlogged | 🟡 Partial | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | All  | || || | |
| Bone Masking | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All  | || || | |
| Motion Extraction (Root Motion) | 🟡 Active | 🟡 Partial | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All  | || || | |
| Motion Matching | 🟡 Active | 🟡 Partial | ⭕ Not Required | 🟡 Experimental | 🔵 In Progress | All  | || || | |
| Debug Rendering | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All  | || || | |
| Animation Sharing | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All  | || || | |
| Animation Compression | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All  | || || | |
| Multi-threading | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All  | || || | |
| Retargeting | 🟢 Complete | 🟡 Partial | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All  | || || There is currently no IK retargeting  |
| Inverse Kinematics (IK) | 🟢 Complete | 🟡 Partial | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All  | || || There is currently no full-body IK  |
| LOD | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All  | || || | |
| Blend Tree/State Machine | 🟢 Complete | 🟡 Partial | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All  | || || | |
| Transition Conditions | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All  | || || | |
| Wildcard Conditions | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All  | || || | |
| Debugging Tools (Anim Graph) | 🟢 Complete | 🟡 Partial | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All  | || || This is complete, but the anim graph static analyzer is still planned and on the backlog  |
| Visual Tools | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All  | || || | |
| Software Skinning (Linear, Dual-Quat) | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All  | || || | |
| GPU Skinning (Linear, Dual-Quat) | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All  | || || | |
| Morph Target/Facial Animation | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All  | || || | |
| GPU Accelerated Morphing | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All  | || || | |
| Simulated Objects/Dynamic Bones | 🟢 Complete | 🟡 Partial | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All  | || || To improve stability and simulation quality this could be ported to use PhysX  |
| Ragdoll Runtime | 🟢 Complete | 🟡 Partial | ⭕ Not Required | 🟡 Experimental | 🔵 In Progress | All  | || || | |
| Cloth Authoring | 🟢 Complete | 🟡 Partial | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All  | || || | |
| Collider Authoring Tools | 🟡 Active | 🟡 Partial | ⭕ Not Required | 🔵 In Progress | 🔵 In Progress | All  | || || | |
| Attachments | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All  | || || | |
| Skinned Attachments | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All  | || || | |
### World Building 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Terrain | 🟡 Active | 🟠 Minimal | ❌ None | 🟡 Experimental | 🟡 Needs Optimization | Windows | || || | |
| Dynamic Vegetation | 🟢 Complete | 🟢 Complete | 🟠 Partial | 🟢 Stable | 🟡 Needs Optimization | All | || || | |
### Viewport 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Manipulators | 🟡 Active | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | Windows Linux MacOS  | || || Manipulators for interacting with entities and components in the viewport  |
| Component Mode | 🟡 Active | 🟡 Partial | ⭕ Not Required | 🔵 In Progress | 🔴 Needs Testing | Windows Linux MacOS  | || || Editing mode for Components in the main viewport  |
| Viewport UI | 🟡 Active | 🟠 Minimal | ⭕ Not Required | 🔵 In Progress | 🔴 Needs Testing | Windows Linux MacOS  | || || Qt UI elements that can be dynamically added/removed from the viewport  |
| Interaction Model | 🟡 Active | 🟡 Partial | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | Windows Linux MacOS  | || || Interaction Model for working with Entities and Prefabs in the viewport  |
| Camera | 🟡 Active | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | Windows Linux MacOS  | || || CameraInput and ModularViewportCameraController for adjusting and interacting with the camera in the Editor  |
| View Bookmarks | 🟡 Active | 🟠 Minimal | ⭕ Not Required | 🟡 Experimental | 🔴 Needs Testing | Windows Linux MacOS  | || || Support for storing view transforms in the Editor  |
| Manipulator Test Framework | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | Windows Linux MacOS  | || || Provides ability to write integration tests for manipulator interactions (screen-space to world-space transformations)  |
| Visibility | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | Windows Linux MacOS  | || || Visibility system to determine entities that fall inside the editor view frustum  |
| Editor Mode Visual Feedback | 🟡 Active | 🟠 Minimal | ⭕ Not Required | 🟡 Experimental | 🔵 In Progress | Windows Linux MacOS  | || || Covers screen space effects to communicate viewport state (e.g. Selection, Focus Mode etc..)  |
### White Box Tool 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Atom Integration | 🟢 Complete | 🟡 Partial | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | All  | || || Atom rendering support for the White Box Tool  |
| Viewport Editing | 🟡 Active | 🟡 Partial | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | Windows Linux MacOS  | || || Interaction Model for White Box Tool viewport editing  |
| Triangulation | 🔵 Backlogged | ❌ None | ⭕ Not Required | ❌ Unproven | ❌ Unsupported | Windows Linux MacOS  | || || | |
| Boolean Operations | 🔵 Backlogged | ❌ None | ⭕ Not Required | ❌ Unproven | ❌ Unsupported | Windows Linux MacOS  | || || | |
| Custom UV Mapping | 🔵 Backlogged | ❌ None | ⭕ Not Required | ❌ Unproven | ❌ Unsupported | Windows Linux MacOS  | || || | |
## SIG-Core 

### Core features 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| AzCore | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All  | || || | |
| AzFramework | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All  | || || | |
| Math libraries | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All  | || || | |
| SDK Build | 🟢 Complete | 🟡 Partial | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | Windows Linux MacOS  | || || | |
| Reflection frameworks | 🟡 Active | 🟡 Partial | ⭕ Not Required | 🟢 Stable | 🟡 Needs Optimization | All  | || || | |
| Streaming system | 🟡 Active | 🟡 Partial | ⭕ Not Required | 🟢 Stable | 🔵 In Progress | All  | || || | |
| Input system | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All  | || || | |
| Logging and tracing | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟡 Needs Optimization | All  | || || | |
| || || || || || || || || || | |
| Profiling | 🟡 Active | 🟡 Partial | ⭕ Not Required | 🟠 Volatile | 🔵 In Progress | Windows  | || || | |
| Opimised standard library | 🟡 Active | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔵 In Progress | All  | || || | |
### Physics API (minimal, non-backend specific) 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Collision Filtering | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟠 Volatile | 🔴 Needs Testing | || || || | |
| Collision Filtering - Programmable Reserved Bits | 🔵 Backlogged | ❌ None | || || || || || || | |
| Joints | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | || || || | |
| Rigid Bodies | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | || || || | |
| Multiple Scenes | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟡 Experimental | 🔴 Needs Testing | || || || Need to figure out workflow.  |
| Character Controller | 🟢 Complete | 🟡 Partial | ⭕ Not Required | 🟠 Volatile | 🔴 Needs Testing | || || || Improvements in backlog/roadmap.  |
| Ragdoll | 🟢 Complete | 🟡 Partial | ⭕ Not Required | 🟠 Volatile | 🔴 Needs Testing | || || || Improvements in backlog/roadmap.  |
| Materials | 🟡 Active | 🟢 Complete | ⭕ Not Required | 🟠 Volatile | 🔴 Needs Testing | || || || Major workflow improvements under way.  |
| Shapes | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | || || || | |
| Heightfields | 🟡 Active | 🟡 Partial | ⭕ Not Required | 🟠 Volatile | 🔴 Needs Testing | || || || | |
| Wind | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟡 Experimental | 🔴 Needs Testing | || || || | |
| Scene Queries | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | || || || | |
### Nvidia PhysX Integration 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Ticking | 🔵 Backlogged | 🟡 Partial | ⭕ Not Required | 🟠 Volatile | 🔴 Needs Testing | All  | || || | |
| Rigid Body Simulation | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟡 Needs Optimization | All  | || || | |
| Continuous Collision Detection (CCD) | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | All  | || || | |
| Collision Asset Pipeline | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | All  | || || | |
| Convex Decomposition | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | All  | || || | |
| Primitive Fitting | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | All  | || || | |
| Primitive Colliders | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | All  | || || | |
| Asset Colliders | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | All  | || || | |
| Shape Colliders | 🟢 Complete | 🟡 Partial | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | All  | || || Tube and Disc not yet supported.  |
| Heightfield Colliders | 🟡 Active | 🟠 Minimal | ⭕ Not Required | 🟠 Volatile | 🟡 Needs Optimization | All  | || || | |
| Triggers | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | All  | || || Usability issue with moving static triggers.  |
| Force Regions | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | All  | || || | |
| Wind | 🔵 Backlogged | 🟡 Partial | ⭕ Not Required | 🟡 Experimental | 🔴 Needs Testing | All  | || || Global wind is currently broken with rigid bodies. Ragdolls aren't affected by wind.  |
| Materials | 🟡 Active | 🟢 Complete | 🟢 Complete | 🟠 Volatile | 🔴 Needs Testing | All  | || || Major workflow improvements under way.  |
| Collision Filtering | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | All  | || || | |
| Joints | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | All  | || || | |
| Articulations | 🟠 Planned | ❌ None | ⭕ Not Required | ❌ Unproven | 🔴 Needs Testing | All  | || || | |
| Character Controller | 🟢 Complete | 🟠 Minimal | ⭕ Not Required | 🟠 Volatile | 🔴 Needs Testing | All  | || || Multiple functional improvements planned.  |
| Ragdoll | 🟡 Active | 🟡 Partial | 🟢 Complete | 🟠 Volatile | 🔴 Needs Testing | All  | || || Improvements in backlog/roadmap.  |
| Scripting | 🟢 Complete | 🟠 Minimal | ❌ None | 🟠 Volatile | 🔴 Needs Testing | All  | || || Needs a lot of usability work.  |
| Scene Queries | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | All  | || || | |
| Multi-Scene | 🔵 Backlogged | ❌ None | ⭕ Not Required | ❌ Unproven | 🔴 Needs Testing | All  | || || Need to figure out UX to progress with this. Many components currently rely on default scene.  |
| PhysX Visual Debugger Integration | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | Windows  | || || Remote debugging not heavily tested.  |
| Debug Visualization | 🟢 Complete | 🟡 Partial | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | Windows Linux MacOS  | || || Only heavily tested on Windows. Lots of issues with z-fighting etc.  |
| Mesh Simplification | ❌ Unscheduled | || || || || || || || | |
### Cloth - NvCloth Integration 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Generic API | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | All  | || || | |
| Support for Mesh Components | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔵 In Progress | All  | || || One optimization pass performed.  |
| Support for Actor Components | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔵 In Progress | All  | || || Skinned meshes: linear and dual quaternion blending. One optimization pass performed.  |
| Mesh Simplification | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | All  | || || | |
| Simulation Constraints | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | All  | || || Motion constraints, Backstop, Tether constraints, horizontal/vertical, shearing, bending  |
| Realtime Editing | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | All  | || || | |
| Wind | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | All  | || || | |
| Actor Colliders | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | All  | || || | |
| CCD | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | All  | || || | |
| Self Collision | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | All  | || || | |
| Async Simulation | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | All  | || || | |
| Debug Visualization | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🔴 Needs Testing | All  | || || | |
| Environmental Collision | 🔵 Backlogged | ❌ None | || || || || || || | |
| Painting Tool | 🔵 Backlogged | ❌ None | || || || || || || | |
| LOD | 🔵 Backlogged | ❌ None | || || || || || || | |
| Mesh Collision | 🔵 Backlogged | ❌ None | || || || || || || | |
### Destruction - Nvidia Blast Integration 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Authoring/Pipeline | 🔵 Backlogged | 🔵 In-Design | ⭕ Not Required | 🟡 Experimental | 🔴 Needs Testing | Windows  | || || | |
| Geometry Destruction Simulation | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟡 Experimental | 🔴 Needs Testing | Windows  | || || | |
| Materials | 🟡 Active | 🟢 Complete | ⭕ Not Required | 🟡 Experimental | 🔴 Needs Testing | Windows  | || || Major workflow improvements under way.  |
| Scripting | 🟢 Complete | 🟠 Minimal | ⭕ Not Required | 🟡 Experimental | 🔴 Needs Testing | Windows  | || || | |
| Atom Integration | 🔵 Backlogged | 🟠 Minimal | ⭕ Not Required | 🟡 Experimental | 🔴 Needs Testing | Windows  | || || | |
| PhysX Integration | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟡 Experimental | 🔴 Needs Testing | Windows  | || || Blast can technically be independent from the physics backend  |
### Vehicles 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Vehicles | ❌ Unscheduled | || || || || || || || | |
### Fluids 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Fluids | ❌ Unscheduled | || || || || || || || | |
### Soft Bodies 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Soft Bodies | ❌ Unscheduled | || || || || || || || | |
## SIG-Docs-Community 

### NewSubsystem 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| New Module | || || || || || || || || | |
## SIG-Graphics-Audio 

### Features 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Deferred Fog | 🟢 Complete | 🟡 Partial | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | All  | || https://docs.o3de.org/docs/user-guide/components/reference/atom/deferred-fog/ | | |
| Tonemapping | 🟢 Complete | 🟢 Complete | 🟢 Complete | 🟢 Stable | 🟡 Needs Optimization | All  | || https://www.o3de.org/docs/atom-guide/atom-sample-viewer/graphics-feature-samples/#tonemapping | | |
| Direct Lighting / Area Lights | 🟢 Complete | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟡 Needs Optimization | All  | || https://www.o3de.org/docs/user-guide/components/reference/atom/light/ | | |
| Meshes | 🟡 Active | 🟡 Partial | 🟢 Complete | 🟢 Stable | 🟡 Needs Optimization | All  | || https://www.o3de.org/docs/atom-guide/features/#meshes | | |
| Skinned Meshes | 🟡 Active | 🟡 Partial | 🟢 Complete | 🟢 Stable | 🟡 Needs Optimization | All  | || https://www.o3de.org/docs/atom-guide/features/#meshes | | |
| Eye Adaptation | 🟢 Complete | 🟢 Complete | 🟢 Complete | 🟢 Stable | 🟡 Needs Optimization | All  | || https://www.o3de.org/docs/atom-guide/features/#lighting | | |
| Culling | 🟡 Active | 🟡 Partial | 🟢 Complete | 🔵 In Progress | 🟡 Needs Optimization | All  | || https://www.o3de.org/docs/user-guide/components/reference/atom/occlusion-culling-plane/ | | |
| HDR Pipeline | 🟢 Complete | 🟢 Complete | 🟢 Complete | 🟢 Stable | 🟡 Needs Optimization | All  | || https://www.o3de.org/docs/atom-guide/features/ | | |
| Shadows | 🟡 Active | 🟡 Partial | 🟢 Complete | 🔵 In Progress | 🟡 Needs Optimization | All  | || https://www.o3de.org/docs/user-guide/components/reference/atom/light/ | | |
| Skybox and Physical Sky | 🟢 Complete | 🟡 Partial | 🟢 Complete | 🟢 Stable | 🟡 Needs Optimization | All  | || https://www.o3de.org/docs/atom-guide/features/#lighting | | |
| SSAO | 🟢 Complete | 🟢 Complete | 🟢 Complete | 🟢 Stable | 🟢 Optimized | All  | || https://www.o3de.org/docs/atom-guide/features/#post-processing-effects-postfx | | |
| Color Grading | 🟢 Complete | 🟢 Complete | 🟢 Complete | 🟢 Stable | 🟡 Needs Optimization | All  | || https://www.o3de.org/docs/atom-guide/features/#post-processing-effects-postfx | | |
| Depth of Field | 🟢 Complete | 🟢 Complete | 🟢 Complete | 🟢 Stable | 🟡 Needs Optimization | All  | || https://www.o3de.org/docs/atom-guide/features/#post-processing-effects-postfx | | |
| PBR Materials | 🟡 Active | 🟢 Complete | 🟢 Complete | 🟢 Stable | 🟡 Needs Optimization | All  | || https://www.o3de.org/docs/atom-guide/look-dev/materials/pbr/ | | |
| Post Processing Volumes | 🟢 Complete | 🟢 Complete | 🟢 Complete | 🟢 Stable | 🟡 Needs Optimization | All  | || https://www.o3de.org/docs/atom-guide/features/#post-processing-effects-postfx | | |
| Decals | 🟡 Active | 🟢 Complete | 🟢 Complete | 🟢 Stable | 🟡 Needs Optimization | All  | || https://www.o3de.org/docs/atom-guide/features/#lighting | | |
| Screen Space Reflections | 🟢 Complete | 🟢 Complete | 🟢 Complete | 🟢 Stable | 🟡 Needs Optimization | All  | || https://www.o3de.org/docs/atom-guide/features/#post-processing-effects-postfx | | |
| Subsurface Scattering | 🟢 Complete | 🟢 Complete | 🟢 Complete | 🟢 Stable | 🟡 Needs Optimization | All  | || https://www.o3de.org/docs/atom-guide/features/#post-processing-effects-postfx | | |
| Motion Vectors | 🟢 Complete | 🟢 Complete | 🟢 Complete | 🟢 Stable | 🟢 Optimized | All  | || https://www.o3de.org/docs/atom-guide/features/#post-processing-effects-postfx | | |
| Temporal Anti-aliasing (TAA) | 🟡 Active | 🟡 Partial | 🟢 Complete | 🔵 In Progress | 🟡 Needs Optimization | All  | || https://www.o3de.org/docs/atom-guide/features/#post-processing-effects-postfx | | |
### Render Hardware Interface 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| DirectX 12 | 🟡 Active | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟡 Needs Optimization | || || https://www.o3de.org/docs/atom-guide/dev-guide/rhi/ | | |
| Vulkan | 🟡 Active | 🟢 Complete | ⭕ Not Required | 🟢 Stable | 🟡 Needs Optimization | || || https://www.o3de.org/docs/atom-guide/dev-guide/rhi/ | | |
| Metal | 🟡 Active | 🟡 Partial | ⭕ Not Required | 🟠 Volatile | 🟡 Needs Optimization | || || https://www.o3de.org/docs/atom-guide/dev-guide/rhi/ | | |
### Audio 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Wwyse Integration | 🟢 Complete | 🟡 Partial | ⭕ Not Required | 🟢 Stable | 🟢 Optimized | || || https://www.o3de.org/docs/atom-guide/dev-guide/rhi/ | | |
## SIG-Network 

### Core Networking 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Transport API | 🟢 Complete | || || || || || || || | |
| Multiple network interface support | 🟢 Complete | || || || || || || || | |
| Compression (TCP/UDP) | 🟢 Complete | || || || || || || || | |
| Metrics support | 🟢 Complete | || || || || || || || | |
| UDP Core | 🟢 Complete | || || || || || || || | |
| UDP: DTLS support | 🟢 Complete | || || || || || || || | |
| UDP: Reliable queue support | 🟢 Complete | || || || || || || || | |
| UDP: Fragmentated packet support | 🟢 Complete | || || || || || || || | |
| TCP | 🟢 Complete | || || || || || || || | |
| TCP: TLS Support | 🟢 Complete | || || || || || || || | |
| TCP: Ringbuffer support Pkg Xmit | 🟢 Complete | || || || || || || || | |
### Multiplayer 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Multiplayer component API | 🟢 Complete | || || || || || || || | |
| Local Prediction | 🟢 Complete | || || || || || || || | |
| Server Side Rollback | 🟢 Complete | || || || || || || || | |
| Play in Editor Mode | 🟡 Active | || || || || || || || | |
| Hosting/Joining a Game | 🟢 Complete | || || || || || || || | |
| Network property support | 🟢 Complete | || || || || || || || | |
| RPC support | 🟢 Complete | || || || || || || || | |
| Network Input support | 🟡 Active | || || || || || || || | |
| ScriptBind support | 🟡 Active | || || || || || || || | |
| Netbound entity support [NetBindComponent] | 🟢 Complete | || || || || || || || | |
| Entity replication support | 🟢 Complete | || || || || || || || | |
| Network Prefab Spawning | 🟡 Active | || || || || || || || | |
| Networked Animation | ❌ Unscheduled | || || || || || || || | |
| Network Audio Support | ❌ Unscheduled | || || || || || || || | |
| Network Simulation (Physics) | 🟢 Complete | || || || || || || || | |
| Quality of Service | 🟡 Active | || || || || || || || | |
| Debugging Tools | 🟡 Active | || || || || || || || | |
| Metrics | 🟡 Active | || || || || || || || | |
### AWS Cloud Services 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| HTTPS Support | 🟢 Complete | || || || || || || || | |
| Restful API Support | 🟡 Active | || || || || || || || | |
| AWS C++ SDK Support | 🟢 Complete | || || || || || || || | |
| Client Side Ident & Auth | 🟡 Active | || || || || || || || | |
| Runtime Metrics | 🟡 Active | || || || || || || || | |
| Amazon GameLift Support | 🟡 Active | || || || || || || || | |
### Microsoft Azure Cloud Services 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Core services | ❌ Unscheduled | || || || || || || || | |
## SIG-Operations 

### NewSubsystem 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| New Module | || || || || || || || || | |
## SIG-Platform 

### Platform Abstraction Layer 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| PAL CMake | 🟡 Active | 🟡 Partial | || || || || || || | |
| PAL Tools/Editor/AP | 🟡 Active | 🟡 Partial | || || || || || || | |
| || || || || || || || || || | |
### Platform Configure (Engine Centric) 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Windows | 🟢 Complete | 🟢 Complete | || || || || || || | |
| Mac | 🟢 Complete | 🟢 Complete | || || || || || || | |
| Android | 🟢 Complete | 🟢 Complete | || || || || || || | |
| Linux | 🟢 Complete | 🟢 Complete | || || || || || || | |
| Jasper | 🟢 Complete | 🟢 Complete | || || || || || || | |
| Paris | 🟢 Complete | 🟢 Complete | || || || || || || | |
| Salem | 🟢 Complete | 🟢 Complete | || || || || || || | |
| Provo | 🟢 Complete | 🟢 Complete | || || || || || || | |
| || || || || || || || || || | |
### Platform Build (Engine Centric) 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Windows | 🟢 Complete | 🟢 Complete | || || || || || || | |
| Mac | 🟢 Complete | 🟢 Complete | || || || || || || | |
| Android | 🟢 Complete | 🟢 Complete | || || || || || || | |
| Linux | 🟢 Complete | 🟢 Complete | || || || || || || | |
| Jasper | 🟢 Complete | 🟢 Complete | || || || || || || | |
| Paris | 🟢 Complete | 🟢 Complete | || || || || || || | |
| Salem | 🟢 Complete | 🟢 Complete | || || || || || || | |
| Provo | 🟢 Complete | 🟢 Complete | || || || || || || | |
| || || || || || || || || || | |
### Platform Configure (Project Centric) 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Windows | 🟡 Active | 🟡 Partial | || || || || || || | |
| Mac | 🟡 Active | 🟡 Partial | || || || || || || | |
| Android | 🟡 Active | 🟡 Partial | || || || || || || | |
| Linux | 🟡 Active | 🟡 Partial | || || || || || || | |
| Jasper | 🟡 Active | 🟡 Partial | || || || || || || | |
| Paris | 🟡 Active | 🟡 Partial | || || || || || || | |
| Salem | 🟡 Active | 🟡 Partial | || || || || || || | |
| Provo | 🟡 Active | 🟡 Partial | || || || || || || | |
### Platform Build (Project Centric) 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Windows | 🟡 Active | 🟡 Partial | || || || || || || | |
| Mac | 🟡 Active | 🟡 Partial | || || || || || || | |
| Android | 🟡 Active | 🟡 Partial | || || || || || || | |
| Linux | 🟡 Active | 🟡 Partial | || || || || || || | |
| Jasper | 🟡 Active | 🟡 Partial | || || || || || || | |
| Paris | 🟡 Active | 🟡 Partial | || || || || || || | |
| Salem | 🟡 Active | 🟡 Partial | || || || || || || | |
| Provo | 🟡 Active | 🟡 Partial | || || || || || || | |
### O3DE Object Externalization 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Project | 🟢 Complete | 🟢 Complete | || || || || || || | |
| Gem | 🟢 Complete | 🟢 Complete | || || || || || || | |
| Template | 🟢 Complete | 🟢 Complete | || || || || || || | |
| Restricted | 🟡 Active | 🟡 Partial | || || || || || || | |
| Repo | 🟡 Active | 🔵 In-Design | || || || || || || | |
| || || || || || || || || || | |
### Language/Localization 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Editor | 🟢 Complete | 🟢 Complete | || || || || || || | |
| Runtime | 🟡 Active | 🟡 Partial | || || || || || || | |
| || || || || || || || || || | |
### Packaging 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Windows | 🟢 Complete | 🟢 Complete | || || || || || || | |
| Mac | 🟢 Complete | 🟢 Complete | || || || || || || | |
| Android | 🟢 Complete | 🟢 Complete | || || || || || || | |
| Linux | 🟢 Complete | 🟢 Complete | || || || || || || | |
| Jasper | 🟡 Active | 🟡 Partial | || || || || || || | |
| Paris | 🟡 Active | 🟠 Minimal | || || || || || || | |
| Salem | 🟡 Active | 🟠 Minimal | || || || || || || | |
| Provo | 🟡 Active | 🟠 Minimal | || || || || || || | |
## SIG-Release 

### NewSubsystem 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| New Module | || || || || || || || || | |
## SIG-Security 

### NewSubsystem 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| New Module | || || || || || || || || | |
## SIG-Security-Reports 

### NewSubsystem 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| New Module | || || || || || || || || | |
## SIG-Testing 

### AutomatedReview 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Early Warning | 🟢 Complete | 🟢 Complete | 🟢 Complete | 🟢 Stable | 🟢 Optimized | || https://github.com/o3de/sig-testing | https://www.o3de.org/docs/user-guide/testing/ | | |
| CTest | 🟢 Complete | 🟢 Complete | 🟢 Complete | 🟢 Stable | 🟢 Optimized | || https://github.com/o3de/sig-testing | https://www.o3de.org/docs/user-guide/testing/ | | |
| GoogleTest | 🟢 Complete | 🟢 Complete | 🟢 Complete | 🟢 Stable | 🟢 Optimized | || https://github.com/o3de/sig-testing | https://www.o3de.org/docs/user-guide/testing/ | | |
| GoogleBenchmark | 🟢 Complete | 🟢 Complete | 🟢 Complete | 🟢 Stable | 🟢 Optimized | || https://github.com/o3de/sig-testing | https://www.o3de.org/docs/user-guide/testing/ | | |
| PyTest | 🟢 Complete | 🟢 Complete | 🟢 Complete | 🟢 Stable | 🟢 Optimized | || https://github.com/o3de/sig-testing | https://www.o3de.org/docs/user-guide/testing/ | | |
| O3DE EditorTest | 🟢 Complete | 🟢 Complete | 🟢 Complete | 🟢 Stable | 🟢 Optimized | || https://github.com/o3de/sig-testing | https://www.o3de.org/docs/user-guide/testing/ | | |
| Test Metrics | 🟢 Complete | 🟢 Complete | 🟢 Complete | 🟢 Stable | 🟢 Optimized | || https://github.com/o3de/sig-testing | https://www.o3de.org/docs/user-guide/testing/ | | |
## SIG-UI-UX 

### UI Components 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Breadcrumb navigation | 🟢 Complete | 🟢 Complete | || || || || || <div>https://www.o3de.org/docs/tools-ui/component-library/uidev-breadcrumbs-component/</div> | | |
| Browse Edit | 🟢 Complete | 🟢 Complete | || || || || || <div>https://www.o3de.org/docs/tools-ui/component-library/uidev-browse-edit-component/</div> | | |
| Button | 🟢 Complete | 🟢 Complete | || || || || || <div>https://www.o3de.org/docs/tools-ui/component-library/uidev-button-component/</div> | | |
| Card | 🟠 Planned | 🟡 Partial | || || || || || <div>https://www.o3de.org/docs/tools-ui/component-library/uidev-card-widget/</div> | | |
| Checkbox | 🟢 Complete | 🟢 Complete | || || || || || <div>https://www.o3de.org/docs/tools-ui/component-library/uidev-checkbox-component/</div> | | |
| Combobox | 🟢 Complete | 🟢 Complete | || || || || || <div>https://www.o3de.org/docs/tools-ui/component-library/uidev-combobox-component/</div> | | |
| Context menu | 🟢 Complete | 🟢 Complete | || || || || || <div>https://www.o3de.org/docs/tools-ui/component-library/uidev-context-menu-component/</div> | | |
| Filtered search | 🟠 Planned | 🟡 Partial | || || || || || <div>https://www.o3de.org/docs/tools-ui/component-library/uidev-filtered-search-component/</div> | | |
| Line edit | 🟢 Complete | 🟢 Complete | || || || || || <div>https://www.o3de.org/docs/tools-ui/component-library/uidev-line-edit-component/</div> | | |
| Progress indicators | 🟢 Complete | 🟢 Complete | || || || || || <div>https://www.o3de.org/docs/tools-ui/component-library/uidev-progress-indicators-component/</div> | | |
| Radio button | 🟢 Complete | 🟢 Complete | || || || || || <div>https://www.o3de.org/docs/tools-ui/component-library/uidev-radio-button-component/</div> | | |
| Reflected property editor | 🟠 Planned | 🟡 Partial | || || || || || <div>https://www.o3de.org/docs/tools-ui/component-library/uidev-reflected-property-editor-component/</div> | | |
| Scrollbar | 🟢 Complete | 🟢 Complete | || || || || || <div>https://www.o3de.org/docs/tools-ui/component-library/uidev-scrollbar-component/</div> | | |
| Slider | 🟢 Complete | 🟢 Complete | || || || || || <div>https://www.o3de.org/docs/tools-ui/component-library/uidev-sliders-component/</div> | | |
| Spinbox | 🟢 Complete | 🟢 Complete | || || || || || <div>https://www.o3de.org/docs/tools-ui/component-library/uidev-spinbox-component/</div> | | |
| Styled dock | 🟢 Complete | 🟢 Complete | || || || || || <div>https://www.o3de.org/docs/tools-ui/component-library/uidev-styled-dock-component/</div> | | |
| Tab | 🟠 Planned | 🟡 Partial | || || || || || <div>https://www.o3de.org/docs/tools-ui/component-library/uidev-tab-component/</div> | | |
| Toggle switch | 🟢 Complete | 🟢 Complete | || || || || || <div>https://www.o3de.org/docs/tools-ui/component-library/uidev-toggle-switch-component/</div> | | |
| Tree view | 🟢 Complete | 🟢 Complete | || || || || || <div><span style="font-size: 0.875rem; letter-spacing: 0.2px; color: var(--jexcel_content_color);">https://www.o3de.org/docs/tools-ui/component-library/uidev-tree-view-component/</span></div> | | |
| Array | ❌ Unscheduled | ❌ None | || || || || || <br> | | |
| Table view | 🟢 Complete | 🟢 Complete | || || || || || <div>https://www.o3de.org/docs/tools-ui/component-library/uidev-table-view-component/</div> | | |
### UX Patterns 
| Module | Feature | Functional | Content | Code/API | Performance | Platform | Github Link | Doc Link | Notes |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Component Card | 🟡 Active | 🟡 Partial | || || || || || <div>https://www.o3de.org/docs/tools-ui/ux-patterns/component-card/overview/</div> | | |
| Error handling | 🟠 Planned | 🟠 Minimal | || || || || || <div>https://www.o3de.org/docs/tools-ui/ux-patterns/error/overview/</div> | | |
| Hotkey management | 🔵 Backlogged | 🟠 Minimal | || || || || || || | |
| UI/UX Responsiveness standard | 🔵 Backlogged | ❌ None | || || || || || || | |
| Viewport interaction | 🔵 Backlogged | 🔵 In-Design | || || || || || || | |
| || || || || || || || || || | |


# Known Issues

