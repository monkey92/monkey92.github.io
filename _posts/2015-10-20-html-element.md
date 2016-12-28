---
layout: post
title: html元素的分类
categories: html
---

html元素的分类  
一、html元素的分为块级元素和行内元素  

二、块级元素和行内元素的特点  

block（块）元素的特点：  
 	1. 总是在新行上开始；  
 	2. 高度，行高以及外边距和内边距都可控制；  
 	3. 宽度缺省是它的容器的100%，除非设定一个宽度。  
 	4. 它可以容纳内联元素和其他块元素  
 
inline元素的特点：   
	1. 和其他元素都在一行上；  
	2. 高和外边距不可改变；  
	3. 宽度就是它的文字或图片的宽度，不可改变，设置width,height无效，可以通过line-height来设置。设置margin 只有左右margin有效，上下无效。设置padding 只有左右padding有效，上下则无效。
	注意元素范围是增大了，但是对元素周围的内容是没影响的。  
	4. 内联元素只能容纳文本或者其他内联元素

三，常见块级元素和行内元素
 
 块级元素： 
    * address - 地址  
	* blockquote - 块引用  
    * center - 举中对齐块 （html5取消了该标签）  
    * div - 常用块级容易，也是css layout的主要标签  
    * dl - 定义列表
    * fieldset - form控制组
    * form - 交互表单
    * h1 - 大标题
    * h2 - 副标题
    * h3 - 3级标题
    * h4 - 4级标题
    * h5 - 5级标题
    * h6 - 6级标题
    * hr - 水平分隔线
    * isindex - input prompt
    * menu - 菜单列表
    * noframes - frames可选内容，（对于不支持frame的浏览器显示此区块内容）
    * noscript - 可选脚本内容（对于不支持script的浏览器显示此内容）
    * ol - 排序表单
    * p - 段落
    * pre - 格式化文本
    * table - 表格
    * ul - 非排序列表（无序列表）
    * address - 地址
 
 行内元素：
    * a - 锚点
    * abbr - 缩写
    * acronym - 首字
    * b - 粗体(不推荐)
    * bdo - bidi override
    * big - 大字体
    * br - 换行
    * cite - 引用
    * code - 计算机代码(在引用源码的时候需要)
    * dfn - 定义字段
    * em - 强调
    * font - 字体设定(不推荐) （html5取消了该标签）
    * i - 斜体
    * img - 图片
    * input - 输入框
    * kbd - 定义键盘文本
    * label - 表格标签
    * q - 短引用
    * s - 中划线(不推荐)
    * samp - 定义范例计算机代码
    * select - 项目选择
    * small - 小字体文本
    * span - 常用内联容器，定义文本内区块
    * strike - 中划线
    * strong - 粗体强调
    * sub - 下标
    * sup - 上标
    * textarea - 多行文本输入框
    * tt - 电传文本
    * u - 下划线
    * var - 定义变量
