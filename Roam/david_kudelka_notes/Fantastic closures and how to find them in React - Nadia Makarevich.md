  * tags: #react #closures #performance
  * link to article: https://www.developerway.com/posts/fantastic-closures
  * author: [[Nadia Makarevich]]
  * notes:
    * ## Description of the problem, we are trying to solve in this article
      * ```javascript
const HeavyComponentMemo = React.memo(
  HeavyComponent,
  (before, after) => {
    return before.title === after.title;
  },
);

const Form = () => {
  const [value, setValue] = useState();

  const onClick = () => {
    // submit our form data here
    console.log(value);
  };

  return (
    <>
      <input
        type="text"
        value={value}
        onChange={(e) => setValue(e.target.value)}
      />
      <HeavyComponentMemo
        title="Welcome to the form"
        onClick={onClick}
      />
    </>
  );
};```
      * So you have this `HeavyComponent` that lives outside of your codebase, and this component is not optimised for performance
      * You need to use in **form**, send to it 2 props -> **title** and **onClick** function. 
      * Once you will be done with your form you want to trigger this **onClick** function, with all the data inside of it (inside the onClick function closure)
    * ## JavaScript, scope, and closures
      * ```javascript
const something = () => {
  const value = 'text';
};

console.log(value); // not going to work, ```
      * By declaring function `something` and const `value` inside of it. It becomes scoped just for the function and the variable is not available for us outside of it
      * **In the opposite direction**, however it's an open road. The inner-most function will "see" all the variables declared outside
        * ```javascript
const something = () => {
  const value = 'text';

  const inside = () => {
    // perfectly fine, value is available here
    console.log(value);
  };
};```
      * This is achieved by creating something known as **closure**. The function inside **"closes"** over all the data from the outside. It's essentially a snapshot of all the **"outside"** data frozen in time stored separately in memory
      * ### In React
        * In React we are creating closures all the time even without realising it. Every single callback function declared inside a component is a closure
          * ```javascript
const Component = () => {
  const onClick = () => {
    // closure!
  };

  return <button onClick={onClick} />;
};```
          * Everything in `useEffect` or `useCallback` hook is a closure
          * ```javascript
const Component = () => {
  const onClick = useCallback(() => {
    // closure!
  });

  useEffect(() => {
    // closure!
  });
};```
        * Every single function **inside** a component is a **closure** since a component itself is just a **function**.
      * ### How to create stale closuer?
        * ```javascript
const cache = {};

const something = (value) => {
  if (!cache.current) {
    cache.current = () => {
      console.log(value);
    };
  }

  return cache.current;
};```
        * Because we cached the value, when we call function `something` for the first time it will create **closure**, but all other calls will have the same exact snapshot of that function -> **stale closure**
        * How to fix this?
          * ```javascript
const something = (value) => {
  // check whether the value has changed
  if (!cache.current || value !== prevValue) {
    cache.current = () => {
      console.log(value);
    };
  }

  // refresh it
  prevValue = value;
  return cache.current;
};```
          * In this scenario, we are caching the function `something`, but at the same time we are reseting cache every time `value` changes
    * ## Stale closures in React: useCallback
      * ```javascript
const Component = () => {
  const [state, setState] = useState();

  const onClick = useCallback(() => {
    // state will always be the initial state value here
    // the closure is never refreshed
    console.log(state);

    // forgot about dependencies
  }, []);
};```
    * ## Stale closures in React: Refs
      * ref in React can solve our issue of passing prop to component, but never cause re-render
        * ```javascript
const Component = ({ someProp }) => {
  // initialize ref - creates closure!
  const ref = useRef(() => {
    // both of them will be stale and will never change
    console.log(someProp);
    console.log(state);
  });

  useEffect(() => {
    // update the closure when state or props change
    ref.current = () => {
      console.log(someProp);
      console.log(state);
    };
  }, [state, someProp]);
};```
    * ## Escaping the closure trap with Refs
      * ```javascript
const Form = () => {
  const ref = useRef();

  useEffect(() => {
    ref.current = () => {
      console.log(value);
    };
  });

  const onClick = useCallback(() => {
    ref.current();
  }, []);

  return (
    <>
      {/* Now memoization will work, onClick never changes */}
      <HeavyComponentMemo onClick={onClick} />
    </>
  );
};```
      * Notice how `ref` is not in dependency list of the `useCallback`
        * `ref` - is just reference to a mutable object that the `useRef` hook returns
      * But when a closure freezes everything around it, it doesn't make objects immutable or frozen. Objects are stored in a different part of the memory, and multiple variables can contain references to exactly same object
        * ```javascript
const a = { value: 'one' };
// b is a different variable that references the same object
const b = a;

a.value = 'two';

console.log(b.value); // will be "two"```
