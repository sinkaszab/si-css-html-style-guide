# 07 - Grouping your rules

**SI CSS + HTML**

#si*css+html/rule-types

## Units & Structures

### Why “unit”?

By design I try to avoid common “buzzwords” like *module* and *component*. Simply to make it easier to make a difference.

### So what is a “unit”?

Cut the crap, let’s talk about what constraints a unit needs to conform:

...

- Base rules
- Constraint rules
- Modifier rules
- State rules

...

## Base rules

Elements only! Keep them as simple as possible. Avoid being too specific.

*Too specific:*

```css
button {
  padding: 5px;
  background-color: green;
}
```

*Good*

```css
button {
  padding: 5px;
}
```

The example might be a bit over-exaggerated, but the main point is:

- If 80% of your buttons will have a 5px padding around, it's appropriate to create a general rule. There might only be a few places where it needs to be overridden. If you have however 4 or 5 types with different paddings which do not have anything in common ... 

### Normalize & Reset

Normalising the base elements is a more modern and less intrusive approach, so that's the preferred solution. However this might depend on what you need to support.

## Modifier/State rules

```css
.isActive {
  /* declarations */
}
```

- What is active?
- Does it refer to one component or more?
- Is it an interface or protocol? A trait?

Let's see:

```html
<div class="taskCard isActive">
    <h1>Urgent</h1>
    <p>Write proper examples.</p>
</div>

<ul>
    <li class="projectList-item isActive">...</li>
    <li class="projectList-item">...</li>
</ul>
```

Well, in an ideal world, these components might share their active state. But what if a 3rd component has different needs for it's active state or the design has been changed?

1. Keep `.isActive` & use negators for the 3rd component. (Not preferred solution. See Chapter 2.)

```css
.isActive {
  /* a, b, c declarations */
}
.loginButton.isActive {
  /* negate: a, b; add: e, f declarations;*/
}
```

2. Make `.isActive` an empty rule-set! ... (Don't do that.)

```css
.isActive { } /* could as well be deleted */

.taskCard.isActive {
  /* A type isActive declarations */
}

.projectList-item.isActive {
  /* A type isActive declarations (duplicated) */
}

.loginButton.isActive {
  /* B type isActive declarations */
}
```

- The problem with the above is, that `<component>.isActive` uses a non-existent rule-set. Kind of a “pseudo” class. A non-explicit/non-existing interface.
- Although with preprocessors we could make this fairly sensible.

```scss
// is-active.scss -> mixins (decorators)

@mixin cardLike--isActive {
  border: 2em solid cyan;
}

@mixin buttonLike--isActive {
  border: 4em solid red;
}

// main.scss
.taskCard {
  /* ... */
  &.isActive {
    @include cardLike--isActive;
  }
}

.projectList-item {
  /* ... */
  &.isActive {
    @include cardLike--isActive;
  }
}

.loginButton {
  /* ... */
  &.isActive {
    @include buttonLike--isActive;
  }
}
```

```css
.taskCard.isActive {
  border: 2em solid cyan;
}

.projectList-item.isActive {
  border: 2em solid cyan;
}

.projectList-item.isActive {
  border: 4em solid red;
}
```

- Duplication resolved with preprocessing CSS.
- But we still have that dangling, specificity increasing non-existent interface.

3. Let's call object oriented design for help. We need an `isActive` interface and different traits that implement the interface for more types of components.

Might be a good solution, if there are still common properties. Prepocessors can help to cleaner represent this scenario.

```scss
// is-active.scss -> interface

%cardLike--isActive { // trait for interface
  border: 2em solid cyan;
}

%buttonLike--isActive { // trait for interface
  border: 4em solid red;
}

// main.scss
.taskCard--isActive {
  @extend %cardLike--isActive; // use trait
  /* ... */
}

.projectList-item--isActive {
  @extend %cardLike--isActive; // use trait
  /* ... */
}

.loginButton--isActive {
  @extend %buttonLike--isActive; // use trait
  /* ... */
}
```

```css
.taskCard--isActive, .projectList-item--isActive {
  border: 2em solid cyan;
}

.projectList-item--isActive {
  border: 4em solid red;
}
```

What this enables us is to hide the interface behind the implementation.
