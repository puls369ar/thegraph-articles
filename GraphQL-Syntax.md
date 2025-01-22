

Basic Types
* ID
* Int
* Boolean
* String 

We can define complex types by ourselves
```graphql
type Job {
  position: String
  company: String
  salary: Int
}

type User {
  id: ID!
  name: String
  age: Int
  job: Job
}
```

by adding an exclamation symbol after the type we make that field required to fetch during the request (f.e `ID!`)
