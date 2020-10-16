# oapi-to-capi

Udemy Vue3 course Section 19

example of how to refactor from Options API (Vue2) to Composition API (Vue3)

## Concepts

Code chunks (computed/methods/watch etc.) get moved into setup()

- Allows us to co-locate related logic/computed props/methods in same area of setup()

  - Example: 'Search Logic' and 'Sorting Logic' code are co-located in setup() of UserList.vue

  - a lot less scrolling! much easier to adjust or update code (from computed, to methods, to watchers blocks)

  - code has cleaner look (for example: replacing this.x with props.x) - seems a bit more intuitive

You can mix and match Options API with Composition API:

- example: UserItem.vue and BaseSearch.vue use Options API (were not migrated to Composition API)


## Installation

npm install


## Run

npm run serve (Development)

