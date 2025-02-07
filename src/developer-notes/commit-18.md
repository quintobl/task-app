# Commit 18

## Add Tasks Component

In this commit, we add a new folder with a new set of files for a Tasks component. This component will eventually hold the tasks that are associated with each user. All that's being done in this commit is that the selected user's name is being outputted to the right side of the user's button.

Here's a quick explanation of what's happening here:

1. User Clicks the Button:<br>
   When the site user clicks the app-user button, the **_onSelectUser()_** method in the UserComponent gets triggered:

HTML for the UserComponent:<br>

```html
<div>
  <button (click)="onSelectUser()">
    <img [src]="imagePath" [alt]="name" />
    <span>{{ name }}</span>
  </button>
</div>
```

Component code for the UserComponent:<br>

```typescript
onSelectUser() {
  this.select.emit(this.id);  // Emits the user ID
}
```

2. Emitting the **_select_** Event:<br>
   This emits a **_select_** event from the child (UserComponent) to the parent (AppComponent), carrying the specific user ID as event data.

3. Parent Component Listens and Handles the Event:<br>
   The parent (AppComponent) is listening for the **_select_** event:

HTML for the AppComponent:<br>

```html
<app-user (select)="onSelectUser($event)"></app-user>
```

When the event is "heard," it triggers the **_onSelectUser()_** method in the AppComponent.

Component code for the AppComponent:<br>

```typescript
onSelectUser(id: string) {
  this.selectedUserId = id; // Update selected user ID
}
```

Where the **_$event_** data is the user's id.

The **_selectedUserId_** property in the AppComponent gets updated based on the ID of the user whose button was clicked.

**N.B.**

1. Added type to event emitter in the user component, i.e., the string value the emitter is emitting.
2. This commit markdown file was updated in commit 19.
