# Commit 15

## Managing State and Changing Data

Data or variables that are managed within a single component is an example of **_Local Component State_**. Examples include:

1. Form inputs
2. Temporary flags
3. Counters

Changes in this state typically trigger updates to the component's view:

```typescript
import { Component } from "@angular/core";

@Component({
  selector: "app-counter",
  template: `
    <p>Counter: {{ counter }}</p>
    <button (click)="increment()">Increment</button>
  `,
})
export class CounterComponent {
  counter = 0;

  increment() {
    this.counter++;
  }
}
```

### Local Component State

The **_counter_** variable above is part of the local component's state. When the counter changes, the view changes.

### Shared State

There is also such a thing as **_Shared State_**, which is data that is shared among different components, usually with services that are injected into a component via dependence injection. It's useful when different parts of an application need access to the same data.

### Application State

This is global state that might include user preferences, session information, or other critical data needed across the entire application.

## Why Manage State

Proper state management ensures:

1. Consistency: The UI always reflects the latest state.
2. Separation of Concerns: Components focus on UI rendering, while services handle logic and state.
3. Maintainability: Clean and structured state makes applications easier to scale.

## Example Scenario: Cart in an E-commerce App

1. Local State: Managing whether a dropdown is open or closed.
2. Shared State: Cart items shared between a product list and a checkout component.
3. Application State: User authentication status.

## Angular Change Detection

Change Detection is a mechanism in Angular that ensures the view updates whenever the underlying state of an application changes. Angular runs a change detection cycle whenever events such as user actions, HTTP responses, or timer events occur. During this cycle:

1. The Angular change detection mechanism traverses the component tree, checking for changes in data bindings.
2. If changes are detected, Angular updates the view (DOM).

### Zone.js

In the "beforetimes" (before Angular v16), change detection was done via a mechanism in the zone.js file. Angular uses zone.js "under the hood." Zone.js notifies Angular with any user events, expired timers, etc, and when any of these events occur, Angular checks all the components within a zone to see if anything needs to be updated in any of those components and their associated templates.

### Signals

Signals are a new way (since Angular v16) of managing state in an application. They provide a more straightforward, efficient, and predictable way to handle reactivity in comparison to traditional Angular features like **_EventEmitters_**, **_RxJS_**, and **_ChangeDetection_**.

A signal is like a box or wrapper around a property/object/nested object that holds the value of that thing and notifies any listeners in the application when the value has changed. Here is an example of signals in action:

```typescript
import { signal } from "@angular/core";

const counter = signal(0);

console.log(counter()); // Output: 0
counter.set(1);
console.log(counter()); // Output: 1
```

In the above code snippet, a signal is used to hold the value of the counter variable. We use the **_set()_** method on the signal, which changes the value of the counter property. We can also use **_computed()_** on a signal, which is a derived value that updates automatically when the dependent signal value changes, as seen below:

```typescript
import { computed, signal } from "@angular/core";

const count = signal(2);
const doubleCount = computed(() => count() * 2);

console.log(doubleCount()); // Output: 4
count.set(3);
console.log(doubleCount()); // Output: 6
```

We can also use **_effect()_**, which executes a function whenever any dependent signal changes, as in the below code snippet:

```typescript
import { effect, signal } from "@angular/core";

const name = signal("Alice");

effect(() => {
  console.log(`Hello, ${name()}`);
});

name.set("Bob"); // Output: Hello, Bob
```

Signals are used to reduce unnecessary overhead and cost when it comes to change detection. It used to be that if a property or object's value changed, then Angular would search each component and template in a zone to check if anything that references the property or object needs to change. In the new way, with signals, only components and templates dependent on a signal will update, which reduces unnecessary rendering. Signals also eliminate some of the complexity introduced by observables and zones.

One quick note: Signals are executed, so we need to include parentheses after the signal in the component and template, like so:

```typescript
const count = signal(2);
```

### Tips for Efficient State and Change Detection

1. Use Signals: Angular v16 introduces Signals for fine-grained reactivity.
2. Avoid Mutating State: Always create new references for state objects ({ ...obj, newProp: value }).
3. OnPush Strategy: Use it for performance-sensitive components.
4. Detach Change Detection: For cases where updates are manually controlled using ChangeDetectorRef.detach().

## Using Signals for the Task App

### UserComponent Component

```typescript
import { Component, computed, signal } from "@angular/core";
import { DUMMY_USERS } from "../dummy-users";

const randomIndex = Math.floor(Math.random() * DUMMY_USERS.length);

@Component({
  selector: "app-user",
  standalone: true,
  imports: [],
  templateUrl: "./user.component.html",
  styleUrl: "./user.component.css",
})
export class UserComponent {
  selectedUser = signal(DUMMY_USERS[randomIndex]);
  imagePath = computed(() => "assets/users/" + this.selectedUser().avatar);

  onSelectUser() {
    const randomIndex = Math.floor(Math.random() * DUMMY_USERS.length);
    this.selectedUser.set(DUMMY_USERS[randomIndex]);
  }
}
```

### UserComponent Template

```html
<div>
  <button (click)="onSelectUser()">
    <img [src]="imagePath()" [alt]="selectedUser().name" />
    <span>{{ selectedUser().name }}</span>
  </button>
</div>
```

Notice that anytime a signal is used, we must execute it like a function, with parentheses at the end, even if the thing we're adding parentheses to is a property.
