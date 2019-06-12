---
type: post
title: redux-observable  RxJS 6  Redux 

---


redux-observable


redux-observable 是基于 RxJS 6 的 Redux 中间件， 用于 compose and cancel async action

```
npm install --save redux-observable
```



Epic

Epic 是一个函数，参数是 action 流和 state 流，返回 action 流

```
const loginEpic = (action$, state$) => action$.pipe(
  ofType('entry/login'),
  delay(1000),
  mapTo({ type: 'PONG' }),
)
```






https://redux-observable.js.org/
