# Redux: Implementation

## Directories

A store is composed of reducers. Each reducer is composed of constants, actions, the reducer and its initialState, and selectors. That's a lot of small, moving parts. It helps to stay organized.

We are going to create a store with a single reducer -- **settings**.

We will have the following folder structure:

```
store
  settings
    actions
    constants
    reducer
    selectors
```

Every folder will have an index.js file that will handle the exports for the directory.
