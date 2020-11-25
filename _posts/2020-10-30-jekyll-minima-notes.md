---
title: "Anatomy of Jekyll Minina Theme"
date: 2020-10-30 14:21:03 +1100
categories: Jekyll
image: /assets/images/jekyll-logo-dark-solid.png
---
A post to disassemble the Jekyll Minima Theme, from style to logic. 

# Style
1. base.scss  
    1. `kern` is shorter for `kernning`. Kerning enables these edges to overlap so the space between each character can be adjusted to be tighter or looser.
`font-kerning` defines distance between chars. 
```
-webkit-font-feature-settings: "kern" 1;
font-kerning: normal;
```
    2. `%vertical-rhythm` to maintain the vertical rhythm between texts. 





***
Reference:  
1. [What does -moz-font-feature-settings: 'kern' do?
](https://stackoverflow.com/questions/45311518/what-does-moz-font-feature-settings-kern-do){:target="\_blank"}
2. [Kerning on the Web](https://blog.typekit.com/2014/02/05/kerning-on-the-web/){:target="\_blank"}
3. [font-feature-settings](https://css-tricks.com/almanac/properties/f/font-feature-settings/){:target="\_blank"}
4. [CSS font-feature-settings 50+关键字属性值完整介绍](https://www.zhangxinxu.com/wordpress/2018/12/css-font-feature-settings-keyword-value/){:target="\_blank"}
5. [Why is Vertical Rhythm an Important Typography Practice?](https://zellwk.com/blog/why-vertical-rhythms/#:~:text=What%20is%20Vertical%20Rhythm%3F,to%20create%20the%20consistent%20spaces.){:target="\_blank"}

