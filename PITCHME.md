# Typescipt - Vuex - E2E - Building


---

- Typescript 101
- Vuex (with TS)
- E2E with nightwathc
- Our build pipeline

---

### TypeScript

Let's jump to some code!

---



### Vuex

- State
- Mutations
- Actions
- Getters

---

#### State

 A single object which contains all your application level state and serves as the "single source of truth".

```js
const state = {
  trades: [],
  counter: 0
}
```

---

 #### Mutations

 The only way to actually change state in a Vuex store is by committing a mutation. Vuex mutations are very similar to events

```js
increment: (state, newCounterValue) => {
  state.counter = newCounterValue
}
```


---

 #### Actions

 Actions are similar to mutations, the differences being that:

- Instead of mutating the state, actions commit mutations.
- Actions can contain arbitrary asynchronous operations.

---

```js
incrementCounter: ({store}) => {
  let newValue = store.counter
  dispatch('increment', ++newValue)
}
```

---

#### Multiple commits in one action

```js
actions: {
  checkout ({ commit, state }, products) {
    // save the items currently in the cart
    const savedCartItems = [...state.cart.added]
    // send out checkout request, and optimistically
    // clear the cart
    commit(types.CHECKOUT_REQUEST)
    // the shop API accepts a success callback and a failure callback
    shop.buyProducts(
      products,
      // handle success
      () => commit(types.CHECKOUT_SUCCESS),
      // handle failure
      () => commit(types.CHECKOUT_FAILURE, savedCartItems)
    )
  }
}
```

source: https://vuex.vuejs.org/en/actions.html

---

 #### Getters

 Sometimes we may need to compute derived state based on store state, for example filtering through a list of items and counting them


 ```js
bookableTrades: state => state.trades.filter(trade => trade.status !== 'DISABLED')
 ```

---

 ### Vuex-counter Example

live code again!

---