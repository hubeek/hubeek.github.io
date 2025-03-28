# Dynamic UIFont

_Status: Published_
_Created: 2021-09-24 02:51:29_
_Tags: iOS, swift_

# UIFont
 
.largeTitle, .title1, .title2, .title3, .headline, .subheadline, .body, .footnote, .caption1, .caption2,  .callout

## Large (Default)  
| Style       | Weight | Size (points)  
| ---------- | :------: | --------------: |  
Large Title | Regular | 34  
Title 1 | Regular | 28  
Title 2 | Regular |  22  
Title 3 | Regular |  20  
Headline | Semi-Bold | 17   
Body |Regular | 17  
Callout | Regular | 16  
Subhead | Regular |15  
Footnote | Regular | 13  
Caption 1 | Regular | 12  
Caption 2 | Regular | 11  

```
let label = UILabel()
label.font = UIFont.preferredFont(forTextStyle: .body)
label.adjustsFontForContentSizeCategory = true 
```
[apple doc](https://developer.apple.com/design/human-interface-guidelines/ios/visual-design/typography/#dynamic-type-sizes])  
[article with examples](https://sarunw.com/posts/scaling-custom-fonts-automatically-with-dynamic-type/)  