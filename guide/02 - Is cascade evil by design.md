# 02 - Is cascade evil by design?

**SI CSS + HTML**

#si*css+html/cascade

Some say the worst thing in CSS is the “C”. [“Do we even need CSS anymore?”](https://css-tricks.com/the-debate-around-do-we-even-need-css-anymore/)

> With great power comes great responsibility.  
*Ben Parker (less known guy Voltaire)*

## Great power

With a small set of rules CSS is capable of styling a huge traversible structure of various semantic elements.

## Great responsibility

You have to handle declaring your globally applied rules with great care:

- Elements alike don’t necessarily mean small difference.
- Specificity creates more specificity.
- The closer to the root, the greater the impact. It’s not only styles that cascade, but also bad design decisions.

---

## 20+ years around

Whenever thinking about CSS, take it into consideration that it was born to support a much simpler idea with *now* a great responsibility to be backwards compatible as much as it can be.

> “[CSS] was originally designed to maintain the ideal of html as a content delivery thing that has semantic meaning,” said Tab Atkins Jr., a spec hacker at Google, in a [Web Platform Podcast](http://thewebplatform.libsyn.com/50-the-evolution-of-css). “Particularly so machines can understand.”

[The Evolution of CSS](https://blogs.adobe.com/creativecloud/the-evolution-of-css/)

---

## Recommendations

### Avoid “negators”.

Negators are properties that will try to revert inherited properties’ effects. “Fixing” a property that is useless for a component creates junk.

```css
btn {
  border: 1px solid red;
}

btn-link {
  border: none;
}
```

```html
<a class="btn btn-link href="#">click here</a>
```

If the next design for `btn` component ignores borders, and you miss to update `btn-link` the *negator* rule, you can increment that debt counter. Why would you remember? Semantically it seems incorrect to grow `btn-link` out of `btn` anyway.

### Start with small rules

Common rules should be small to keep flexibility in children.
