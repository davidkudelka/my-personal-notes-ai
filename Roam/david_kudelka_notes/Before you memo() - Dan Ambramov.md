  * tags: #react #performance #memo
  * author: [[Dan Abramov]]
  * link to article: https://overreacted.io/before-you-memo/
  * notes:
    * ### Let's look at this code
      * ```javascript
export default function App() {
  let [color, setColor] = useState('red');
  return (
    <div>
      <input value={color} onChange={(e) => setColor(e.target.value)} />
      <p style={{ color }}>Hello, world!</p>
      <ExpensiveTree />
    </div>
  );
}```
      * How would you optimise it?
        * Probably go to `<ExpensiveTree />` component and use `memo`
        * But do you actually have to do it?
    * ### Other solutions
      * **Move the state Down**
        * ```javascript
export default function App() {
  return (
    <>
      <Form />
      <ExpensiveTree />
    </>
  );
}

function Form() {
  let [color, setColor] = useState('red');
  return (
    <>
      <input value={color} onChange={(e) => setColor(e.target.value)} />
      <p style={{ color }}>Hello, world!</p>
    </>
  );
}```
        * Quite easy solution, we can move the state down, because only just segment of our components are using it
      * **Lift the content up**
        * Maybe you can't move the state down, because the state is used not only in one segment, but across whole component
          * ```javascript
export default function App() {
  let [color, setColor] = useState('red');
  return (
    <div style={{ color }}>
      <input value={color} onChange={(e) => setColor(e.target.value)} />
      <p>Hello, world!</p>
      <ExpensiveTree />
    </div>
  );
}```
        * So the solution could be
          * ```javascript
export default function App() {
  return (
    <ColorPicker>
      <p>Hello, world!</p>
      <ExpensiveTree />
    </ColorPicker>
  );
}

function ColorPicker({ children }) {
  let [color, setColor] = useState("red");
  return (
    <div style={{ color }}>
      <input value={color} onChange={(e) => setColor(e.target.value)} />
      {children}
    </div>
  );
}```
    * ## What's the moral?
      * Before you apply `memo`, you should think about your component structure, maybe there is issue in that
      * Component structure as well highly depends on the data flow in your application, more to say about this in those article notes - [[Parents & Owners in React Data Flow - Jules Blom]]