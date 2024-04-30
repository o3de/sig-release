The **Open 3D Engine (O3DE)** 23.10.3 This release is a point release (primarily bug fixes) for the 23.10 major release. This point release focuses on bug fixes for the Document Property Editor (DPE), crashes across Windows and Linux, optimization for decals, minor improvements for editor startup times, address control input inconsistencies, quality of life improvements for the Asset Browser, and resolves some build issues with clang versions.


# PR's for point release

# o3de/o3de
* https://github.com/o3de/o3de/pull/17388 - cherry pick DPE fixes from development #17525
  * handle dynamic container elements (o3de#17411)
  * re-enable recycling, esp for prefab override labels (o3de#17343)
  * fix element add for containers with DynamicElementType (o3de#17441)
  * Handle ClassElement::FLG_POINTER in DPE-based Inspector (o3de#17457)
  * Speed up DPE's color picker handling by 2-3x and disallow redundant updates (#17493)
  * added recycling capability to several common handlers (o3de#17512)

* https://github.com/o3de/o3de/pull/17545 - Cherry-pick DPE fixes to point-release 23.10.3 #17545
  * Add simple assert
  * Revert previous assert 
  * Fix GrowTextEdit sizing and sizeHint implementation to correctly work with the DPE's size detection code
  * Add static variables so it's easier to track and edit min/max sizes. 
  * WIP - DPE Layout classes rewrite 
  * Minor refactoring 
  * Remove repeated code, remove TODOs 
  * Remove debug prints 
  * Update Code/Framework/AzToolsFramework/AzToolsFramework/UI/DocumentPropertyEditor/ContainerActionButtonHandler.cpp
  * Update Code/Framework/AzToolsFramework/AzToolsFramework/UI/DocumentPropertyEditor/DocumentPropertyEditor.cpp
  * Detect whether the Property Editor is being instanced in the Editor or in a Unit Test and handle deletion differently
  * Fix int conversion warnings.
    
* https://github.com/o3de/o3de/pull/17670 - Ensure Collider widgets correctly signal when they're being edited #17670
* https://github.com/o3de/o3de/pull/17712 - Fix the proportions of the Editor splashscreen for 23.10.3
* https://github.com/o3de/o3de/pull/17828 - Cherry pick PR #17819 Fix decal material loading when asset is already loaded
* https://github.com/o3de/o3de/pull/17817 - Cherry-pick PR #17568
  * Fixes the bug causing asset browser to be unable to delete/move/etc. (#17568)
  * Fixes Asset Browser cannot delete asset #15671
  * Adds missing functionality from the Linux ProcessWatcher to indicate the difference between a different problem launching program, and the program not being found.
  * Fixes the workflow of the Move/Delete/Rename operations in the Asset Browser to properly return the appropriate error when Source Control is not properly configured.
  * Adds a toggle for source control notification in AP, so that if you toggle the Editor to not use Source Control, the AP will not either.
  * Uses the same setting in AP as the Editor, to determine whether Source Control should be used or not, and sets it to false by default, just like the Editor.

* https://github.com/o3de/o3de/pull/17816 - Cherry-pick pull request #17424
  * Fix issue #14877 - mouse wheel being intepreted as x-axis movement on linux (#17424)
  * Fix issue Linux: mouse_delta_x listens to the mouse wheel input #14877 - mouse wheel being intepreted as x-axis movement on Linux
  * Fixed existing tests and added a new test case
 
* https://github.com/o3de/o3de/pull/17815 - cherry-pick from dev to point-release, PR #17697 - A few small improvements for the editor startup time
* https://github.com/o3de/o3de/pull/17814 - Fixes Input handler is handling mouse_delta inputs inconsistently
* https://github.com/o3de/o3de/pull/17814 - cherry-pick from development to Point Release of PR #17672- Fixes input handler is handling mouse_delta inputs inconsistently
* https://github.com/o3de/o3de/pull/17813 - cherry-pick crashfix part of PR 17664
* https://github.com/o3de/o3de/pull/17812 - cherry-pick from development to point-release/23103 PR #17594 Add missing file from installer
* https://github.com/o3de/o3de/pull/17811 - CHERRY-PICK from dev to point-release/23103 PR #17526 - Startup time improvements on Linux
* https://github.com/o3de/o3de/pull/17809 - Cherrypick PR 17464 from development to point release #17809 - Fixes the ALT key being held down after alt-tabbing
* https://github.com/o3de/o3de/pull/17808 - Cherry-pick PR17420 from dev to point-release #17808 - This fixes a potential memory stomp issue, Potential fix for ScriptCanvasDeveloper crash
* https://github.com/o3de/o3de/pull/17799 - Allow direct selection of entities inside prefabs in Entity Pick mode #17799
* https://github.com/o3de/o3de/pull/17798 - Cherry-pick - Allow for Entity creation and Prefab instantiation in place via viewport interactions. #17798
* https://github.com/o3de/o3de/pull/17797 - Prefabs - Select the container of a prefab after instantiation
* https://github.com/o3de/o3de/pull/17787 - Cherry Pick fix linux editor first time crash #17787
* https://github.com/o3de/o3de/pull/17786 - Cherry pick fix for python bindings on Linux for methods that return size_t #17786
* https://github.com/o3de/o3de/pull/17785 - Cherry pick fix for bootstrap.py files that are invoked from non-Editor tools #17785
* https://github.com/o3de/o3de/pull/17784 - Cherry Pick Fix logic for determining the file extension for shader files #17784
* https://github.com/o3de/o3de/pull/17780 - Cherry-pick clang 17 compiler errors fix from development #17780
* https://github.com/o3de/o3de/pull/17771 - Cherrypick my linux/clang compile fixes from dev to point release #17771
* https://github.com/o3de/o3de/pull/17763 - Cherry-pick fix to ChangeValidate functions not triggering in Property Editors

# o3de/o3de-extras

* https://github.com/o3de/o3de-extras/pull/690 - This PR collects changes that should be integrated into the next point-release.
  * updates in the documentation that are common for main and development [663](https://github.com/o3de/o3de-extras/pull/633)
  * fix for rclcpp SIGINT and SIGTERM handling (it was not handled in 2310.2) [636](https://github.com/o3de/o3de-extras/pull/636)
  * fix in Twist Robot Control that allows to move the robot more smoothly [645](https://github.com/o3de/o3de-extras/pull/645)
  * fix of the ROS2 Python tests that did not work in 2310.2 [663](https://github.com/o3de/o3de-extras/pull/663)
  * fix in scale calculation applied to a sensor (sensors were not placed correctly when scaled)
  * fix of the multiplayer template which did not work in 2310.2
  * removal of the unused texture files that were duplicated along different Gems [682](https://github.com/o3de/o3de-extras/pull/682)
 * Enable compilation of WarehouseAutomationGem with a project-centric approach. [665](https://github.com/o3de/o3de-extras/pull/665)
