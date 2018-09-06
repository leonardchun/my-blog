title: MarkDown
author: Leonard
tags: []
categories:
  - 语法手册
cover_picture: /images/md.jpg
date: 2018-08-29 20:06:00
---
** {{ title }}：** <Excerpt in index | 首页摘要>
分布式系统不是万能，不能解决所有痛点。在高可用，一致性，分区容错性必须有所权衡。
<!-- more -->
<The rest of contents | 余下全文>

markdown基本语法

一、标题
    在想要设置为标题的文字前面加#来表示
    一个#是一级标题，二个#是二级标题，以此类推。支持六级标题。

二、字体

    加粗
    要加粗的文字左右分别用两个*号包起来
    
    斜体
    要倾斜的文字左右分别用一个*号包起来
    
    斜体加粗
    要倾斜和加粗的文字左右分别用三个*号包起来
    
    删除线
    要加删除线的文字左右分别用两个~~号包起来

三、引用
    在引用的文字前加>即可。引用也可以嵌套，如加两个>>三个>>>
    n个...
    貌似可以一直加下去，但没神马卵用

四、分割线
    三个或者三个以上的 - 或者 * 都可以。

五、图片
    
    ![图片alt](图片地址 ''图片title'')
    
    图片alt就是显示在图片下面的文字，相当于对图片内容的解释。
    图片title是图片的标题，当鼠标移到图片上时显示的内容。title可加可不加

    示例：
    ![blockchain](https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/
    u=702257389,1274025419&fm=27&gp=0.jpg "区块链")
六、超链接
    超链接名](超链接地址 "超链接title")
    title可加可不加
    示例：
    [简书](http://jianshu.com)
    [百度](http://baidu.com)

    <a href="超链接地址" target="_blank">超链接名</a>
    例<a href="https://www.jianshu.com/u/1f5ac0cf6a8b" target="_blank">简书</a>
七、列表
* 无序列表
    无序列表用 - + * 任何一种都可以
* 有序列表
    数字加点
* 列表嵌套
    上一级和下一级之间敲三个空格即可

八、表格
| Tables | Are | Cool |
| ------------- |:-------------:| -----:|
| col 3 is | right-aligned | $1600 |
| zebra stripes | are neat | $1 |

    通过使用“|”符号分割表格的每格，以及“-”减号及“:”冒号表示对齐方式，减号的个数不限，但减号至少要有一个

    若没有冒号或冒号在减号左边表示左对齐
    减号两边都有表示中间对齐
    若在减号右边表示右对齐
    第一行表格每类的名字一定要有以及减号和冒号的一行也一定要有，第一行属性会自动黑体加粗，即第一行是表格属性名，第二行则是表格对齐方式，第三行是表格输出的第一行内容，第四行是第二行内容，以此类推

    注意上述的冒号一定要是英文模式下输入，不可在中文形式，一定要注意
    
九、代码
    单行代码：代码之间分别用一个反引号包起来
    
    ```
    public static void main(){
        system.out.println("Hello World！");
    }
    ```
    
十、流程图
```flow
st=>start: 开始
op=>operation: My Operation
cond=>condition: Yes or No?
e=>end
st->op->cond
cond(yes)->e
cond(no)->op
&```