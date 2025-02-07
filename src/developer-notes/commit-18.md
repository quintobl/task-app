# Commit 18

## Add Tasks Component

In this commit, we add a new folder with a new set of files for a Tasks component. This component will eventually hold the tasks that are associated with each user. All that's being done in this commit is that the selected user's name is being outputted to the right side of the user's button.

Here's a quick explanation of what's happening here:

1. User Clicks the Button:
   When the site user clicks the app-user button, the **_onSelectUser()_** method in the UserComponent gets triggered:

   ```typescript
   onSelectUser() {
     this.select.emit(this.id);  // Emits the user ID
   }
   ```

2. Emitting the **_select_** Event:
   This emits a **_select_** event from the child (UserComponent) to the parent (AppComponent), carrying the specific user ID as event data.

3. Parent Component Listens and Handles the Event:
   The parent (AppComponent) is listening for the **_select_** event:

   ```html
   <app-user (select)="onSelectUser($event)"></app-user>
   ```

When the event is "heard," it triggers the **_onSelectUser($event)_** method in the AppComponent.

```typescript
onSelectUser(id: string) {
  this.selectedUserId = id; // Update selected user ID
}
```

Where the **_$event_** data is the user's id.

4. Updating the **_selectedUserId_** Property:<br>
   The **_selectedUserId_** property gets updated based on the ID of the user whose button was clicked.

**Note** Added type to event emitter in the user component, i.e., the string value the emitter is emitting.
