## taro-github-rank

> 为了方便能够方便地查看github当前最受关注的人和仓库，决定通过这个项目来实现

### GraphQL请求示例

> Connections是可以进行检索的

#### 仓库相关信息

```
query {
  repository(owner:"lsqy", name:"taro-music") {
    forkCount,
    description,
    createdAt,
    stargazers {
      totalCount
    },
    issues(orderBy:{field: UPDATED_AT, direction: DESC} , labels: null, first: 10) {
      edges{
        cursor
        node{
          title
          updatedAt
          number
        }
      }
    }
    labels(first: 20){
      nodes{
        name
      }
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

- 中国top50最受关注

```
query {
  search(query:"location:China", type: USER, first: 50, after: null) {
    edges{
      cursor
      node{
        ... on User {
          name,
          email,
          websiteUrl,
          url,
          location,
          isHireable,
          viewerIsFollowing,
          bio,
          followers(first: 10) {
            edges{
              cursor
              node {
                login
              }
            },
            nodes {
              login
            },
            pageInfo {
              endCursor,
              hasNextPage,
              hasPreviousPage,
              startCursor
            },
            totalCount
          }
        }
      }
    }
  }
}
```