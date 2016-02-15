**`actionType`**` :: string`

**`action`**` :: {...{*}, type}`

**`state`**` :: {*}`

**`actionCreator`**` :: ...* -> action`

**`reducer`**` :: ...* -> state, action -> state`

**`createStore`**` :: reducer, initialState, enhancer -> store`

**`listener`**`(IO) :: _ -> _`

**`getState`**`(IO) :: _ -> state`

**`dispatch`**`(IO) :: action -> action`

**`subscribe`**`(IO) :: listener -> unsubscribe`

**`replaceReducer`**`(IO) :: reducer -> _`

**`combineReducers`**`(IO) :: {...[reducer]} -> reducer`

**`bindActionCreators`**`(IO) :: {...[actionCreator]}, dispatch -> {...[boundedActionCreator]}`

**`middleware`**`(IO) :: store -> next -> action -> action`

**`applyMiddleware`**`(IO) :: ...middlewares -> createStore -> store`



