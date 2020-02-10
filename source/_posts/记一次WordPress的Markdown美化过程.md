title: 记一次WordPress的Markdown美化过程
url: 415.html
id: 415
categories:
  - Linux &amp; VPS
date: 2019-05-19 10:38:21
tags:
---
主要动作是：
1. 添加了块引用效果
2. 阻止了代码块中的`<`&`>`被转义

1\. 添加块引用特效
-----------

在`自定义->额外CSS`中粘贴
```css
blockquote {
	border-left: 4px solid #707070;
	border-left: 4px solid rgba(51, 51, 51, 0.7);
	color: #707070;
	color: rgba(51, 51, 51, 0.7);
	font-size: 18px;
	font-size: 1.8rem;
	font-style: italic;
	line-height: 1.6667;
	margin-bottom: 1.6667em;
	padding-left: 0.7778em;
}
```

2\. 避免< > 被转义
-------------

在 `外观->theme-editor->functions.php` 中添加
```php
function my_content_filter( $content ) {
	$new_content = str_replace('<','<',$content);
	$new_content = str_replace('>','>',$new_content);
    return $new_content;
}
add_filter( 'the_content', 'my_content_filter');
```