# Commit 13

## Getter

Since the src attribute on the image tag is clunky and can be refactored, I added a getter to the UserComponent that returns the image path that was stored in the image tag's src attribute:

![user-getter-image-path](user-getter-image-path.png)

The new getter function will then replace the image tag's src attribute:

```html
<div>
  <button>
    <img [src]="imagePath" [alt]="selectedUser.name" />
    <span>{{ selectedUser.name }}</span>
  </button>
</div>
```

We are still binding to the image tag's src attribute, but we are using a computed getter in the UserComponent instead, keeping our code clean.
