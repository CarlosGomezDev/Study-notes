`2020-01-13, React, 20:00`

### React
JavaScript library for user interfaces, created by facebook.
React native, for native mobile applications using react.
Best resource, react docs: http://reactjs.org

An element is the most atomic unit of a React application.
A collection of elements is a component. A component is a function that return UI.
Props or properties, is an object in React that contains properties about a component, we can use it to display dynamic data within a component.

#### React Toolkits
One of the most common ways of building react is using toolkits

**1. create-react-app**, for new single-page applications.
**2. Next.js**, for server-side rendered sites together with *Node.js*.
**3. Gatsby**, for static content.
**4. React Native**, for mobile native applications together with *Expo*.

#### create-react-app
Exists to make the process of setting up a React application easier.
- package.json contain all of our project's dependencies
 - Testing libraries `jest-dom`, `react-testing-library`, `user-event`
 - `react` library to work in react
 - `react-dom` to render our react to the browser
 - `react-scripts` to bundle and server our code
- `scr` folder, with all files needed to write a `react` application
- `public` folder, used to place all production ready files

##### JSX
JavaScript as XML is a language extension to write tags directly in the .js file.

##### Babel
Behind the scenes, babel is working to translate text that browsers do not understand, like JSX, and converting it into regular React.js or Vanilla JS code.