## 命令

在 Allay 模板中，使用 `{- -}` 表示命令块，使用 `{: :}` 表示表达式块。所有表达式块都会被求值并替换为其结果。

Allay 模板支持多种命令，用于控制模板渲染流程。

### `set`

`set` 指令用于在当前作用域创建变量。

```html
{- set $var .something -}
{: $var :} <!-- 使用变量 -->
```

`set` 指令将当前作用域变量（即 `this`）的 `something` 字段赋值给变量 `$var`，之后可以在模板中使用该变量。

### `get`

`get` 指令用于返回当前作用域中的变量。但通常可以省略，因为变量会自动解析。

```html
{: get $var :}
{: $var :} <!-- 等价于上面 -->
```

### `for`

`for` 指令用于遍历列表。如果变量不是列表或不存在，则会抛出错误。

```html
<ul>
    {- for $player: .players -}
    <!-- 为 .players 中的每个项创建变量 $player -->
    <li>
    {: $player.name :}
    </li>
    {- end -}
</ul>
```

也可以通过提供第二个变量访问当前项的索引：

```html
<ul>
    {- for $player, $index: .players -}
    <!-- 支持索引，从 0 开始 -->
    <li>
    {: $index + 1 :}: {: $player.name :}
    </li>
    {- end -}
</ul>
```

### `with`

`with` 指令用于通过对象进入子[作用域](./scope.md)。如果对象不存在，则会跳过。

```html
{- with .author -}
<p>{: .name :}</p>
{- end -}
```

### `if` 和 `else`

`if` 指令用于条件渲染内容。如果条件不为 null 且为 true，则渲染内容，否则跳过。可以使用 `else` 提供备选内容。

```html
{- if .is_admin -}
<p>Admin</p>
{- else -}
<p>User</p>
{- end -}
```

### `end`

`end` 指令用于结束命令块，如 `for`、`with` 或 `if`。

### `param`

`param` 指令用于访问传递给模板或include指令的参数。参数从0开始索引。

```html
<div class="say">{: param.0 :}</div>
<div class="author">{: param.1 :}</div>
```

### `include`

`include` 指令用于包含其他模板文件。

- 第一个参数是文件路径
- 第二个参数是要传递给包含模板的作用域（如果未提供，则使用当前作用域）
- 其他参数可传递给包含模板，并通过 `param` 访问

```html
{- include "header.html" -}
<!-- 使用当前作用域 -->
{- include "article/post.html" .post "My Post" -}
<!-- 传递 .post 作为作用域，"My Post" 作为参数 0 -->
```
