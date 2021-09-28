# GraphQL

## Type Definition

### Supported type definition

```graphql
type Book {
  title: String  # returns a String
  author: Author # returns an Author
	id: Int # return a signed 32‐bit integer
	isPublished: Boolean # return a Boolean (true or false)
	price: Float # signed double-precision floating-point value
}
```

### Required field / Optional field

You can mark the field as required by adding exclaimation mark `!`

For ex
```graphql
type Student {
	id: Int! # cannot be null
	name: String # can be null,
	friends: [Friend] # List of Friend
}
```

### Interface

```graphql
interface Book {
  title: String!
  author: Author!
}

type Textbook implements Book {
  title: String!
  author: Author!
  courses: [Course!]!
}

type ColoringBook implements Book {
  title: String!
  author: Author!
  colors: [String!]!
}

type Query {
  books: [Book!]!
}
```

Querying interface

```graphql
query GetBooks {
  books {
    # Querying for __typename is almost always recommended,
    # but it's even more important when querying a field that
    # might return one of multiple types.
    __typename
    title
    ... on Textbook {
      courses { # Only present in Textbook
        name
      }
    }
    ... on ColoringBook {
      colors # Only present in ColoringBook
    }
  }
}
```

## Query
```graphql
type Query {
    info: String!
    feed: [Link!]!
  }

```

## Mutation

```graphql
type Mutation {
	post(url: String!, description: String!): Link!
}
```


### input

In case you want to specify input as object for your mutation, you can add `input` for  your mutation

```graphql
input AddPostInput {
  url: String!
	description: String!
}

type Mutation {
	post(input: AddPostInput): Link!
}
```

## Resolver

```js
const resolvers = {
  Query: {
    info: () => `This is the API of a Hackernews Clone`
  },
  Mutation: {
		post: (parent, args, context, info) => {
			let idCount = links.length

				 const link = {
					id: `link-${idCount++}`,
					description: args.description,
					url: args.url,
				}
				links.push(link)
				
			return link;
			}
		}
	}
```





