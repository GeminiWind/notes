# GraphQL

## TypeDef

```js
const typeDefs = `
  type Query {
    info: String!
    feed: [Link!]!
  }

  type Link {
    id: ID!
    description: String!
    url: String!
  }
`
```

## Query
```
type Query {
    info: String!
    feed: [Link!]!
  }

```

## Mutation

```
type Mutation {
    post(url: String!, description: String!): Link!
  }
```

## Resolver

```js
const resolvers = {
  Query: {
    info: () => `This is the API of a Hackernews Clone`
  },
  Mutation: {
	post: (parent, args) => {
  
    let idCount = links.length

       const link = {
        id: `link-${idCount++}`,
        description: args.description,
        url: args.url,
      }
      links.push(link)
      return link
    }
  }
}
```

