# 05 - Namespaces & naming conventions
**SI*CSS + HTML**

#si*css+html/naming-convention

A preprocessor can make your intentions clear.

```scss
.article-search {
  ...
  &-bar {
    ...
  }
}
```

However if you are working on a long term project you’ll most likely spend a lot of time working with the browser’s style inspector.

```css
.article-search-bar {
  ...
}
```

Seeing only the CSS can make you confused. Is it *article search + bar* or *article + search bar*? Let’s abstract the problem:
- - - -
*Fig. 1*
```css
lorem-ipsum-dolor-amet-sit {
  ...
}
```

Could you identify the parts?
- - - -

*Fig. 2*
```pseudo
var loremIpsum = new Dolor().ametSit();
```

It’s not just the naming but also the grammar context what helps in most programming languages.
- - - -
*Fig. 3*
```css
loremIpsum-dolor-ametSit {
  ...
}
```

CSS doesn’t provide such grammar that expresses this abstraction. That’s why you should prefer *figure 3* to clearly and explicitly communicate your intentions.