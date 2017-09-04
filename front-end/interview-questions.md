前端面试问题合集及解答
==

不同于传统的软件工程师职位面试，前端职位面试较少注重算法层面的内容，更多是问一些关于 HTML、CSS 和 JavaScript 的专业知识。

虽然已经有一些现有的资源来帮助前端开发者准备面试，但它们并没有帮助软件工程师面试的材料那么丰富。在现有的资源里，[Front End Job Interview Questions](https://github.com/h5bp/Front-end-Developer-Interview-Questions) 大概算是最有帮助的问题合集了，不幸的是，我并没有在网上找到完整且令人满意的答案，所以在这篇文章里，我将尝试解答这些问题。作为一个开源仓库，希望本项目可以随着 Web 的发展，在社区的支持下存活下去。

## 目录

  1. [HTML 问题](#html-questions)
  1. [CSS 问题](#css-questions)
  1. [JS 问题](#js-questions)

## HTML 问题

这个部分是对 [Front-end Job Interview Questions - HTML Questions](https://github.com/h5bp/Front-end-Developer-Interview-Questions#html-questions) 的解答，欢迎提 Pull Request 进行建议和纠正！

#### `doctype` 是做什么的？

`doctype` 是 document type（文档类型）的缩写。它是一个声明，在 HTML5 里用它来区分标准解析模式和怪异解析模式。所以它的存在是告诉浏览器要在标准模式下解析和渲染 Web 页面。

说白了就是，只需把 `<!DOCTYPE html>` 添加到你的页面开头就行了。

###### 参考

- https://stackoverflow.com/questions/7695044/what-does-doctype-html-do
- https://www.w3.org/QA/Tips/Doctype

#### 完全标准模式、近乎标准模式和怪异模式的区别是什么？

- **怪异模式** - 布局会模拟在 Netscape Navigator 4 和 IE 5 中的非标准行为。为了支持那些在广泛采用 Web 标准之前建立的网站，这个模式很有必要。怪异模式的行为列表可以查看[这个链接](https://developer.mozilla.org/en-US/docs/Gecko's_Almost_Standards_Mode)。
- **完全标准模式** - 在此模式下布局行为是由 HTML 和 CSS 规范描述的。
- **近乎标准模式** - 这个模式只实现了很少一部分怪异行为，可以通过[这个链接](https://developer.mozilla.org/en-US/docs/Gecko's_Almost_Standards_Mode)查看区别。

###### 参考

- https://developer.mozilla.org/en-US/docs/Quirks_Mode_and_Standards_Mode

#### HTML 和 XHTML 的区别是什么？

XHTML 属于 XML 标记语言，和 HTML 是不一样的。一些差异如下：

- XHTML 文档必须结构完整良好，不像 HTML 的容错性那么高。
- XHTML 的元素和属性名是大小写敏感的，而 HTML 不是。
- 原始的 `<` 和 `&` 字符不允许单独出现，除非包含在 `CDATA` 块中（`<![CDATA[ ... ]]>`）。 而 JavaScript 通常会包含一些在 CDATA 块之外，不能存在于 XHTML 里的字符，比如 `<` 操作符。所以在 XHTML 里很难去使用内联的 `styles` 和 `script` 标签，而且应该避免使用。
- 在 XML 里如果出现一个严重的解析错误（如一个错误的标签结构）将导致文档处理被中止。

在[维基百科](https://en.wikipedia.org/wiki/XHTML#Relationship_to_HTML)上可以找到完整的差异列表。

###### 参考

- https://developer.mozilla.org/en-US/docs/Archive/Web/Properly_Using_CSS_and_JavaScript_in_XHTML_Documents_
- https://en.wikipedia.org/wiki/XHTML

#### 服务页面类型为 `application/xhtml+xml` 的话会有什么问题？

基本上，问题还是在于解析 HTML 和 XML 之间的区别。

- XHTML，或者说 XML 的语法缺少容错性，如果你的页面不是完全兼容 XML 的话，就会有解析错误，而且用户会得到不可读的内容。
- 将页面类型服务为 `application/xhtml+xml` 的话将导致 IE 8 展示一个未知格式文件的下载对话框，而不是展示你的页面，因为首个支持 XHTML 的 IE 浏览器是 IE 9。

###### 参考

- https://developer.mozilla.org/en-US/docs/Quirks_Mode_and_Standards_Mode#XHTML

#### 如何用多语言提供一个服务页面？

这个问题有一点模糊，我将假设问的是最常见的情况，如何在多语言环境下服务页面是可用的，而页面里的内容还照样是单语言。

当向服务器发出一个 HTTP 请求的时候，发出请求的用户代理通常还会发送关于语言偏好的信息，比如 header 里的 `Accept-Language` 字段。如果有可用的语言版本，服务器就会根据这个信息返回合适语言的文档版本。返回的 HTML 文档也应该在 `<html>` 标签里声明 `lang` 属性，比如 `<html lang="en">...</html>`。

在后端，HTML 标记会包含 `i18n` 占位符，而且特定语言的内容会存储在 YML 或者 JSON 格式的文件当中。服务器通常就可以在后端框架的帮助下，动态地用特定语言内容来生成 HTML 页面。

###### 参考

- https://www.w3.org/International/getting-started/language

#### 在做多语言站点的设计或开发时，你必须注意哪些事情？

- 在 HTML 里使用 `lang` 属性。
- 引导用户使用他们的母语 - 允许用户轻松修改他的国家或语言。
- 图片里放文本不是一个可扩展的方法 - 在图片里放置文本仍旧是一种很受欢迎的方式，它可以在任意计算机上都展示好看的非系统字体。然而要翻译图片文本的话，每个文本字符串都需要为每种语言创建一个单独的图片。这样做的话数量稍微一多就会失控了。
- 限制词语或句子的长度 - 某些内容在用另一种语言展示的时候会变得很长。在设计时一定要注意布局和溢出的问题。最好避免设计大量文本或者破坏设计。标题、标签和按钮等内容上的字符也属于考虑范围。但对于自然流动的文本如正文文本和评论来说，它们就不那么重要了。
- 注意颜色是如何被感知的 - 不同的语言和文化对颜色的感知是不同的。设计应该适当地使用颜色。
- 格式化日期和货币 - 日历日期有时需要以不同的方式呈现。例如 “May 31, 2012” 是美国呈现方式，“31 May 2012” 是部分欧洲国家的呈现方式。
- 不要连接翻译的字符串 - 千万不要出现这种情况：`"The date today is " + date`。它会以不同的单词顺序出现在不同的语言中。所以尽量使用模板参数替代。

###### 参考

- https://www.quora.com/What-kind-of-things-one-should-be-wary-of-when-designing-or-developing-for-multilingual-sites

#### `data-` （标签）属性有什么好处？

在 JavaScript 框架流行之前，前端开发者普遍使用 `data-` （标签）属性将额外的数据存储在 DOM 本身，而无需在 DOM 上添加其他非标准的（标签）属性或者额外的（对象）属性。这么做的目的是将自定义数据存储到页面或应用当中，因为已经没有更合适的（标签）属性或元素来存储它们了。

目前，已经不鼓励使用 `data-`（标签）属性了。其中一个原因就是用户可以使用检查浏览器元素功能，轻易地改变这个数据属性。而数据模型可以更好地存储在 JavaScript 内部，并且有可能使用一个库或框架，通过数据绑定来更新 DOM。

###### 参考

- http://html5doctor.com/html5-custom-data-attributes/

#### 把 HTML5 看作一个开放的 Web 平台。那么 HTML5 由哪几块组成？

- 语义化 - 允许你更精确地描述内容是什么。
- 连通性 - 允许你用新型的方式与服务器通信。
- 离线存储 - 允许 Web 页面在本地客户端存储数据，并更有效地离线操作
- 多媒体 - 使视频和音频在开放的 Web 中成为头等公民。
- 2D/3D 图形及效果 - 允许更多样化的展示选项。
- 性能与集成 - 提供更快的速度优化，更好地使用计算机硬件。
- 设备访问 - 允许使用各种输入输出设备。
- 样式 - 让开发者写出更复杂的主题。

###### 参考

- https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/HTML5

#### 描述 `cookie`、`sessionStorage` 和 `localStorage` 之间的区别

上面提到的技术都是客户端的键值存储机制。它们都只能将值存储为字符串。

|  |`cookie`|`localStorage`|`sessionStorage`|
|--|--|--|--|
| 发起方 | 客户端或服务器。服务器可以使用 `Set-Cookie` 头部。 | 客户端 | 客户端 |
| 过期时间 | 手动设置 | 永久 | 标签页关闭 |
| 跨浏览器持久会话 | 取决于是否设置过期时间 | 是 | 否 |
| 是否域相关 | 是 | 否 | 否 |
| 跟随每个 HTTP 请求发送到服务器| 所有 Cookie 都会通过 `Cookie` 头部自动发送 | 否 | 否 |
| 最大容量（每个域） | 4kb | 5MB | 5MB |
| 可访问性 | 所有窗口 | 所有窗口 | 同标签页 |

###### 参考

- https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies
- http://tutorial.techaltum.com/local-and-session-storage.html

#### 描述 `<script>`、`<script async>` 和 `<script defer>` 之间的区别

- `<script>` - HTML 解析会被阻塞，脚本会被获取并立即执行，执行完毕后 HTML 解析恢复。
- `<script async>` - 脚本获取将与 HTML 解析并行，并在其可用时执行（可能在 HTML 解析完成之前）。当脚本独立于页面上其他脚本时，建议使用 `async`， 比如分析脚本。  
- `<script defer>` - 脚本获取将与 HTML 解析并行，并在页面完成解析时执行。如果有多个这样的脚本，那么每个延迟脚本会按照其在文档中的记录顺序来执行。如果脚本依赖完整解析的 DOM，那么 `defer` 属性就会很有用，它确保了在脚本执行之前 HTML 完整解析。这么做其实和将一个普通的 `<script>` 放到 `<body>` 的后面没有太大的区别。但是一个延迟脚本不能包含 `document.write`。

注意：没有 `src` 属性的 script 标签，`async` 和 `defer` 属性都会被忽略。

###### 参考

- http://www.growingwiththeweb.com/2014/02/async-vs-defer-attributes.html
- https://stackoverflow.com/questions/10808109/script-tag-async-defer
- https://bitsofco.de/async-vs-defer/

#### 为什么通常认为最好将 CSS 的 `<link>` 标签放在 `<head></head>` 标签之间，将 JS 的 `<script>` 标签放在 `</body>` 标签之前？你知道有什么例外吗？

**将 `<link>` 标签放在 `<head>` 标签里**

将 `<link>` 标签放到头部标签里是规范的一部分。除此之外，放在顶部还使得页面可以渐进式渲染，从而提高用户体验。将样式表放在文档底部的问题在于，它禁止在许多浏览器中进行渐进式渲染，包括Internet Explorer。一些浏览器还会阻止渲染，以避免在样式改变时重新绘制页面元素。用户在这种情况下会卡到一个空白的白色页面。所以放到顶部避免了未添加样式内容的闪现。

**将 `<script>` 标签放在 `<body>` 标签之前**

`<script>` 脚本会在下载和执行的时候阻塞 HTML 解析。在页面底部下载脚本可使 HTML 页面第一时间解析完成并呈现给用户。

当脚本里包含 `document.write()` 的时候就不可以将 `<script>` 放到底部了，但使用 `document.write()` 并不是一个好的实践方法。而且，将 `<script>` 放到页面底部意味着浏览器在整个文档完成解析之前都不能开始下载脚本。还有一个可能的解决方案是，将 `<script>` 标签放到 `<head>` 里并使用 `defer` 属性。

###### 参考
 https://developer.yahoo.com/performance/rules.html#css_top

#### 什么是渐进式渲染？

渐进式渲染是用来提高网页性能（特别是提高感知加载时间）的技术，以使内容尽可能快地渲染完成并展示。

过去在宽带互联网时代渐进式渲染更加流行，但在现代开发当中它仍然十分有用，因为移动互联网变得越来越受欢迎（并且不可靠）！

这种技术的例子有：

- 图片懒加载 - 页面上的图片并非一次性加载完。当用户滚动页面到需要展示图片部分的时候，才使用 JavaScript 来加载图片。
- 对可见内容进行优先级排序（或者首屏渲染） - 只需为了首先在用户浏览器当中渲染的页面，引入所必需的最少的样式、内容和脚本，以便尽可能快地展示页面，之后就可以使用延迟脚本或者监听 `DOMContentLoaded`/`load` 事件来加载其他资源和内容。
- 异步 HTML 片段 - 由于页面是在后端构建的，所以能把一部分 HTML 内容刷新到浏览器上。更多技术细节可以访问[这里](http://www.ebaytechblog.com/2014/12/08/async-fragments-rediscovering-progressive-html-rendering-with-marko/)。

###### 参考

- https://stackoverflow.com/questions/33651166/what-is-progressive-rendering
- http://www.ebaytechblog.com/2014/12/08/async-fragments-rediscovering-progressive-html-rendering-with-marko/

#### 你之前使用过不同的 HTML 模板语言吗？

当然，举几个例子，Jade、ERB、Slim、Handlebars、Jinja 和 Liquid，它们或多或少都提供了类似的功能，用于转义内容，提供有用的过滤器来操纵需要展示的数据。大多数模板引擎还允许你在显示内容之前，在需要自定义处理的事件中注入自己的过滤器。

### 其他答案

- https://neal.codes/blog/front-end-interview-questions-html/
- http://peterdoes.it/2015/12/03/a-personal-exercise-front-end-job-interview-questions-and-my-answers-all/

## CSS 问题

这个部分是对 [Front-end Job Interview Questions - CSS Questions](https://github.com/h5bp/Front-end-Developer-Interview-Questions#css-questions) 的解答，欢迎提 Pull Request 进行建议和纠正！

#### 在 CSS 里，类 和 ID 选择器的区别是什么？

- **ID 选择器** - 在文档里是唯一的。当使用片段标识符链接时，可以使用它来标识一个元素。每个元素只能拥有一个 `id` 属性。
- **类选择器** - 可以在文档里的多个元素上重复使用。主要用来给元素添加样式或将元素作为目标。

#### “Resetting” 和 “Normalizing” 的 CSS 有什么区别？你会选择哪一种，为什么？

- **Resetting** - Resetting 是为了去除元素上所有的浏览器默认样式。比如，所有元素的 `margin`、`padding` 和 `font-size` 都会被重置成一样的值。你将不得不为常见的排版元素重新声明样式。
- **Normalizing** - Normalizing 会保存有用的默认样式，而不是“取消样式”。它还纠正了常见浏览器依赖的错误。

当我需要一个非常定制化或者非传统的站点设计时，我会选择重置样式，这样我就可以做很多我自己的样式设计，而不需要保留任何默认样式。

###### 参考

- https://stackoverflow.com/questions/6887336/what-is-the-difference-between-normalize-css-and-reset-css

#### 描述什么是浮动以及它如何工作

浮动是 CSS 的一个位置属性。不同于会脱离文档流的 `position: absolute` 元素，浮动的元素仍然是页面流的一部分，并且会影响其他位置的元素（如文本将围绕浮动元素流动）。

CSS 的 `clear` 属性可以用在浮动为 `left`/`right`/`both` 的元素下方。

如果一个父级元素只包含浮动元素，那么它的高度就会被折叠为 0。这个问题可以在容器关闭之前，浮动元素的后面通过清除浮动来修复。

`.clearfix` 这个 hack 类使用了 CSS 的伪类（`:after`）来清除浮动。相比在父元素上设置 overflow，添加一个额外的 `clearfix` 类是更好的办法。然后应用下面的 CSS：

```css
.clearfix:after {
  content: ' ';
  visibility: hidden;
  display: block;
  height: 0;
  clear: both;
}
```

或者，给父元素添加一个 `overflow: auto` 或 `overflow: hidden` 的属性，这样就可以在子元素里建立一个新的区块格式化上下文，并使父元素展开包含它的子元素。

###### 参考

- https://css-tricks.com/all-about-floats/

#### 描述 `z-index` 以及堆叠上下文是如何表现的

CSS 里的 `z-index` 属性控制重叠元素的垂直叠加顺序。但 `z-index` 只影响 `position` 值不是 `static` 的元素。

Without any `z-index` value, elements stack in the order that they appear in the DOM (the lowest one down at the same hierarchy level appears on top). Elements with non-static positioning (and their children) will always appear on top of elements with default static positioning, regardless of HTML hierarchy.

A stacking context is an element that contains a set of layers. Within a local stacking context, the `z-index` values of its children are set relative to that element rather than to the document root. Layers outside of that context — i.e. sibling elements of a local stacking context — can't sit between layers within it. If an element B sits on top of element A, a child element of element A, element C, can never be higher than element B even if element C has a higher `z-index` than element B.

Each stacking context is self-contained - after the element's contents are stacked, the whole element is considered in the stacking order of the parent stacking context. A handful of CSS properties trigger a new stacking context, such as `opacity` less than 1, `filter` that is not `none`, and `transform that is not `none`.

###### References

- https://css-tricks.com/almanac/properties/z/z-index/
- https://philipwalton.com/articles/what-no-one-told-you-about-z-index/
- https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context

#### Describe Block Formatting Context (BFC) and how it works.

A Block Formatting Context (BFC) is part of the visual CSS rendering of a web page in which block boxes are laid out. Floats, absolutely positioned elements, `inline-blocks`, `table-cells`, `table-caption`s, and elements with `overflow` other than `visible` (except when that value has been propagated to the viewport) establish new block formatting contexts.

A BFC is an HTML box that satisfies at least one of the following conditions:

- The value of `float` is not `none`.
- The value of `position` is neither `static` nor `relative`.
- The value of `display` is `table-cell`, `table-caption`, `inline-block`, `flex`, or `inline-flex`.
- The value of `overflow` is not `visible`.

In a BFC, each box's left outer edge touches the left edge of the containing block (for right-to-left formatting, right edges touch).

Vertical margins between adjacent block-level boxes in a BFC collapse. Read more on [collapsing margins](https://www.sitepoint.com/web-foundations/collapsing-margins/).

###### References

- https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Block_formatting_context
- https://www.sitepoint.com/understanding-block-formatting-contexts-in-css/

#### What are the various clearing techniques and which is appropriate for what context?

- Empty `div` method - `<div style="clear:both;"></div>`.
- Clearfix method - Refer to the `.clearfix` class above.
- `overflow: auto` or `overflow: hidden` method - Parent will establish a new block formatting context and expand to contains its floated children.

In large projects, I would write a utility `.clearfix` class and use them in places where I need it. `overflow: hidden` might clip children if the children is taller than the parent and is not very ideal.

#### Explain CSS sprites, and how you would implement them on a page or site.

CSS sprites combine multiple images into one single larger image. It is commonly used technique for icons (Gmail uses it). How to implement it:

1. Use a sprite generator that packs multiple images into one and generate the appropriate CSS for it.
1. Each image would have a corresponding CSS class with `background-image`, `background-position` and `background-size` properties defined.
1. To use that image, add the corresponding class to your element.

**Advantages:**

- Reduce the number of HTTP requests for multiple images (only one single request is required per spritesheet). But with HTTP2, loading multiple images is no longer much of an issue.
- Advance downloading of assets that won't be downloaded until needed, such as images that only appear upon `:hover` pseudo-states. Blinking wouldn't be seen.

#### What are your favorite image replacement techniques and which do you use when?

CSS image replacement is a technique of replacing a text element (usually a header tag like an `<h1>`) with an image (often a logo). It has its origins in the time before web fonts and SVG. For years, web developers battled against browser inconsistencies to craft image replacement techniques that struck the right balance between design and accessibility.

It's not really relevant these days. Check out the link below for all the available techniques.

###### References

- https://css-tricks.com/the-image-replacement-museum/

#### How would you approach fixing browser-specific styling issues?

- After identifying the issue and the offending browser, use a separate style sheet that only loads when that specific browser is being used. This technique requires server-side rendering though.
- Use libraries like Bootstrap that already handles these styling issues for you.
- Use `autoprefixer` to automatically add vendor prefixes to your code.
- Use Reset CSS or Normalize.css.

#### How do you serve your pages for feature-constrained browsers? What techniques/processes do you use?

- Graceful degradation - The practice of building an application for modern browsers while ensuring it remains functional in older browsers.
- Progressive enhancement - The practice of building an application for a base level of user experience, but adding functional enhancements when a browser supports it.
- Use [caniuse.com](https://caniuse.com/) to check for feature support.
- Autoprefixer for automatic vendor prefix insertion.
- Feature detection using [Modernizr](https://modernizr.com/).

#### What are the different ways to visually hide content (and make it available only for screen readers)?

These techniques are related to accessibility (a11y).

- `visibility: hidden`. However the element is still in the flow of the page, and still takes up space.
- `width: 0; height: 0`. Make the element not take up any space on the screen at all, resulting in not showing it.
- `position; absolute; left: -99999px`. Position it outside of the screen.
- `text-indent: -9999px`. This only works on text within the `block` elements.

I would go with the `absolute` positioning approach, as it has the least caveats and works for most elements.

#### Have you ever used a grid system, and if so, what do you prefer?

I like the `float`-based grid system because it still has the most browser support among the alternative existing systems (flex, grid). It has been used in Bootstrap for years and has been proven to work.

#### Have you used or implemented media queries or mobile-specific layouts/CSS?

Yes. An example would be transforming a stacked pill navigation into a fixed-bottom tab navigation beyond a certain breakpoint.

#### Are you familiar with styling SVG?

No... Sadly.

#### How do you optimize your webpages for print?

- Create a stylesheet for print or use media queries.

```html
<!-- Main stylesheet on top -->
<link rel="stylesheet" href="/global.css" media="all" />
<!-- Print only, on bottom -->
<link rel="stylesheet" href="/print.css" media="print" />
```

Make sure to put non-print styles inside `@media screen { ... }`.

```css
@media print {
  ...
}
```

- Deliberately add page breaks.

```html
<style>
.page-break {
  display: none;
  page-break-before: always;
}
</style>

Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Fusce eu felis. Curabitur sit amet magna. Nullam aliquet. Aliquam ut diam...
<div class="page-break"></div>
Lorem ipsum dolor sit amet, consectetuer adipiscing elit....
```

###### References

- https://davidwalsh.name/optimizing-structure-print-css

#### What are some of the "gotchas" for writing efficient CSS?

Firstly, understand that browsers match selectors from rightmost (key selector) to left. Browsers filter out elements in the DOM according to the key selector, and traverse up its parent elements to determine matches. The shorter the length of the selector chain, the faster the browser can determine if that element matches the selector. Hence avoid key selectors that are tag and universal selectors. They match a large numbers of elements and browsers will have to do more work in determining if the parents do match.

[BEM (Block Element Modifier)](https://bem.info/) methodology recommends that everything has a single class, and, where you need hierarchy, that gets baked into the name of the class as well, this naturally makes the selector efficient and easy to override.

Be aware of which CSS properties trigger reflow, repaint and compositing. Avoid writing styles that change the layout (trigger reflow) where possible.

###### References

- https://developers.google.com/web/fundamentals/performance/rendering/
- https://csstriggers.com/

#### What are the advantages/disadvantages of using CSS preprocessors?

**Advantages:**

- CSS is made more maintainable.
- Easy to write nested selectors.
- Variables for consistent theming. Can share theme files across different projects.
- Mixins to generate repeated CSS.
- Splitting your code into multiple files. CSS files can be split up too but doing so will require a HTTP request to download each CSS file.

**Disadvantages:**

- Requires tools for preprocessing. Re-compilation time can be slow.

#### Describe what you like and dislike about the CSS preprocessors you have used.

**Likes:**

- Mostly the advantages mentioned above.
- Less is written in JavaScript, which plays well with Node.

**Dislikes:**

- I use Sass via `node-sass`, which is a binding for LibSass written in C++. I have to frequently recompile it when switching between node versions.
- In Less, variable names are prefixed with `@`, which can be confused with native CSS keywords like `@media`, `@import` and `@font-face` rule.

#### How would you implement a web design comp that uses non-standard fonts?

Use `@font-face` and define `font-family` for different `font-weight`s.

#### Explain how a browser determines what elements match a CSS selector.

This part is related to the above about writing efficient CSS. Browsers match selectors from rightmost (key selector) to left. Browsers filter out elements in the DOM according to the key selector, and traverse up its parent elements to determine matches. The shorter the length of the selector chain, the faster the browser can determine if that element matches the selector.

For example with this selector `p span`, browsers firstly find all the `<span>` elements, and traverse up its parent all the way up to the root to find the `<p>` element. For a particular `<span>`, as soon as it finds a `<p>`, it knows that the `<span>` matches and can stop its matching.

###### References

- https://stackoverflow.com/questions/5797014/why-do-browsers-match-css-selectors-from-right-to-left

#### Describe pseudo-elements and discuss what they are used for.

A CSS pseudo-element is a keyword added to a selector that lets you style a specific part of the selected element(s). They can be used for decoration (`:first-line`, `:first-letter`) or adding elements to the markup (combined with `content: ...`) without having to modify the markup (`:before`, `:after`).

- `:first-line` and `:first-letter` can be used to decorate text.
- Used in the `.clearfix` hack as shown above to add a zero-space element with `clear: both`.
- Triangular arrows in tooltips use `:before` and `:after`. Encourages separation of concerns because the triangle is considered part of styling and not really the DOM. It's not really possible to draw a triangle with just CSS styles without using an additional HTML element.

###### References

- https://css-tricks.com/almanac/selectors/a/after-and-before/

#### Explain your understanding of the box model and how you would tell the browser in CSS to render your layout in different box models.

The CSS box model describes the rectangular boxes that are generated for elements in the document tree and laid out according to the visual formatting model. Each box has a content area (e.g. text, an image, etc.) and optional surrounding `padding`, `border`, and `margin` areas.

The CSS box model is responsible for calculating:

- How much space a block element takes up.
- Whether or not borders and/or margins overlap, or collapse.
- A box's dimensions.

The box model has the following rules:

- The dimensions of a block element are calculated by `width`, `height`, `padding`, `border`s, and `margin`s.
- If no `height` is specified, a block element will be as high as the content it contains, plus `padding` (unless there are floats, for which see below).
- If no `width` is specified, a non-floated block element will expand to fit the width of its parent minus `padding`.
- The `height` of an element is calculated by the content's `height`.
- The `width` of an element is calculated by the content's `width`.
- By default, `padding`s and `border`s are not part of the `width` and `height` of an element.

###### References

- https://www.smashingmagazine.com/2010/06/the-principles-of-cross-browser-css-coding/#understand-the-css-box-model

#### What does `* { box-sizing: border-box; }` do? What are its advantages?

- By default, elements have `box-sizing: content-box` applied, and only the content size is being accounted for.
- `box-sizing: border-box` changes how the `width` and `height` of elements are being calculated, `border` and `padding` are also being included in the calculation.
- The `height` of an element is now calculated by the content's `height` + vertical `padding` + vertical `border` width.
- The `width` of an element is now calculated by the content's `width` + horizontal `padding` + horizontal `border` width.

#### List as many values for the `display` property that you can remember.

- `none`, `block`, `inline`, `inline-block`, `table`, `table-row`, `table-cell`, `list-item`.

#### What's the difference between `inline` and `inline-block`?

I shall throw in a comparison with `block` for good measure.

|  |`block`|`inline-block`|`inline`|
|--|--|--|--|
| Size | Fills up the width of its parent container. | Depends on content. | Depends on content. |
| Positioning | Start on a new line and tolerates no HTML elements next to it (except when you add `float`) | Flows along with other content and allows other elements beside. | Flows along with other content and allows other elements beside. |
| Can specify `width` and `height` | Yes | Yes | No. Will ignore if being set. |
| Can be aligned with `vertical-align` | No | Yes | Yes |
| Margins and paddings | All sides respected. | All sides respected. | Only horizontal sides respected. Vertical sides, if specified, do not affect layout. Vertical space it takes up depends on `line-height`, even though the `border` and `padding` appear visually around the content. |
| Float | - | - | Becomes like a `block` element where you can set vertical margins and paddings. |

**What's the difference between a `relative`, `fixed`, `absolute` and `static`-ally positioned element?**

A positioned element is an element whose computed `position` property is either `relative`, `absolute`, `fixed` or `sticky`.

- `static` - The default position; the element will flow into the page as it normally would. The `top`, `right`, `bottom`, `left` and `z-index` properties do not apply.
- `relative` - The element's position is adjusted relative to itself, without changing layout (and thus leaving a gap for the element where it would have been had it not been positioned).
- `absolute` - The element is removed from the flow of the page and positioned at a specified position relative to its closest positioned ancestor if any, or otherwise relative to the initial containing block. Absolutely positioned boxes can have margins, and they do not collapse with any other margins. These elements do not affect the position of other elements.
- `fixed` - The element is removed from the flow of the page and positioned at a specified position relative to the viewport and doesn't move when scrolled.
- `sticky` - Sticky positioning is a hybrid of relative and fixed positioning. The element is treated as `relative` positioned until it crosses a specified threshold, at which point it is treated as `fixed` positioned.

###### References

- https://developer.mozilla.org/en/docs/Web/CSS/position

#### The 'C' in CSS stands for Cascading. How is priority determined in assigning styles (a few examples)? How can you use this system to your advantage?

Browser determines what styles to show on an element depending on the specificity of CSS rules. We assume that the browser has already determined the rules that match a particular element. Among the matching rules, the specificity, four comma-separate values, `a, b, c, d` are calculated for each rule based on the following:

1. `a` is whether inline styles are being used. If the property declaration is an inline style on the element, `a` is 1, else 0.
2. `b` is the number of ID selectors.
3. `c` is the number of classes, attributes and pseudo-classes selectors.
4. `d` is the number of tags and pseudo-elements selectors.

The resulting specificity is not a score, but a matrix of values that can be compared column by column. When comparing selectors to determine which has the highest specificity, look from left to right, and compare the highest value in each column. So a value in column `b` will override values in columns `c` and `d`, no matter what they might be. As such, specificity of `0,1,0,0` would be greater than one of `0,0,10,10`.

In the cases of equal specificity: the latest rule is the one that counts. If you have written the same rule into your style sheet (regardless of internal or external) twice, then the lower rule in your style sheet is closer to the element to be styled, it is deemed to be more specific and therefore will be applied.

I would write CSS rules with low specificity so that they can be easily overridden if necessary. When writing CSS UI component library code, it is important that they have low specificities so that users of the library can override them without using too complicated CSS rules just for the sake of increasing specificity or resorting to `!important`.

###### References

- https://www.smashingmagazine.com/2007/07/css-specificity-things-you-should-know/
- https://www.sitepoint.com/web-foundations/specificity/

#### What existing CSS frameworks have you used locally, or in production? How would you change/improve them?

- **Bootstrap** - Slow release cycle. Bootstrap 4 has been in alpha for almost 2 years. Add a spinner button component, as it is widely-used.
- **Semantic UI** - Source code structure makes theme customization is extremely hard to understand. Painful to customize with unconventional theming system. Hardcoded config path within the vendor library. Not well-designed for overriding variables unlike in Bootstrap.
- **Bulma** - A lot of non-semantic and superfluous classes and markup required. Not backward compatible. Upgrading versions breaks the app in subtle manners.

#### Have you played around with the new CSS Flexbox or Grid specs?

Yes. Flexbox is mainly meant for 1-dimensional layouts while Grid is meant for 2-dimensional layouts.

Flexbox solves many common problems in CSS, such as vertical centering of elements within a container, sticky footer, etc. Bootstrap and Bulma are based on Flexbox, and it is probably the recommended way to create layouts these days. Have tried Flexbox before but ran into some browser incompatibility issues (Safari) in using `flex-grow`, and I had to rewrite my code using `inline-blocks` and math to calculate the widths in percentages, it wasn't a nice experience.

Grid is by far the most intuitive approach for creating grid-based layouts (it better be!) but browser support is not wide at the moment.

###### References

- https://philipwalton.github.io/solved-by-flexbox/

#### How is responsive design different from adaptive design?

Both responsive and adaptive design attempt to optimize the user experience across different devices, adjusting for different viewport sizes, resolutions, usage contexts, control mechanisms, and so on.

Responsive design works on the principle of flexibility - a single fluid website that can look good on any device. Responsive websites use media queries, flexible grids, and responsive images to create a user experience that flexes and changes based on a multitude of factors. Like a single ball growing or shrinking to fit through several different hoops.

Adaptive design is more like the modern definition of progressive enhancement. Instead of one flexible design, adaptive design detects the device and other features, and then provides the appropriate feature and layout based on a predefined set of viewport sizes and other characteristics. The site detects the type of device used, and delivers the pre-set layout for that device. Instead of a single ball going through several different-sized hoops, you'd have several different balls to use depending on the hoop size.

###### References

- https://developer.mozilla.org/en-US/docs/Archive/Apps/Design/UI_layout_basics/Responsive_design_versus_adaptive_design
- http://mediumwell.com/responsive-adaptive-mobile/
- https://css-tricks.com/the-difference-between-responsive-and-adaptive-design/

#### Have you ever worked with retina graphics? If so, when and what techniques did you use?

I tend to use higher resolution graphics (twice the display size) to handle retina display. The better way would be to use a media query like `@media only screen and (min-device-pixel-ratio: 2) { ... }` and change the `background-image`.

For icons, I would also opt to use svgs and icon fonts where possible, as they render very crisply regardless of resolution.

Another method would be to use JavaScript to replace the `<img>` `src` attribute with higher resolution versions after checking the `window.devicePixelRatio` value.

###### References

- https://www.sitepoint.com/css-techniques-for-retina-displays/

#### Is there any reason you'd want to use `translate()` instead of `absolute` positioning, or vice-versa? And why?

`translate()` is a value of CSS `transform`. Changing `transform` or `opacity` does not trigger browser reflow or repaint, only compositions, whereas changing the absolute positioning triggers `reflow`. `transform` causes the browser to create a GPU layer for the element but changing absolute positioning properties uses the CPU. Hence `translate()` is more efficient and will result in shorter paint times for smoother animations.

When using `translate()`, the element still takes up its original space (sort of like `position: relative`), unlike in changing the absolute positioning.

###### References

- https://www.paulirish.com/2012/why-moving-elements-with-translate-is-better-than-posabs-topleft/

### Other Answers

- https://neal.codes/blog/front-end-interview-css-questions
- http://jgthms.com/css-interview-questions-and-answers.html
- https://quizlet.com/28293152/front-end-interview-questions-css-flash-cards/
- http://peterdoes.it/2015/12/03/a-personal-exercise-front-end-job-interview-questions-and-my-answers-all/

## JS Questions

Answers to [Front-end Job Interview Questions - JS Questions](https://github.com/h5bp/Front-end-Developer-Interview-Questions#js-questions). Pull requests for suggestions and corrections are welcome!

#### Explain event delegation

Event delegation is a technique involving adding event listeners to a parent element instead of adding them to the descendant elements. The listener will fire whenever the event is triggered on the descendant elements due to event bubbling up the DOM. The benefits of this technique are:

- Memory footprint goes down because only one single handler is needed on the parent element, rather than having to attach event handlers on each descendant.
- There is no need to unbind the handler from elements that are removed and to bind the event for new elements.

###### References

- https://davidwalsh.name/event-delegate
- https://stackoverflow.com/questions/1687296/what-is-dom-event-delegation

#### Explain how `this` works in JavaScript

There's no simple explanation for `this`; it is one of the most confusing concepts in JavaScript. A hand-wavey explanation is that the value of `this` depends on how the function is called. I have read many explanations on `this` online, and I found [Arnav Aggrawal](https://medium.com/@arnav_aggarwal)'s explanation to be the clearest. The following rules are applied:

1. If the `new` keyword is used when calling the function, `this` inside the function is a brand new object.
2. If `apply`, `call`, or `bind` are used to call/create a function, `this` inside the function is the object that is passed in as the argument.
3. If a function is called as a method, such as `obj.method()` — `this` is the object that the function is a property of.
4. If a function is invoked as a free function invocation, meaning it was invoked without any of the conditions present above, `this` is the global object. In a browser, it is the `window` object. If in strict mode (`'use strict'`), `this` will be `undefined` instead of the global object.
5. If multiple of the above rules apply, the rule that is higher wins and will set the `this` value.
6. If the function is an ES2015 arrow function, it ignores all the rules above and receives the `this` value of its surrounding scope at the time it is created.

For an in-depth explanation, do check out his [article on Medium](https://codeburst.io/the-simple-rules-to-this-in-javascript-35d97f31bde3).

###### References

- https://codeburst.io/the-simple-rules-to-this-in-javascript-35d97f31bde3
- https://stackoverflow.com/a/3127440/1751946

#### Explain how prototypal inheritance works

This is an extremely common JavaScript interview question. All JavaScript objects have a `prototype` property, that is a reference to another object. When a property is accessed on an object and if the property is not found on that object, the JavaScript engine looks at the object's `prototype`. and the `prototype`'s `prototype` and so on, until it finds the property defined on one of the `prototype`s or until it reaches the end of the prototype chain. This behaviour simulates classical inheritance, but it is really more of [delegation than inheritance](https://davidwalsh.name/javascript-objects).

###### References

- https://www.quora.com/What-is-prototypal-inheritance/answer/Kyle-Simpson
- https://davidwalsh.name/javascript-objects

#### What do you think of AMD vs CommonJS?

Both are ways to implement a module system, which was not natively present in JavaScript until ES2015 came along. CommonJS is synchronous while AMD (Asynchronous Module Definition) is obviously asynchronous. CommonJS is designed with server-side development in mind while AMD, with its support for asynchronous loading of modules, is more intended for browsers.

I find AMD syntax to be quite verbose and CommonJS is closer to the style you would write import statements in other languages. Most of the time, I find AMD unnecessary, because if you served all your JavaScript into one concatenated bundle file, you wouldn't benefit from the async loading properties. Also, CommonJS syntax is closer to Node style of writing modules and there is less context-switching overhead when switching between client side and server side JavaScript development.

I'm glad that with ES2015 modules, that has support for both synchronous and asynchronous loading, we can finally just stick to one approach. Although it hasn't been fully rolled out in browsers and in Node, we can always use transpilers to convert our code.

###### References

- https://auth0.com/blog/javascript-module-systems-showdown/
- https://stackoverflow.com/questions/16521471/relation-between-commonjs-amd-and-requirejs

#### Explain why the following doesn't work as an IIFE: `function foo(){ }();`. What needs to be changed to properly make it an IIFE?

IIFE stands for Immediately Invoked Function Expressions. The JavaScript parser reads `function foo(){ }();` as `function foo(){ }` and `();`, where the former is a function declaration and the latter (a pair of brackets) is an attempt at calling a function but there is no name specified, hence it throws `Uncaught SyntaxError: Unexpected token )`.

Here are two ways to fix it that involves adding more brackets: `(function foo(){ })()` and `(function foo(){ }())`. These functions are not exposed in the global scope and you can even omit its name if you do not need to reference itself within the body.

###### References

- http://lucybain.com/blog/2014/immediately-invoked-function-expression/

#### What's the difference between a variable that is: `null`, `undefined` or undeclared? How would you go about checking for any of these states?

**Undeclared** variables are created when you assign to a value to an identifier that is not previously created using `var`, `let` or `const`. Undeclared variables will be defined globally, outside of the current scope. In strict mode, a `ReferenceError` will be thrown when you try to assign to an undeclared variable. Undeclared variables are bad just like how global variables are bad. Avoid them at all cost! To check for them, wrap its usage in a `try`/`catch` block.

```js
function foo() {
  x = 1;   // Throws a ReferenceError in strict mode
}

foo()
console.log(x) // 1
```

A variable that is `undefined` is a variable that has been declared, but not assigned a value. It is of type `undefined`. If a function does not return any value as the result of executing it is assigned to a variable, the variable also has the value of `undefined`. To check for it, compare using the strict equality (`===`) operator or `typeof` which will give the `'undefined'` string. Note that you should not be using the abstract equality operator to check, as it will also return `true` if the value is `null`.

```js
var foo;
console.log(foo); // undefined
console.log(foo === undefined); // true
console.log(typeof foo === 'undefined'); // true

console.log(foo == null); // true. Wrong, don't use this to check!

function bar() {}
var baz = bar();
console.log(baz === undefined); // undefined
```

A variable that is `null` will have been explicitly assigned to the `null` value. It represents no value and is different from `undefined` in the sense that it has been explicitly assigned. To check for `null,` simply compare using the strict equality operator. Note that like the above, you should not be using the abstract equality operator (`==`) to check, as it will also return `true` if the value is `undefined`.

```
var foo = null;
console.log(foo === null); // true

console.log(foo == undefined); // true. Wrong, don't use this to check!
```

As a personal habit, I never leave my variables undeclared or unassigned. I will explicitly assign `null` to them after declaring, if I don't intend to use it yet.

###### References

- https://stackoverflow.com/questions/15985875/effect-of-declared-and-undeclared-variables
- https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/undefined

#### What is a closure, and how/why would you use one?

TODO

#### What's a typical use case for anonymous functions?

They can be used in IIFEs to encapsulate some code within a local scope so that variables declared in it do not leak to the global scope.

```
(function() {
  // Some code here.
})();
```

As a callback that is used once and does not need to be used anywhere else. The code will seem more self-contained and readable when handlers are defined right inside the code calling them, rather than having to search elsewhere to find the function body.

```
setTimeout(function () {
  console.log('Hello world!');
}, 1000);
```

Arguments to functional programming constructs or Lodash (similar to callbacks).

```
const arr = [1, 2, 3];
const double = arr.map(function (el) {
  return el * 2;
});
console.log(double); // [2, 4, 6]
```

###### References

- https://www.quora.com/What-is-a-typical-usecase-for-anonymous-functions
- https://stackoverflow.com/questions/10273185/what-are-the-benefits-to-using-anonymous-functions-instead-of-named-functions-fo

#### How do you organize your code? (module pattern, classical inheritance?)

TODO

#### What's the difference between host objects and native objects?

Native objects are objects that are part of the JavaScript language defined by the ECMAScript specification, such as `String`, `Math`, `RegExp`, `Object`, `Function`, etc.

Host objects are provided by the runtime environment (browser or Node), such as `window`, `XMLHTTPRequest`, etc.

###### References

- https://stackoverflow.com/questions/7614317/what-is-the-difference-between-native-objects-and-host-objects

#### Difference between: `function Person(){}`, `var person = Person()`, and `var person = new Person()`?

This question is pretty vague. My best guess at its intention is that it is asking about constructors in JavaScript. Technically speaking, `function Person(){}` is just a normal function declaration. The convention is use PascalCase for functions that are intended to be used as constructors.

`var person = Person()` invokes the `Person` as a function, and not as a constructor. Invoking as such is a common mistake if it the function is intended to be used as a constructor. Typically, the constructor does not return anything, hence invoking the constructor like a normal function will return `undefined` and that gets assigned to the variable intended as the instance.

`var person = new Person()` creates an instance of the `Person` object using the `new` operator, which inherits from `Person.prototype`. An alterative would be to use `Object.create`, such as: `Object.create(Person.prototype)`.

```js
function Person(name) {
  this.name = name;
}

var person = Person('John');
console.log(person); // undefined
console.log(person.name); // Uncaught TypeError: Cannot read property 'name' of undefined

var person = new Person('John');
console.log(person); // Person { name: "John" }
console.log(person.name); // "john"
```

###### References

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new

#### What's the difference between `.call` and `.apply`?

Both `.call` and `.apply` are used to invoke functions and the first parameter will be used as the value of `this` within the function. However, `.call` takes in a comma-separated arguments as the next arguments while `.apply` takes in an array of arguments as the next argument. An easy way to remember this is C for `call` and comma-separated and A for `apply` and array of arguments.

```js
function add(a, b) {
  return a + b;
}

console.log(add.call(null, 1, 2)) // 3
console.log(add.apply(null, [1, 2])) // 3
```

#### Explain `Function.prototype.bind`.

Taken word-for-word from [MDN](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_objects/Function/bind):

> The `bind()` method creates a new function that, when called, has its this keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called.

In my experience, it is most useful for binding the value of `this` in methods of classes that you want to pass into other functions. This is frequently done in React components.

###### References

- https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_objects/Function/bind

#### When would you use `document.write()`?

`document.write()` writes a string of text to a document stream opened by `document.open()`. When `document.write()` is executed after the page has loaded, it will call `document.open` which clears the whole document (`<head>` and `<body>` removed!) and replaces the contents with the given parameter value in string. Hence it is usually considered dangerous and prone to misuse.

There are some answers online that explain `document.write()` is being used in analytics code or [when you want to include styles that should only work if JavaScript is enabled](https://www.quirksmode.org/blog/archives/2005/06/three_javascrip_1.html). It is even being used in HTML5 boilerplate to [load scripts in parallel and preserve execution order](https://github.com/paulirish/html5-boilerplate/wiki/Script-Loading-Techniques#documentwrite-script-tag)! However, I suspect those reasons might be outdated and in the modern day, they can be achieved without using `document.write()`. Please do correct me if I'm wrong about this.

###### References

- https://www.quirksmode.org/blog/archives/2005/06/three_javascrip_1.html
- https://github.com/h5bp/html5-boilerplate/wiki/Script-Loading-Techniques#documentwrite-script-tag

#### What's the difference between feature detection, feature inference, and using the UA string?

TODO

#### Explain Ajax in as much detail as possible.

TODO

#### What are the advantages and disadvantages of using Ajax?

TODO

#### Explain how JSONP works (and how it's not really Ajax).

TODO

#### Have you ever used JavaScript templating? If so, what libraries have you used?

Yes. Handlebars, Underscore, Lodash, AngularJS and JSX. I disliked templating in AngularJS because it made heavy use of strings in the directives and typos would go uncaught. JSX is my new favourite as it is closer to JavaScript and there is barely and syntax to be learnt. Nowadays, you can even use ES2015 template string literals as a quick way for creating templates without relying on third-party code.

```
const template = `<div>My name is: ${name}</div>`;
```

However, do beware of a potential XSS in the above approach as the contents are not escaped for you, unlike in templating libraries.

#### Explain "hoisting".

Hoisting is a term used to explain the behavior of variable declarations in your code. Variables declared or initialized with the `var` keyword will have their declaration "hoisted" up to the top of the current scope. However, only the declaration is hoisted, the assignment (if there is one), will stay where it is. Let's explain with a few examples.

```
// var declarations are hoisted.
console.log(foo); // undefined
var foo = 1;
console.log(foo); // 1

// let/const declarations are NOT hoisted.
console.log(bar); // ReferenceError: bar is not defined
let bar = 2;
console.log(bar); // 2
```

Function declarations have the body hoisted while the function expressions (written in the form of variable declarations) only has the variable declaration hoisted.

```
// Function Declaration
console.log(foo); // [Function: foo]
foo(); // 'FOOOOO'
function foo() {
  console.log('FOOOOO');
}
console.log(foo); // [Function: foo]

// Function Expression
console.log(bar); // undefined
bar(); // Uncaught TypeError: bar is not a function
var bar = function() {
  console.log('BARRRR');
}
console.log(bar); // [Function: bar]
```

#### Describe event bubbling.

When an event triggers on a DOM element, it will attempt to handle the event if there is a listener attached, then the event is bubbled up to its parent and the same thing happens. This bubbling occurs up the element's ancestors all the way to the `document`. Event bubbling is the mechanism behind event delegation.

#### What's the difference between an "attribute" and a "property"?

Attributes are defined on the HTML markup but properties are defined on the DOM. To illustrate the difference, imagine we have this text field in our HTML: `<input type="text" value="Hello">`.

```
const input = document.querySelector('input');
console.log(input.getAttribute('value')); // Hello
console.log(input.value); // Hello
```

But after you change the value of the text field by adding "World!" to it, this becomes:

```
console.log(input.getAttribute('value')); // Hello
console.log(input.value); // Hello World!
```

###### References

- https://stackoverflow.com/questions/6003819/properties-and-attributes-in-html

#### Why is extending built-in JavaScript objects not a good idea?

Extending a built-in/native JavaScript object means adding properties/functions to its `prototype`. While this may seem like a good idea at first, it is dangerous in practice. Imagine your code uses a few libraries that both extend the `Array.prototype` by adding the same `contains` method, the implementations will overwrite each other and your code will break if the behavior of these two methods are not the same.

The only time you may want to extend a native object is when you want to create a polyfill, essentially providing your own implementation for a method that is part of the JavaScript specification but might not exist in the user's browser due to it being an older browser.

###### References

- http://lucybain.com/blog/2014/js-extending-built-in-objects/

#### Difference between document load event and document DOMContentLoaded event?

The `DOMContentLoaded` event is fired when the initial HTML document has been completely loaded and parsed, without waiting for stylesheets, images, and subframes to finish loading.

`window`'s `load` event is only fired after the DOM and all dependent resources and assets have loaded.

###### References

- https://developer.mozilla.org/en-US/docs/Web/Events/DOMContentLoaded
- https://developer.mozilla.org/en-US/docs/Web/Events/load

#### What is the difference between `==` and `===`?

`==` is the abstract equality operator while `===` is the strict equality operator. The `==` operator will compare for equality after doing any necessary type conversions. The `===` operator will not do type conversion, so if two values are not the same type `===` will simply return `false`. When using `==`, funky things can happen, such as:

```js
1 == '1' // true
1 == [1] // true
1 == true // true
0 == '' // true
0 == '0' // true
0 == false // true
```

My advice is never to use the `==` operator, except for convenience when comparing against `null` or `undefined`, where `a == null` will return `true` if `a` is `null` or `undefined`.

```js
var a = null;
console.log(a == null); // true
console.log(a == undefined); // true
```

###### References

- https://stackoverflow.com/questions/359494/which-equals-operator-vs-should-be-used-in-javascript-comparisons

#### Explain the same-origin policy with regards to JavaScript.

TODO

#### Make this work:

```js
duplicate([1,2,3,4,5]); // [1,2,3,4,5,1,2,3,4,5]
```

```js
function duplicate(arr) {
  return arr.concat(arr);
}

duplicate([1,2,3,4,5]); // [1,2,3,4,5,1,2,3,4,5]
```

#### Why is it called a Ternary expression, what does the word "Ternary" indicate?

"Ternary" indicates three, and a ternary expression accepts three operands, the test condition, the "then" expression and the "else" expression. Ternary expressions are not specific to JavaScript and I'm not sure why it is even in this list.

###### References

- https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Conditional_Operator

#### What is `"use strict";`? What are the advantages and disadvantages to using it?

'use strict' is a statement used to enable strict mode to entire scripts or individual functions. Strict mode is a way to opt in to a restricted variant of JavaScript.

Advantages:

- Makes it impossible to accidentally create global variables.
- Makes assignments which would otherwise silently fail to throw an exception.
- Makes attempts to delete undeletable properties throw (where before the attempt would simply have no effect).
- Requires that function parameter names be unique.
- `this` is undefined in the global context.
- It catches some common coding bloopers, throwing exceptions.
- It disables features that are confusing or poorly thought out.

Disadvantages:

- Many missing features that some developers might be used to.
- No more access to `function.caller` and `function.arguments`.
- Concatenation of scripts written in different strict modes might cause issues.

Overall, I think the benefits outweigh the disadvantages, and I never had to rely on the features that strict mode blocks. I would recommend using strict mode.

###### References

- http://2ality.com/2011/10/strict-mode-hatred.html
- http://lucybain.com/blog/2014/js-use-strict/

#### Create a for loop that iterates up to `100` while outputting **"fizz"** at multiples of `3`, **"buzz"** at multiples of `5` and **"fizzbuzz"** at multiples of `3` and `5`.

Check out this version of FizzBuzz by [Paul Irish](https://gist.github.com/jaysonrowe/1592432#gistcomment-790724).

```js
for (let i = 1; i <= 100; i++) {
  let f = i % 3 == 0, b = i % 5 == 0;
  console.log(f ? (b ? 'FizzBuzz' : 'Fizz') : (b ? 'Buzz' : i));
}
```

I would not advise you to write the above during interviews though. Just stick with the long but clear approach. For more wacky versions of FizzBuzz, check out the reference link below.

###### References

- https://gist.github.com/jaysonrowe/1592432

#### Why is it, in general, a good idea to leave the global scope of a website as-is and never touch it?

Every script has access to the global scope, and if everyone is using the global namespace to define their own variables, there will bound to be collisions. Use the module pattern (IIFEs) to encapsulate your variables within a local namespace.

#### Why would you use something like the `load` event? Does this event have disadvantages? Do you know any alternatives, and why would you use those?

TODO

#### Explain what a single page app is and how to make one SEO-friendly.

The below is taken from the awesome [Grab Front End Guide](https://github.com/grab/front-end-guide), which coincidentally, is written by me!

Web developers these days refer to the products they build as web apps, rather than websites. While there is no strict difference between the two terms, web apps tend to be highly interactive and dynamic, allowing the user to perform actions and receive a response for their action. Traditionally, the browser receives HTML from the server and renders it. When the user navigates to another URL, a full-page refresh is required and the server sends fresh new HTML for the new page. This is called server-side rendering.

However in modern SPAs, client-side rendering is used instead. The browser loads the initial page from the server, along with the scripts (frameworks, libraries, app code) and stylesheets required for the whole app. When the user navigates to other pages, a page refresh is not triggered. The URL of the page is updated via the [HTML5 History API](https://developer.mozilla.org/en-US/docs/Web/API/History_API). New data required for the new page, usually in JSON format, is retrieved by the browser via [AJAX](https://developer.mozilla.org/en-US/docs/AJAX/Getting_Started) requests to the server. The SPA then dynamically updates the page with the data via JavaScript, which it has already downloaded in the initial page load. This model is similar to how native mobile apps work.

The benefits:

- The app feels more responsive and users do not see the flash between page navigations due to full-page refreshes.
- Fewer HTTP requests are made to the server, as the same assets do not have to be downloaded again for each page load.
- Clear separation of the concerns between the client and the server; you can easily build new clients for different platforms (e.g. mobile, chatbots, smart watches) without having to modify the server code. You can also modify the technology stack on the client and server independently, as long as the API contract is not broken.

The downsides:

- Heavier initial page load due to loading of framework, app code, and assets required for multiple pages.
- There's an additional step to be done on your server which is to configure it to route all requests to a single entry point and allow client-side routing to take over from there.
- SPAs are reliant on JavaScript to render content, but not all search engines execute JavaScript during crawling, and they may see empty content on your page. This inadvertently hurts the Search Engine Optimization (SEO) of your app. However, most of the time, when you are building apps, SEO is not the most important factor, as not all the content needs to be indexable by search engines. To overcome this, you can either server-side render your app or use services such as [Prerender](https://prerender.io/) to "render your javascript in a browser, save the static HTML, and return that to the crawlers".

###### References

- https://github.com/grab/front-end-guide#single-page-apps-spas
- http://stackoverflow.com/questions/21862054/single-page-app-advantages-and-disadvantages
- http://blog.isquaredsoftware.com/presentations/2016-10-revolution-of-web-dev/
- https://medium.freecodecamp.com/heres-why-client-side-rendering-won-46a349fadb52

#### What is the extent of your experience with Promises and/or their polyfills?

TODO

#### What are the pros and cons of using Promises instead of callbacks?

TODO

#### What are some of the advantages/disadvantages of writing JavaScript code in a language that compiles to JavaScript?

Some examples of languages that compile to JavaScript include CoffeeScript, Elm, ClojureScript, PureScript and TypeScript.

Advantages:

- Fixes some of the longstanding problems in JavaScript and discourages JavaScript anti-patterns.
- Enables you to write shorter code, by providing some syntactic sugar on top of JavaScript, which I think ES5 lacks, but ES2015 is awesome.
- Static types are awesome (in the case of TypeScript) for large projects that need to be maintained over time.

Disadvantages:

- Require a build/compile process as browsers only run JavaScript and your code will need to be compiled into JavaScript before being served to browsers.
- Debugging can be a pain if your source maps do not map nicely to your pre-compiled source.
- Most developers are not familiar with these languages and will need to learn it. There's a ramp up cost involved for your team if you use it for your projects.
- Smaller community (depends on the language), which means resources, tutorials, libraries and tooling would be harder to find.
- IDE/editor support might be lacking.
- These languages will always be behind the latest JavaScript standard.
- Developers should be cognizant of what their code is being compiled to — because that is what would actually be running, and that is what matters in the end.

Practically, ES2015 has vastly improved JavaScript and made it much nicer to write. I don't really see the need for CoffeeScript these days.

#### References

- https://softwareengineering.stackexchange.com/questions/72569/what-are-the-pros-and-cons-of-coffeescript

#### What tools and techniques do you use debugging JavaScript code?

TODO

#### What language constructions do you use for iterating over object properties and array items?

For objects:

- `for` loops - `for (var property in obj) { console.log(property); }`. However, this will also iterate through its inherited properties, and you will add an `obj.hasOwnProperty(property)` check before using it.
- `Object.keys()` - `Object.keys(obj).forEach(function (property) { ... })`. `Object.keys()` is a static method that will lists all enumerable properties of the object that you pass it.

For arrays:

- `for` loops - `for (var i = 0; i < arr.length; i++)`. The common pitfall here is that `var` is in the function scope and not the block scope and most of the time you would want block scoped iterator variable. ES2015 introduces `let` which has block scope and it is recommended to use that instead. So this becomes: `for (let i = 0; i < arr.length; i++)`.
- `forEach` - `arr.forEach(function (el, index) { ... })`. This construct can be more convenient at times because you do not have to use the `index` if all you need is the array elements. There are also the `every` and `some` methods which will allow you to terminate the iteration early.

Most of the time, I would prefer the `.forEach` method, but it really depends on what you are trying to do. `for` loops allow more flexibility, such as prematurely terminate the loop using `break` or incrementing the iterator more than once per loop.


#### Explain the difference between mutable and immutable objects.

- What is an example of an immutable object in JavaScript?
- What are the pros and cons of immutability?
- How can you achieve immutability in your own code?

TODO

#### Explain the difference between synchronous and asynchronous functions.

TODO

#### What is event loop? What is the difference between call stack and task queue?

The event loop is a single-threaded loop that monitors the call stack and checks if there is any work to be done in the task queue. If the call stack is empty and there are callback functions in the task queue, a function is dequeued and pushed onto the call stack to be executed.

If you haven't already checked out Philip Robert's [talk on the Event Loop](https://2014.jsconf.eu/speakers/philip-roberts-what-the-heck-is-the-event-loop-anyway.html), you should. It is one of the most viewed videos on JavaScript.

###### References

- https://2014.jsconf.eu/speakers/philip-roberts-what-the-heck-is-the-event-loop-anyway.html
- http://theproactiveprogrammer.com/javascript/the-javascript-event-loop-a-stack-and-a-queue/

#### Explain the differences on the usage of `foo` between `function foo() {}` and `var foo = function() {}`

The former is a function declaration while the latter is a function expression. The key difference is that function declarations have its body hoisted but the bodies of function expressions are not (they have the same hoisting behaviour as variables). For more explanation on hoisting, refer to the question above on hoisting. If you try to invoke a function expression before it is defined, you will get an `Uncaught TypeError: XXX is not a function` error.

**Function Declaration**

```js
foo(); // 'FOOOOO'
function foo() {
  console.log('FOOOOO');
}
```

**Function Expression**

```js
foo(); // Uncaught TypeError: foo is not a function
var foo = function() {
  console.log('FOOOOO');
}
```

###### References

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function

### Other Answers

- http://flowerszhong.github.io/2013/11/20/javascript-questions.html
