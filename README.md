<h1 align="center"> ReactJS Redux Install & Use In Step By Step :) </h1>

**Step 1: Install Dependencies**

```bash
npm install react-redux @reduxjs/toolkit
```

**Step 2: Create Redux Slice**

In the `Features` folder, create a file named `counterSlice.js`:

```javascript
// counterSlice.js

import { createSlice } from "@reduxjs/toolkit";

const initialState = {
  value: 0,
  menuOpen: true,
};

export const counterSlice = createSlice({
  name: "counter",
  initialState,
  reducers: {
    increment: (state) => {
      state.value += 1;
    },
    decrement: (state) => {
      state.value -= 1;
    },
    incrementByAmount: (state, action) => {
      state.value += action.payload;
    },
    toggleMenu: (state) => {
      state.menuOpen = !state.menuOpen;
    },
    setMenuOpen: (state, action) => {
      state.menuOpen = action.payload;
    },
  },
});

export const { increment, decrement, incrementByAmount, toggleMenu, setMenuOpen } = counterSlice.actions;

export default counterSlice.reducer;
```

**Step 3: Create Redux Store**

In the `GlobalRedux` folder, create a file named `store.js`:

```javascript
// store.js

import { combineReducers, configureStore } from "@reduxjs/toolkit";
import counterReducer from "./Features/counterSlice";

const rootReducer = combineReducers({
  counter: counterReducer,
  // Add other reducers here
});

export const store = configureStore({
  reducer: rootReducer,
});
```

**Step 4: Create Redux Provider**

In the `GlobalRedux` folder, create a file named `provider.js`:

```javascript
// provider.js

import React from "react";
import { Provider } from "react-redux";
import { store } from "./store";

export function ReduxProvider({ children }) {
  return <Provider store={store}>{children}</Provider>;
}
```

**Step 5: Integrate Redux Provider in Your App**

In your `index.js` or `main.jsx` file:

```javascript
// main.jsx

import React from 'react';
import ReactDOM from 'react-dom';
import { ReduxProvider } from './GlobalRedux/provider';
import App from './App';

ReactDOM.createRoot(document.getElementById('root')).render(
  <ReduxProvider>
    <App />
  </ReduxProvider>
);
```

**Step 6: Use Redux in Your Component**

In your `App.jsx` (or any component where you want to use Redux):

```javascript
// App.jsx

import React from 'react';
import { useDispatch, useSelector } from 'react-redux';
import { decrement, increment } from '../../GlobalRedux/Features/counterSlice';

const App = () => {
  const count = useSelector((state) => state.counter.value);
  const dispatch = useDispatch();

  return (
    <div>
      <button onClick={() => dispatch(increment())}>Increment</button>
      <span>{count}</span>
      <button onClick={() => dispatch(decrement())}>Decrement</button>
    </div>
  );
};

export default App;
```
