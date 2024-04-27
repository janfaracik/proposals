# App bar

⚠️ WIP proposal for the very WIP branch https://github.com/janfaracik/jenkins/tree/projct-app-bar-revamp (this branch will be nuked before an MR is opened)

<img width="340" alt="App bar with open menu" src="https://github.com/janfaracik/proposals/assets/43062514/99b93d6e-7631-4025-b4a3-70da8e494814"> <img width="340" alt="image" src="https://github.com/janfaracik/proposals/assets/43062514/e036beb5-16e4-4a3a-bfd1-e81947cf95af">

App bars provide the page heading as well as important actions for the current page. This proposal is to move actions from the existing sidepanel to the app bar by updating the existing `Action` API.

## Changes

The existing `Action` object looks like so:

```java
String getIconFileName();
String getDisplayName();
String getUrlName();
```

The intention would be to update it to:

```java
String getIconFileName(); // Preexisting
String getDisplayName(); // Preexisting
String getUrlName(); // Now deprecated in favour of getEvent()
Group getGroup();
Event getEvent();
Semantic getSemantic();
Badge getBadge();
boolean isVisibleInContextMenu();
```

`Group` is a new field which allows developers to group their actions together if need be. There are several predefined groups, but developers can create their own if necessary - `FIRST_IN_APP_BAR, IN_APP_BAR, LAST_IN_APP_BAR, FIRST_IN_MENU, IN_MENU, LAST_IN_MENU`. Suggestions of where best to place an action would be available in the Design Library.

`Event` is a new field which dictates what happens when a user clicks an action. There are several options developers can use - `LinkEvent` (the default, defaults to the existing `urlName` field), `ConfirmationEvent` (displays a confirmation popup, e.g. for deleting projects) and lastly `JavascriptAction` (for executing arbitrary JS code, such as for building projects). A `DropdownEvent` (for displaying submenus) could be implemented in the future for complex menus.

`Semantic` is a new field which defines the _intention_ of an action by changing its appearance (see [Semantics on the Design Library](https://weekly.ci.jenkins.io/design-library/Colors/)). This can be seen in the above pictures where `Build now` and `Delete project` have set the semantic field to `BUILD` and `DESTRUCTIVE` respectively.

`Badge` is a new field which behaves like existing badge implementations, it allows developers to highlight important information, such as the number of updates available to a user.

`isVisibleInContextMenu` is a new field which dictates if the action is visible in a `model-link` dropdown (not to be confused with the app bar dropdown).

---

Actions are read via the `getTransientActions()` method on `Actionable` and converted to `JSON`, where they're then read via JS and rendered on the page. This allows us to have one consistent API across model-links, buttons and overflow menus. 

The new app bar actions replace the existing `model-link` dropdown implementation, which was previously created via a confusing method call in `side-panel.jelly` to add items to the list. Actions are now identical between the two places, reducing duplication. 

## Questions

### Why not use a new object?

Backwards compatability with the existing Actions.
