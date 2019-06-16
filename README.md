# Summary

Combination of:

- https://github.com/masaok/scotch-graphql-demo
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
