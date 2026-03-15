  * tags: #frontend #dom #virtual-dom #svelte #react
  * link to article: https://svelte.dev/blog/virtual-dom-is-pure-overhead
  * author: [[Rich Harris]]
  * notes:
    * ## What is virtual DOM?
      * You can represent React component like this
        * ```javascript
function HelloMessage(props) {
  return <div className="greeting">Hello {props.name}</div>;
}
// But as well like this
function HelloMessage(props) {
  return React.createElement('div', { className: 'greeting' }, 'Hello ', props.name);
}```
      * Both are the same, it creates object and that object is **virtual DOM**
    * ### So... is the virtual DOM slow?
      * Not really, it's quite fast as it is just looping over objects (components)
      * But the original idea was to make React re-render the whole page on every state change
        * This wasn't successful endeavour - that's why we have in React `shouldComponentUpdate` and that is why React created something called **fiber**
        * **fiber** - it allows the update to broken up into multiple updates (it doesn't mean it's faster - its just happening over time - not blocking main thread)
    * ### Where does the overhead come from?
      * React is doing something called diffing - it's going through the DOM and trying to find what changed
      * Example of the code snippet at the beginning of this page. `HelloMessage` -> changed `props.name`
        * it compares if `div` changed for different DOM element - it didn't
        * it compares if `classname` changed for different `classname` - it didn't
        * it compares if `props.name` changed - it did YAY success!
      * It would be great to skip those steps into just comparing if `props.name` changed - and that is exactly what `Svelte` does - because of its compiler, it knows which parts of application can update and it doesn't do it in runtime
    * ### It's not just the diffing though
      * Diffing is usually fast, at least fast enough. Arguably, the greater overhead is in the components themselves. People can write code with mistakes :D
      * Example code
        * ```javascript
function MoreRealisticComponent(props) {
  const [selected, setSelected] = useState(null);
 
  return (
    <div>
      <p>Selected {selected ? selected.name : 'nothing'}</p>
 
      <ul>
        {props.items.map((item) => (
          <li>
            <button onClick={() => setSelected(item)}>{item.name}</button>
          </li>
        ))}
      </ul>
    </div>
  );
}```
      * **What is wrong here?**
        * On every state update -> you are as well generating new list of `<li>` elements
      * Most of the people wouldn't optimise this code - why? - because it's very fast, so you don't want to spend time optimising something that nobody notices
        * The issue occurs, when your application gets bigger and those problems are almost everywhere
        * Your app will eventually succumb to 'death by a thousand cuts'
    * ### Why do frameworks use virtual DOM then?
      * It let's you build applications without thinking about state transitions, with performance that is generally good enough.
        * -> That means less buggy code, and more time spent on creative tasks instead of tedious ones
        * -> But it turns out we can achieve a similar programming model without using virtual DOM - and that's where **Svelte** comes in