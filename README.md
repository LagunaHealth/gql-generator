# gql-generator

CLI tool that generates graphql queries and mutations placeholders from graphql schema file.

---

## how does it work

This CLI tool takes in a graphql schema as input and generates every query and mutation with input params with type placeholders and output types.

The queries and mutations are generated into two folders [query, mutation] and for each query/mutation a .gql file is created

gql-generator has three inputs:

- input: path to graphql schema file
- output: path to output folders to
- depth: how deep to generate the type

---

## example

we have the following schema file:

```graphql
input CreateUserInput {
  firstName: String!
}

type Mutation {
  createUser(input: CreateUserInput!): User!
}

type Query {
  users: [User!]!
}

type User {
  id: String!
  username: String!
}
```

---

the output will be:

`query/users.gql`

```graphql
query {
  users {
    id
    username
  }
}
```

`mutation/createUser.gql`

```graphql
mutation {
  createUser (
    input: {
      firstName: String!
    }
  ) {
    id
    username
  }
}
```

---

## How to Use

```bash
# install
npm install -g @lagunahealth/gql-generator

# see the usage
gql-generator --help

gql-generator --input ./schema.gql --output ./ --depth 6
```
