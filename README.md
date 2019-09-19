## taro-github-rank

> 为了方便能够方便地查看github当前最受关注的人和仓库，决定通过这个项目来实现

### GraphQL请求示例

#### 仓库相关信息

```
query {
  repository(owner:"lsqy", name:"taro-music") {
    forkCount,
    description,
    createdAt,
    stargazers {
      totalCount
    }
  }
}

```

#### 用户相关信息

```
query {
  user(login:"lsqy") {
    name,
    avatarUrl,
    login,
    location,
    id,
    company,
    bio
  }
}

```