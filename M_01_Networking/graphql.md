# 🚀 GraphQL in React (Frontend Only) – Beginner’s Guide

## ✅ Goal:  
You will learn how to **query, mutate, and handle data from a GraphQL API** in a React app using **Apollo Client** — without worrying about building backend APIs.

---

## 🔧 Step 1: What Is Apollo Client (and Why Use It)?

### 🧠 Apollo Client:
> A powerful GraphQL client for React that helps you fetch, cache, and update data from GraphQL APIs easily.

**Why not fetch/axios?**
| axios/fetch + REST         | Apollo Client + GraphQL         |
|----------------------------|----------------------------------|
| Manual request setup       | Declarative `useQuery`, `useMutation` |
| No built-in caching        | Smart client-side caching       |
| Separate URLs per resource| Single endpoint                 |
| Harder to batch            | GraphQL batches in one call     |

Apollo makes your frontend **cleaner**, **faster**, and **smarter** when working with GraphQL.

---

## ⚙️ Step 2: Installing Apollo Client in React

```bash
npm install @apollo/client graphql
```

---

## 🏗️ Step 3: Setting Up ApolloProvider (Like Context API)

```tsx
// index.tsx or App.tsx
import { ApolloClient, InMemoryCache, ApolloProvider } from '@apollo/client';

const client = new ApolloClient({
  uri: 'https://example.com/graphql', // GraphQL API endpoint
  cache: new InMemoryCache(),
});

const App = () => (
  <ApolloProvider client={client}>
    <YourMainApp />
  </ApolloProvider>
);
```

✅ Now all components inside `ApolloProvider` can use GraphQL queries!

---

## 🔎 Step 4: Fetching Data Using `useQuery`

```tsx
import { useQuery, gql } from '@apollo/client';

const GET_USERS = gql`
  query {
    users {
      id
      name
      email
    }
  }
`;

function UsersList() {
  const { loading, error, data } = useQuery(GET_USERS);

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error! {error.message}</p>;

  return (
    <ul>
      {data.users.map((user) => (
        <li key={user.id}>{user.name} - {user.email}</li>
      ))}
    </ul>
  );
}
```

---

## 🛠️ Step 5: Writing Data Using `useMutation`

```tsx
import { useMutation, gql } from '@apollo/client';

const CREATE_USER = gql`
  mutation CreateUser($name: String!, $email: String!) {
    createUser(name: $name, email: $email) {
      id
      name
    }
  }
`;

function CreateUserForm() {
  const [createUser, { loading, error, data }] = useMutation(CREATE_USER);

  const handleCreate = () => {
    createUser({ variables: { name: "Gaurav", email: "gaurav@mail.com" } });
  };

  return (
    <div>
      <button onClick={handleCreate}>Create User</button>
      {loading && <p>Creating...</p>}
      {error && <p>Error: {error.message}</p>}
      {data && <p>User Created: {data.createUser.name}</p>}
    </div>
  );
}
```

---

## 🧠 Key Hooks You’ll Use in React

| Hook           | Purpose                     |
|----------------|-----------------------------|
| `useQuery()`   | Fetching data (GET)         |
| `useMutation()`| Creating/updating/deleting  |
| `useLazyQuery()`| Manual fetch trigger       |

---

## 🗃️ Bonus: Apollo DevTools for Debugging
Install Apollo DevTools Chrome extension to inspect queries, responses, cache, etc.

---

## 🧪 Sample GraphQL APIs to Practice
You can test Apollo Client with public GraphQL APIs:
- [https://countries.trevorblades.com/](https://countries.trevorblades.com/)
- [https://graphqlzero.almansi.me/api](https://graphqlzero.almansi.me/api) (Fake JSONPlaceholder-like)

---

## 🧾 Summary

| Concept              | REST (axios/fetch)          | GraphQL (Apollo Client)         |
|----------------------|-----------------------------|----------------------------------|
| Data fetching        | `axios.get('/api/users')`   | `useQuery(GET_USERS)`           |
| Data creation        | `axios.post(...)`           | `useMutation(CREATE_USER)`      |
| Response shape       | Fixed, server-controlled    | Dynamic, client-controlled       |
| Dev experience       | Manual and verbose          | Declarative, reactive, elegant   |

---

✅ Done! You now understand:
- What Apollo Client is
- How to integrate GraphQL in React
- How to write queries and mutations with hooks

---
