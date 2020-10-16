# oapi-to-capi

Udemy Vue3 course Section 19

example of how to refactor from Options API (Vue2) to Composition API (Vue3)

## Concepts

Code chunks (computed/methods/watch etc.) get moved into setup()

- Allows us to co-locate related logic/computed props/methods in same area of setup()

  - variables/computed/methods for 'Search Logic' co-located in setup() of UserList.vue

  - variables/computed/methods for 'Sorting Logic' co-located in setup() of UserList.vue

  - a lot less scrolling in a complex components (don't need to scroll between computed, methods, watchers blocks)

  - code has cleaner look (for example: replacing this.x with props.x) - seems a bit more intuitive

You can mix and match Options API with Composition API:

- example: UserItem.vue and BaseSearch.vue use Options API (were not migrated to Composition API)


## Installation

npm install


## Run

npm run serve (Development)

