# 2.2.4 选择器

CSS 选择器的语法规则：

| 选择器 | 例子 | 例子描述 |
| :--- | :--- | :--- |
| .class | .intro | 选择 class="intro" 的所有节点。 |
| \#id | \#firstname | 选择 id="firstname" 的所有节点。 |
| \* | \* | 选择所有节点。 |
| element | p | 选择所有 p 节点。 |
| element,element | div,p | 选择所有 div 节点和所有 p 节点。 |
| element element | div p | 选择 div 节点内部的所有 p 节点。 |
| element&gt;element | div&gt;p | 选择父节点为 div 节点的所有 p 节点。 |
| element+element | div+p | 选择紧接在 div 节点之后的所有 p 节点。 |
| \[attribute\] | \[target\] | 选择带有 target 属性所有节点。 |
| \[attribute=value\] | \[target=blank\] | 选择 target="blank" 的所有节点。 |
| \[attribute~=value\] | \[title~=flower\] | 选择 title 属性包含单词 "flower" 的所有节点。 |
| :link | a:link | 选择所有未被访问的链接。 |
| :visited | a:visited | 选择所有已被访问的链接。 |
| :active | a:active | 选择活动链接。 |
| :hover | a:hover | 选择鼠标指针位于其上的链接。 |
| :focus | input:focus | 选择获得焦点的 input 节点。 |
| :first-letter | p:first-letter | 选择每个 p 节点的首字母。 |
| :first-line | p:first-line | 选择每个 p 节点的首行。 |
| :first-child | p:first-child | 选择属于父节点的第一个子节点的每个 p 节点。 |
| :before | p:before | 在每个 p 节点的内容之前插入内容。 |
| :after | p:after | 在每个 p 节点的内容之后插入内容。 |
| :lang\(language\) | p:lang | 选择带有以 "it" 开头的 lang 属性值的每个 p 节点。 |
| element1~element2 | p~ul | 选择前面有 p 节点的每个 ul 节点。 |
| \[attribute^=value\] | a\[src^="https"\] | 选择其 src 属性值以 "https" 开头的每个 a 节点。 |
| \[attribute$=value\] | a\[src$=".pdf"\] | 选择其 src 属性以 ".pdf" 结尾的所有 a 节点。 |
| \[attribute\*=value\] | a\[src\*="abc"\] | 选择其 src 属性中包含 "abc" 子串的每个 a 节点。 |
| :first-of-type | p:first-of-type | 选择属于其父节点的首个 p 节点的每个 p 节点。 |
| :last-of-type | p:last-of-type | 选择属于其父节点的最后 p 节点的每个 p 节点。 |
| :only-of-type | p:only-of-type | 选择属于其父节点唯一的 p 节点的每个 p 节点。 |
| :only-child | p:only-child | 选择属于其父节点的唯一子节点的每个 p 节点。 |
| :nth-child\(n\) | p:nth-child | 选择属于其父节点的第二个子节点的每个 p 节点。 |
| :nth-last-child\(n\) | p:nth-last-child | 同上，从最后一个子节点开始计数。 |
| :nth-of-type\(n\) | p:nth-of-type | 选择属于其父节点第二个 p 节点的每个 p 节点。 |
| :nth-last-of-type\(n\) | p:nth-last-of-type | 同上，但是从最后一个子节点开始计数。 |
| :last-child | p:last-child | 选择属于其父节点最后一个子节点每个 p 节点。 |
| :root | :root | 选择文档的根节点。 |
| :empty | p:empty | 选择没有子节点的每个 p 节点（包括文本节点）。 |
| :target | \#news:target | 选择当前活动的 \#news 节点。 |
| :enabled | input:enabled | 选择每个启用的 input 节点。 |
| :disabled | input:disabled | 选择每个禁用的 input 节点 |
| :checked | input:checked | 选择每个被选中的 input 节点。 |
| :not\(selector\) | p:not | 选择非 p 节点的每个节点。 |
| ::selection | ::selection | 选择被用户选取的节点部分。 |

