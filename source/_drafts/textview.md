---
title: textview
permalink: textview
toc: false
date: 2019-01-18 15:36:15
tags:
categories:
---
- `android:text`: Set the text to display.
- `android:textColor`: Set the color of the text. You can set the attribute to a color value, a predefined resource, or a theme. Color resources and themes are described in other chapters.
- `android:textAppearance`: The appearance of the text, including its color, typeface, style, and size. You set this attribute to a predefined style resource or theme that already defines these values.
- `android:textSize`: Set the text size (if not already set by android:textAppearance). Use sp (scaled-pixel) sizes such as 20sp or 14.5sp, or set the attribute to a predefined resource or theme.
- `android:textStyle`: Set the text style (if not already set by android:textAppearance). Use normal, bold, italic, or bold|italic.
- `android:typeface`: Set the text typeface (if not already set by android:textAppearance). Use normal, sans, serif, or monospace.
- `android:lineSpacingExtra`: Set extra spacing between lines of text. Use sp (scaled-pixel) or dp (device-independent pixel) sizes, or set the attribute to a predefined resource or theme.
- `android:autoLink`: Controls whether links such as URLs and email addresses are automatically found and converted to clickable (touchable) links.

Use one of the following with android:autoLink:

- none: Match no patterns (default).
- web: Match web URLs.
- email: Match email addresses.
- phone: Match phone numbers.
- map: Match map addresses.
- all: Match all patterns (equivalent to web|email|phone|map).
For example, to set the attribute to match web URLs, use `android:autoLink="web"`.