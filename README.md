Now let's move back into our React app folder. We will now replace the local data-mock usage with a fetch from the server. For that we can use the native fetch API, however, it needs to be used in the right life-cycle hook of the React.Component.

There are 2 naive approaches for that:

Calling fetch()outside the component, but this way that chats will be fetched even if we're not even intending to create an instance of the component.
fetch().then(() => /* ... */)
const MyComponent = () => {}
Calling fetch()inside the component, but then it will be invoked whenever the component is re-rendered.
const MyComponent = () => {
  fetch().then(() => /* ... */)
}

Introducing: React hooks

With React hooks we can invoke the desired logic in the right life-cycle stage of the target component. This way we can avoid potential memory leaks or extra calculations. To implement a proper fetch(), we will be using 2 React hooks:

React.useState()- which is used to get and set a state of the component - will be used to store the chats fetched from the server.
const [value, setValue] = useState(initialValue);
React.useMemo()- which is used to run a computation only once certain conditions were met - will be used to run the fetch()function only once the component has mounted.
const memoizedValue = useMemo(calcFn, [cond1, cond2, ...conds]);
The result of that approach will look like this, in the context of our ChatsList component:
