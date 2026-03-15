  * ## Notes
    * React interacts with web dom
    * ```javascript
<html>
  <body>
    <script type="module">
      const root = document.createElement('div')
      root.id = 'root'
      document.body.append(root)

      const doc = document.createElement('div')
      doc.textContent = 'Hello World'
      doc.className = 'container'
      root.append(doc)
    </script>
  </body>
</html>```
    * Basically something like this, but it abstracts away the imperative way and replacing it with more declarative approach
    * The react way
      * ```javascript
  <script type="module">
    const rootElement = document.getElementById('root')

    const reactElement1 = React.createElement('span', {children: 'Hello'})
    const reactElement2 = React.createElement('span', {children: 'World'})

    const reactElement = React.createElement('div', {
      class: 'container',
      children: [reactElement1, reactElement2],
    })
    ReactDOM.render(reactElement, rootElement)
  </script>```
    * To be able to compile JSX we have to use babel and tag script as babel script
      * ```javascript
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@17.0.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@17.0.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.12.4/babel.js"></script>

  <script type="text/babel">
    const className = 'container'
    const helloWorld = 'Hello World'
    const element = <div className={className}> {helloWorld} </div>
    ReactDOM.render(element, document.getElementById('root'))
  </script>
</body>```
