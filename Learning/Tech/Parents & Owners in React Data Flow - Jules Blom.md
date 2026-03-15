  * tags: #article #react #data-flow 
  * author: [[Jules Blom]]
  * link to article: https://julesblom.com/writing/parents-owners-data-flow
  * notes:
    * ### What makes a React app well-composed?
      * An easy-to-follow data flow
      * Well-encapsulated components
      * Good rendering performance
    * ### Prop drilling vs lifting the components up
      * Simple application with using prop drilling
        * ```javascript
function App() {
  const [currentUser, setCurrentUser] = useState({ name: "Jules" });
  const [personalMessage, setPersonalMessage] = useState();

  return (
    <div>
      <Header />
      <div>
        {currentUser ? (
          <Dashboard user={currentUser} personalMessage={personalMessage} />
        ) : (
          <LoginScreen onLogin={() => setCurrentUser({ name: "Michael" })} />
        )}
      </div>
      <Footer />
    </div>
  );
}

function Dashboard({ user, personalMessage }) {
  return (
    <main>
      <h2>The Dashboard</h2>
      <DashboardNav />
      <DashboardContent user={user} personalMessage={personalMessage} />
    </main>
  );
}

function DashboardContent({ user, personalMessage }) {
  return (
    <div>
      <h3>Dashboard Content</h3>
      <WelcomeMessage user={user} personalMessage={personalMessage} />
    </div>
  );
}

function WelcomeMessage({ user, personalMessage }) {
  return (
    <div>
      <p>Welcome {user.name} {personalMessage}</p>
    </div>
  );
}```
        * **What is the problem there?**
          * If you want to refactor something, what do you have to do? Adjust all of the components and their props
      * Application that is lifting the components up
        * ```javascript
function App() {
  const [currentUser, setCurrentUser] = useState({ name: "Jules" });

  return (
    <div>
      <Header />
      <div>
        {currentUser ? (
          <Dashboard>
            <DashboardNav />
            <DashboardContent>
              <WelcomeMessage user={currentUser} />
            </DashboardContent>
          </Dashboard>
        ) : (
          <LoginScreen onLogin={() => setCurrentUser({ name: "Michael" })} />
        )}
      </div>
      <Footer />
    </div>
  );
}

function Dashboard({ children }) {
  return (
    <main>
      <h2>The Dashboard</h2>
      {children}
    </main>
  );
}

function DashboardContent({ children }) {
  return (
    <div>
      <h3>Dashboard Content</h3>
      {children}
    </div>
  );
}

function WelcomeMessage({ user }) {
  return (
    <div>
      <p>Welcome {user.name}</p>
    </div>
  );
}```
    * ### Parent vs Owner Hierarchy
      * The parent tree: which components are nested inside of another. This is what you see in the React DevTools
      * The owner tree: which component renders another components. This is the hierarchy we see in the code
    * ### Slotted component
      * It can have different names as `layout`, `wrapper` or `container` component
      * It refers to component that instead of just having other components in it's return function, it will place it's children on specific place, therefore can be used as a wrapper
    * ### Wrap up
      * Understanding the owner vs parent component distinction is important for composing well
        * The create similar but different hierarchies. They're related, which makes it easy to mix them up
        * The owner tree is the shape of the data flow
          * If the data flow is a mess, look at the owner trees. This can reveal when it's a good idea to lift a component up
      * Slotted component can skip a level in the owner tree while creating the same parent tree
        * Which is useful when `prop drilling` 
    * ### Bad side of lifting components up
      * This inversion of control [lifting components] can make your code cleaner in many cases by reducing the amount of props you need to pass through your application and giving more control to the root components.
      * Such inversion, however, isn’t the right choice in every case; moving more complexity higher in the tree makes those higher-level components more complicated and forces the lower-level components to be more flexible than you may want.
