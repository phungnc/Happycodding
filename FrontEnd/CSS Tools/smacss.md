## SMACSS
css architecture
the very core of SMACSS is categorization.

There are five types of categories:

### Categorizing CSS Rules

1. Base

It doesn't include any class or ID selectors.
It applied to an element.

```css
body, form {
    margin: 0;
    padding: 0;
}

a {
    color: #039;
}

a:hover {
    color: #03F;
}
```

2. Layout

These devide the page into major sections.

Only has a single selector: a single ID or class name.

```css
#article {
    float: left;
}

#sidebar {
    float: right;
}

.l-flipped #article {
    float: right;
}

.l-flipped #sidebar {
    float: left;
}
```

3. Module

These are the reusable modular components of a design

4. State

These describe how things look when in a particular state (hiden, collapse, expanded, active/inactive)

5. Theme

These define things like a color scheme or typographic treatment across a site

### Naming Rules

1. l- for layout
2. is- for state
3. every modules start with a prefix like .moduleName-
4. use .exm for code examples

### Demo

less
  |
  |----+-layouts/
  |    | +-- _footer.less
  |    | +-- _header.less
  |    | +-- _grid.less
  |    |
  |    +-base/
  |    | +-base.less
  |    |
  |    +-modules/
  |    | +-- button.less
  |    | +-- icon.less
  |    | +-- box.less
  |    |
  |    +-states/
  |    | +-- button-state.less  
