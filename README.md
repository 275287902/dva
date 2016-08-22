# dva

[![NPM version](https://img.shields.io/npm/v/dva.svg?style=flat)](https://npmjs.org/package/dva)
[![Build Status](https://img.shields.io/travis/sorrycc/dva.svg?style=flat)](https://travis-ci.org/sorrycc/dva)
[![Coverage Status](https://img.shields.io/coveralls/sorrycc/dva.svg?style=flat)](https://coveralls.io/r/sorrycc/dva)
[![NPM downloads](http://img.shields.io/npm/dm/dva.svg?style=flat)](https://npmjs.org/package/dva)

Lightweight elm-style framework based on react and redux.

----

## Documents

- [dva 入门：手把手教你写应用](https://github.com/sorrycc/blog/issues/8)
- [dva 简介](https://github.com/dvajs/dva/issues/1)
- [React + Redux 最佳实践](https://github.com/sorrycc/blog/issues/1) (dva 基于此封装)
- [subscription 及其适用场景](https://github.com/dvajs/dva/issues/3#issuecomment-229250708)
- [支付宝前端应用架构的发展和选择: 从 roof 到 redux 再到 dva](https://github.com/sorrycc/blog/issues/6)

## Features

- based on redux, redux-saga and react-router
- **small api:** only 5 methods
- **transparent side effects:** using effects and subscriptions brings clarity to IO
- **mobile and react-native support:** don't need router
- **dynamic model and router:** split large scale app on demand
- **plugin system:** with hooks
- **hmr support:** components and routes is ready

## Demos

- [HackerNews](https://dvajs.github.io/dva-hackernews/) ([repo](https://github.com/dvajs/dva-hackernews), [intro](https://github.com/sorrycc/blog/issues/9))
- [Count](./examples/count) ([jsfiddle](https://jsfiddle.net/puftw0ea/))
- [Popular Products](./examples/popular-products)
- [Friend List](./examples/friend-list)
- [User Dashboard](./examples/user-dashboard)

## Getting Started

### Install

```bash
$ npm install --save dva
```

### Example

Let's create an count app that changes when user click the + or - button. 

```javascript
import React from 'react';
import dva, { connect } from 'dva';
import { Router, Route } from 'dva/router';

// 1. Initialize
const app = dva();

// 2. Model
app.model({
  namespace: 'count',
  state: 0,
  reducers: {
    add  (count) { return count + 1 },
    minus(count) { return count - 1 },
  },
});

// 3. View
const App = connect(({ count }) => ({
  count
}))(function(props) {
  return (
    <div>
      <h2>{ props.count }</h2>
      <button key="add" onClick={()   => { props.dispatch({type: 'count/add'})}}>+</button>
      <button key="minus" onClick={() => { props.dispatch({type: 'count/minus'})}}>-</button>
    </div>
  );
});

// 4. Router
app.router(({ history }) =>
  <Router history={history}>
    <Route path="/" component={App} />
  </Router>
);

// 5. Start
app.start('#root');
```

## FAQ

### Why is it called dva?

dva is a hero from [overwatch](http://ow.blizzard.cn/heroes/dva). She is cute, and `dva` is the shortest one that is available on npm.

### Is it production ready?

Yes.

## License

[MIT](https://tldrlegal.com/license/mit-license)
