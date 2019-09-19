## GraphQL介绍

### GraphQL术语

&nbsp;&nbsp;`GitHub GraphQL API v4`代表了从`GitHub REST API v3`到架构和概念的转变。您可能会在`GraphQL API v4`参考文档中遇到一些新的术语。

### Schema

`Schema`定义了`GraphQL API`的类型系统。它描述了客户端可能访问的所有完整数据集(对象、字段、关系等其他)。来自客户端的调用将根据`Schema`进行验证和执行。客户端可以通过内省找到关于`Schema`的信息。`Schema`驻留在`GraphQL API`服务器上。有关更多信息，请参见“[发现GraphQL API](https://developer.github.com/v4/guides/intro-to-graphql/#discovering-the-graphql-api)”。

### Field（字段）

字段（`Field`）是可以从对象中检索的数据单元。正如官方的`GraphQL`文档所说:“GraphQL查询语言基本上是在对象上选择相应的字段。”

官方也这样去描述字段（`Field`）:

> 所有的`GraphQL`操作都必须明确指定其选择的字段是一个标量值，以确保可以得到一个明确的响应。

这就意味这如果你尝试返回一个不是标量值的字段，那么模式匹配就会抛出一个错误，你必须添加嵌套子字段，直到所有字段都返回标量值。

### Argument（参数）

参数是一组附加到特定字段的键值对。有些字段需要参数。`Mutations`需要输入对象作为参数。

### Implementation (引用)

一个`GrapQL schema`可以使用`implements`实现一个对象从一个接口中继承。

下面是一个定义接口X和对象Y的`schema`的人为例子:

```
interface X {
  some_field: String!
  other_field: String!
}

type Y implements X {
  some_field: String!
  other_field: String!
  new_field: String!
}

```
这意味着当对象Y添加特定于对象Y的新字段时，对象Y需要与接口X相同的字段/参数/返回类型。!表示字段是必需的。

在参考文档中，您会发现:

- 每个对象都列出了它在implementation下继承的接口。
- 每个接口都列出了在实现下从它继承的对象。

### 探索 GraphQL API

> GraphQL是可以自查的。这意味着您可以查询GraphQL模式以获得关于自身的详细信息。

- 查询`_schema`列出模式中定义的所有类型，并获取每个类型的详细信息:

```
query {
  __schema {
    types {
      name
      kind
      description
      fields {
        name
      }
    }
  }
}
```

- 查询`_type`获取任何类型的详细信息:

```
query {
  __type(name: "Repository") {
    name
    kind
    description
    fields {
      name
    }
  }
}

```

- 您还可以通过GET请求运行模式的自身查询:

```
curl -H "Authorization: bearer token" https://api.github.com/graphql
```

你会得到一个`json`的结果集,你可以通过你常用的工具美化显示

