# Summary

Combination of:

- https://scotch.io/tutorials/a-practical-graphql-getting-started-guide-with-nodejs
  - https://github.com/masaok/scotch-graphql-demo
- https://dev.to/adnanrahic/how-to-deploy-a-nodejs-application-to-aws-lambda-using-serverless-2nc7
  - https://github.com/masaok/serverless-nodejs-app-demo

# Tutorial Source

https://serverless.com/blog/running-scalable-reliable-graphql-endpoint-with-serverless/

# Queries

## Get Single User

Query:
```
query getSingleUser($userID: Int!) {
    user(id: $userID) {
        name
        age
        gender
    }
}
```
Variables:
```
{ 
    "userID":1
}
```
Result:
```
{
  "data": {
    "user": {
      "name": "Brian",
      "age": 21,
      "gender": "M"
    }
  }
}
```

## Get Users with Aliases
```
query getUsersWithAliases($userAID: Int!, $userBID: Int!) {
    userA: user(id: $userAID) {
        name
        age
        gender
    },
    userB: user(id: $userBID) {
        name
        age
        gender
    }
}
```
Variables:
```
{ 
    "userAID":1,
    "userBID":2
}
```
Result:
```
{
  "data": {
    "userA": {
      "name": "Brian",
      "age": 21,
      "gender": "M"
    },
    "userB": {
      "name": "Kim",
      "age": 22,
      "gender": "M"
    }
  }
}
```
## Fragments
Query:
```
query getUsersWithFragments($userAID: Int!, $userBID: Int!) {
    userA: user(id: $userAID) {
        ...userFields
    },
    userB: user(id: $userBID) {
        ...userFields
    }
}

fragment userFields on Person {
  name
  age
  gender
}
```
Variables:
```
{ 
    "userAID":1,
    "userBID":2
}
```
Result:
```
{
  "data": {
    "userA": {
      "name": "Brian",
      "age": 21,
      "gender": "M"
    },
    "userB": {
      "name": "Kim",
      "age": 22,
      "gender": "M"
    }
  }
}
```
## Directives
Query:
```
query getUsers($gender: String, $age: Boolean!, $id: Boolean!) {
  users(gender: $gender){
    ...userFields
  }
}

fragment userFields on Person {
  name
  age @skip(if: $age)
  id @include(if: $id)
}
```
Variables:
```
{
  "gender": "F",
  "age": true,
  "id": true
}
```
Result:
```
{
  "data": {
    "users": [
      {
        "name": "Faith",
        "id": 3
      },
      {
        "name": "Joy",
        "id": 5
      }
    ]
  }
}
```
