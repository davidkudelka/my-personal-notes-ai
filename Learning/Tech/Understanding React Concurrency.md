  * tags: #react #concurrency #article
  * author: [[Slava Knyazev]]
  * notes:
    * ## What is React Concurrency
      * The basic premise of React concurrency is to re-work the rendering process such that while rendering the next view, the current view is kept responsive
      * Code example
        * ```javascript
function MyCounter() {
    const [isPending, startTransition] = useTransition();
    const [count, setCount] = useState(0);
    const increment = useCallback(() => {
        startTransition(() => {
            // Run this update concurrently
            setCount(count => count + 1);
        });
    }, []);
 
    return (
        <>
            <button onClick={increment}>Count {count}</button>
            <span>{isPending ? "Pending" : "Not Pending"}</span>
            // Component which benefits from concurrency
            <ManySlowComponents count={count} />
        </>
    )
}```
      * There is one quite similar hook that takes advantage of concurrency as well and that is `useDeferredValue`
        * It should be used for **inputs** and that is, because you don't have control over the state of that component
        * Code example
          * ```javascript
function useDeferredValue<T>(value: T) {
    const [isPending, startTransition] = useTransition();
    const [state, setState] = useState(value);
    useEffect(() => {
        // Dispatch concurrent render
        // when input changes
        startTransition(() => {
            setState(value);
        });
    }, [value])

    return state;
}```