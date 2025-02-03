# Commit 1

This commit included a README.md file with a brief description of the course for which this repo was created.

# Commit 2

This commit includes all the starter files provided by the instructor. These files include the configuration files that are TypeScript-specific, the Angular and Package JSON files, the main.ts file, the global style sheet, an assets folder for storing images, and the app component and associated style sheet and template files.

## What is Angular?

Angular is a front-end JavaScript framework. It uses Typescript, which is a superset of JavaScript, which means that all valid JavaScript code is also valid TypeScript code. Typescript offers static typing, which allows the developer to define types of variables (like in a language such as C#). TypeScript compiles down to plain JavaScript.

## Configuration Files

The following are the configuration files that are included in the application.

1. tsconfig.app.json
2. tsconfig.json
3. tsconfig.spec.json

These are TypeScript-specific configuration files that control how the TypeScript is compiled down to JavaScript. They also contain configurations for how strict TypeScript is (i.e., how much the application will 'complain' if you, e.g., assign a property the wrong type).

4. package-lock.json
5. package.json

These files contain all the dependencies that the app relies on.

6. angular.json

This file contains extra configuration settings for the CLI and Angular-provided tools in general.

7. .editorconfig
8. .gitignore

The .editorconfig file contains rules for the code editor regarding how the code should be formatted, etc.
The .gitignore file is used to hide certain files from a git repo if the developer is using git for version control.

## src Folder

This folder contains the application's:

1. Components
2. Templates
3. Style sheets
4. Spec files
5. index.html
6. style.css
7. main.ts

These components, templates, style sheets, and spec files are described below. The style.css file is the global style sheet. The index.html is the root html file that will be loaded when a user visits the website. The main.ts file is the first code file to be executed when the Angular application loads in the browser.

## Components, Templates, CSS Files, and Spec Files

### Components

Components are the building blocks of the user interface. They do the following:

1. They define views and manage logic for a specific part of the UI.
2. They provide encapsulation, data binding, and are reusable throughout the app.
3. They are decorated with the keyword "Component."
4. They contain either a templateUrl or template key in the Component decorator, which either contains inline html or points to a separate html file.
5. They contain either a styleUrls array or style key, which either contain inline styling or points to a separate style sheet.
6. They contain a class name.
7. They contain all the methods and properties of the application.
8. They contain a selector, which is the name of the component that will be used as a custom HTML tag (i.e., wherever the selector is used as a custom HTML tag, the markup in the associated template will show on the UI). An example is below:

```typescript
import { Component } from "@angular/core";

@Component({
  selector: "app-root",
  standalone: true,
  imports: [],
  templateUrl: "./app.component.html",
  styleUrl: "./app.component.css",
})
export class AppComponent {}
```

The component decorator adds metadata to the component, and the component is imported from the Angular core library. The decorator converts the class AppComponent to an Angular component.

### Templates

A template is the HTML file that is associated with the component. Data can be shared to and from the template and component. It contains all the HTML that will be rendered on the UI. An example is below:

```html
<p>{{ message }}</p>
<button (click)="changeMessage()">Click me!</button>
```

### CSS Files

CSS files are where the CSS for a component is stored, so they contain the styling that is specific to the component they are associated with.

### Spec Files

Spec files are the test files that are created for each component, and they are used to test the functionality of the component.

# Commits 3, 4

These commits contain updates to the README.md file.
