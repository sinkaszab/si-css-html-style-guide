# 07 - Grouping your rules
**SI*CSS + HTML**

#si*css+html/rule-types

## Units & Structures
### Why “unit”?
By design I try to avoid common “buzzwords” like *module* and *component*. Simply to make it easier to make a difference.

### So what is a “unit”?
Cut the crap, let’s talk about what constraints a unit needs to conform:

...

* Base rules
* Constraint rules
* Modifier rules
* State rules






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
* If 80% of your buttons will have a 5px padding around, it's appropriate to create a general rule. There might only be a few places where it needs to be overridden. If you have however 4 or 5 types with different paddings which do not have anything in common ... 
* 

### Normalize & Reset
Normalising the base elements is a more modern and less intrusive approach, so that's the preferred solution. However this might depend on what you need to support.

## Constraint rules~1
## Brand rules~1
## Unit rules
Why unit? Mainly because other methodologies don’t use it. It will help you start with a blank page.

## Section rules

~1 Should stay private. Should be @extended or @included as mixin.

A unit is a component that you could grab and move to another section.
Sections hold together units sharing common semantics. Navigation holds links to other pages. Sections are containers for units of common purpose.