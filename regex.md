# Regular expression (regex)

⭐️ [Regex For Noobs (like me!) - An Illustrated Guide](https://www.janmeppe.com/blog/regex-for-noobs/)

[Live Regular Expression Tester for PHP](https://www.phpliveregex.com/)

## Practical cases

[Sample Regular Expressions](https://www.phpliveregex.com/learn/)

## How to match

**Match timestamp in .vtt file**
```regex
(?:\d{2})?:?\d{2}:\d{2}\.\d{3}.+
```
```vtt
00:00:33.633 --> 00:00:35.200
♪ Let me up first ♪
```
https://www.w3.org/TR/webvtt1/#webvtt-timestamp

**Filter only href and use capture group to grab the URL using PCRE**
```regex
href="([^"]*)"
```
`[^"]*` matches any character except `"`.

