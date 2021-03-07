# Redux: Implementation

## Directories

A store is composed of reducers. Each reducer is composed of constants, actions, the reducer, initialState, and selectors. That's a lot of small, moving parts. It helps to stay organized.

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
