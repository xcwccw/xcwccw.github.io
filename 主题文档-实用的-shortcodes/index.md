# LoveIt主题文档 - 实用的 Shortcodes


# 实用的 Shortcodes

## 1.link

**1.`link` shortcode 有以下命名参数：**

* **href** `必选`(**第一个**位置参数)：链接的目标

* **content** `可选` (**第二个**位置参数)：链接的内容, 默认值是 **href** 参数的值（支持 Markdown 或者 HTML 格式.*）

* **title** `可选`(**第三个**位置参数)：HTML `a` 标签 的 `title` 属性, 当悬停在链接上会显示的提示.

* **rel** `可选`：HTML `a` 标签 的 `rel` 补充属性.

* **class**`可选`：HTML `a` 标签 的 `class` 属性.



**2.一个 `link` 示例：**

```markdown
{{</* link "https://assemble.io" */>}}
或者
{{</* link href="https://assemble.io" */>}}

{{</* link "mailto:contact@revolunet.com" */>}}
或者
{{</* link href="mailto:contact@revolunet.com" */>}}

{{</* link "https://assemble.io" Assemble */>}}
或者
{{</* link href="https://assemble.io" content=Assemble */>}}
```

呈现的输出效果如下：

* {{< link "https://assemble.io" >}}
* {{< link "mailto:contact@revolunet.com" >}}
* {{< link "https://assemble.io" Assemble >}}



**3.一个带有标题的 `link` 示例：**

```markdown
{{</* link "https://github.com/" GitHub "Visit Upstage!" */>}}
或者
{{</* link href="https://github.com/" content=GitHub title="Hello GitHub!" */>}}
```

**呈现的输出效果如下 (将鼠标悬停在链接上，会有一行提示):**

{{< link "https://github.com" GitHub "Hello GitHub!" >}}



## 2.image

**1.`image` shortcode 有以下命名参数:**

* **src** *[必需]* (**第一个**位置参数)：图片的 URL.

* **alt** *[可选]* (**第二个**位置参数)：图片无法显示时的替代文本, 默认值是 **src** 参数的值（支持 Markdown 或者 HTML 格式）

* **caption** *[可选]* (**第三个**位置参数)：图片标题（支持 Markdown 或者 HTML 格式）

* **title** *[可选]*：当悬停在图片上会显示的提示

* **class** *[可选]*：HTML `figure` 标签的 `class` 属性

* **src_s** *[可选]*：图片缩略图的 URL, 用在画廊模式中, 默认值是 **src** 参数的值.

* **src_l** *[可选]*：高清图片的 URL, 用在画廊模式中, 默认值是 **src** 参数的值.

* **height** *[可选]*：图片的 `height` 属性.

* **width** *[可选]*：图片的 `width` 属性.

* **linked** *[可选]*：图片是否需要被链接, 默认值是 `true`.

* **rel** *[可选]*：HTML `a` 标签 的 `rel` 补充属性, 仅在 **linked** 属性设置成 `true` 时有效.



**2.一个 `image` 示例:**

```markdown
{{</* image src="/images/avatar.png" caption="江南烧酒 (`image`)" src_s="/images/avatar.png" src_l="/images/avatar.png" */>}}
```

呈现的输出效果如下:

{{< image src="/images/avatar.png" caption="江南烧酒 (`image`)" src_s="/images/avatar.png" src_l="/images/avatar.png" >}}



## 3.admonition

**1.`admonition` shortcode 支持 12 种 横幅**（支持 Markdown 或者 HTML 格式）

{{< admonition >}}
一个 **注意** 横幅
{{< /admonition >}}

{{< admonition abstract >}}
一个 **摘要** 横幅
{{< /admonition >}}

{{< admonition info >}}
一个 **信息** 横幅
{{< /admonition >}}

{{< admonition tip >}}
一个 **技巧** 横幅
{{< /admonition >}}

{{< admonition success >}}
一个 **成功** 横幅
{{< /admonition >}}

{{< admonition question >}}
一个 **问题** 横幅
{{< /admonition >}}

{{< admonition warning >}}
一个 **警告** 横幅
{{< /admonition >}}

{{< admonition failure >}}
一个 **失败** 横幅
{{< /admonition >}}

{{< admonition danger >}}
一个 **危险** 横幅
{{< /admonition >}}

{{< admonition bug >}}
一个 **Bug** 横幅
{{< /admonition >}}

{{< admonition example >}}
一个 **示例** 横幅
{{< /admonition >}}

{{< admonition quote >}}
一个 **引用** 横幅
{{< /admonition >}}



**2.`admonition` shortcode 有以下命名参数：**

* **type** *[可选]* (**第一个**位置参数)：`admonition` 横幅的类型, 默认值是 `note`.

* **title** *[可选]* (**第二个**位置参数)：`admonition` 横幅的标题, 默认值是 **type** 参数的值.

* **open** *[可选]* (**第三个**位置参数)：横幅内容是否默认展开, 默认值是 `true`.



**3.一个 `admonition` 示例：**

```markdown
{{</* admonition type=tip title="This is a tip" open=false */>}}
一个 **技巧** 横幅
{{</* /admonition */>}}
或者
{{</* admonition tip "This is a tip" false */>}}
一个 **技巧** 横幅
{{</* /admonition */>}}
```

呈现的输出效果如下:

{{< admonition tip "This is a tip" false >}}
一个 **技巧** 横幅
{{< /admonition >}}



## 4.person

**`person` shortcode 用来在你的文章中以 [h-card](http://microformats.org/wiki/h-card) 的格式插入个人网站链接**

**1.`person` shortcode 有以下命名参数：**

* **url** *[必需]* (**第一个**位置参数)：URL of the personal page

* **name** *[必需]* (**第二个**位置参数)：Name of the person

* **text** *[可选]* (**第三个**位置参数)：Text to display as hover tooltip of the link

* **picture** *[可选]* (**第四个**位置参数)：A picture to use as person's avatar

* **nick** *[可选]*：Nickame of the person



**2.一个 `person` 示例：**

```markdown
{{</* person url="https://evgenykuznetsov.org" name="Evgeny Kuznetsov" nick="nekr0z" text="author of this shortcode" picture="https://evgenykuznetsov.org/img/avatar.jpg" */>}}
```

呈现的输出效果为 {{< person url="https://evgenykuznetsov.org" name="Evgeny Kuznetsov" nick="nekr0z" text="author of this shortcode" picture="https://evgenykuznetsov.org/img/avatar.jpg" >}}

