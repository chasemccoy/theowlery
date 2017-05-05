---
title: How to remove the margins from an iOS Today View Extension
author: Chase McCoy
layout: post
categories:
  - Development
---

If you’ve ever developed a Today Extension for iOS, you know that by default there is a margin on the left hand side so that the content of the widget aligns with the title. This is nice, but sometimes we want our content to extend to the edge of the widget.

This is very simple to accomplish, but it’s a bit of code that I always forget. Just add this to the view controller of your widget and you are all set:

```objc
- (UIEdgeInsets)widgetMarginInsetsForProposedMarginInsets:(UIEdgeInsets)defaultMarginInsets {
    return UIEdgeInsetsZero;
}
```