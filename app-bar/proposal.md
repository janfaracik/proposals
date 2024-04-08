# App bar

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
String getUrlName(); // Now deprecated in favour of getAction()
Group getGroup();
Action getAction(); // Action name not final
Semantic getSemantic();
Badge getBadge();
boolean isVisibleInContextMenu();
```

## Questions

### Why not use a new object?

Backwards compatability with the existing Actions.
