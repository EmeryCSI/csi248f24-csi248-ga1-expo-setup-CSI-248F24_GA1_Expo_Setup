# Renton Technical College CSI-248

<br />

<div align="center">  
    <img src="logo.jpg" alt="Logo">
    <h3 align="center">Guided Activity 1</h3>
</div>

This repository is a part of CSI-248 at Renton Technical College.

## Guided Activity 1

## Setup Expo - If you have already done this in class you may skip this step

1. Sign up for an account at https://expo.dev/
2. Install Expo Go on your mobile device in the Apple App Store or Google Play Store
3. Sign in to the Expo Go App on your phone using your account you made at expo.dev
4. If you are unable to get Expo Go working on your mobile device you can also run a react native project in the browser.

## Clone this repository

1. Clone the repository to your local machine. (Do not use OneDrive for assignments in this course!)
2. Make note of the folder where you cloned the repository.
3. After you have cloned this repository navigate to your local repository using the cd command.
4. Open the repository in Visual Studio Code by typing `code .`

# React Native Basics: Components, Props, and State

## Getting Started

Before we dive into components, props, and state, we need to set up our development environment. We'll create a new React Native project using Expo, which provides a set of tools and services for React Native development.

## Project Setup Explained

Let's break down each step of our setup process:

1. **Create a new Expo project**:
   - We'll use `npx create-expo-app` which creates a new React Native project with Expo
   - `basic-resume` will be our project name
   ```bash
   npx create-expo-app basic-resume
   ```

2. **Navigate into the project directory**:
   - Change into the newly created project folder
   ```bash
   cd basic-resume
   ```

3. **Set up a proper project structure**:
   - Create a `src` folder to organize our source code
   - Create a `components` folder inside `src` to store our React components
   - This structure helps keep our code organized as the project grows
   ```bash
   mkdir src
   mkdir src/components
   ```

After running these commands, your project structure will look like this:
```
basic-resume/
├── src/
│   └── components/    # Where we'll store our components
├── App.js            # Main application file
├── package.json      # Project dependencies and scripts
└── ... other files   # Various configuration files
```

## Part 1: Understanding Components

### What is a Component?
In React Native, a component is like a building block for your app's interface. Think of it like a custom LEGO piece that you can:
- Create once and reuse many times
- Customize with different data
- Combine with other components to build complex interfaces

Components can be as simple as a button or as complex as an entire screen. They help us:
- Break down our app into manageable pieces
- Reuse code instead of repeating it
- Keep our code organized and maintainable

### Creating Our First Component

We'll start by creating a simple Header component. This component will display a name and title, showing us the basic structure of a React Native component.

1. **Create a new file**:
   - Create `Header.js` in the components folder
   - Path should be: `src/components/Header.js`

2. **Understanding the Component Structure**:
   - Components are JavaScript functions that return JSX
   - They must import necessary items from 'react-native'
   - They must return a single parent element
   - They should be exported to use in other files

Here's our first component:
```javascript
// src/components/Header.js
import { View, Text } from 'react-native';

// This is a basic component that displays text
const Header = () => {
  return (
    <View>
      <Text>John Doe</Text>
      <Text>Software Developer</Text>
    </View>
  );
};

export default Header;
```

## Part 2: Understanding and Using Props

### What are Props?
Props (short for "properties") are how we pass data to components. They work like:
- Parameters in a function
- Attributes in an HTML tag
- Configuration settings for a component

Think of props as a way to customize a component each time you use it. Just like how you might configure settings on your phone, props let you configure how a component looks and behaves.

### Why Do We Need Props?
Without props, components would be static and show the same thing every time. Props allow us:
- To reuse components with different data
- To make components flexible and customizable
- To pass data from parent components to child components

### Making Our Header Dynamic with Props

Let's modify our Header component to accept and use props. We'll change it from showing fixed text to showing whatever text we pass to it.

Update `src/components/Header.js`:
```javascript
// src/components/Header.js
import { View, Text } from 'react-native';

// Props are passed as a parameter to the component
const Header = (props) => {
  // We can destructure props to get specific values
  const { name, title } = props;
  
  return (
    <View>
      <Text>{name}</Text>
      <Text>{title}</Text>
    </View>
  );
};

export default Header;
```

## Part 3: Building a Simple Resume

### 1. Create a Contact Component
```javascript
// src/components/Contact.js
import { View, Text } from 'react-native';

const Contact = ({ email, phone }) => {
  return (
    <View>
      <Text>Email: {email}</Text>
      <Text>Phone: {phone}</Text>
    </View>
  );
};

export default Contact;
```

### 2. Create an Experience Component
```javascript
// src/components/Experience.js
import { View, Text } from 'react-native';

const Experience = ({ company, position, years }) => {
  return (
    <View>
      <Text>{company}</Text>
      <Text>{position}</Text>
      <Text>{years}</Text>
    </View>
  );
};

export default Experience;
```

### 3. Put it All Together in App.js
```javascript
// App.js
import { View } from 'react-native';
import Header from './src/components/Header';
import Contact from './src/components/Contact';
import Experience from './src/components/Experience';

export default function App() {
  return (
    <View>
      <Header 
        name="John Doe" 
        title="Software Developer" 
      />
      
      <Contact 
        email="john@email.com"
        phone="123-456-7890"
      />
      
      <Experience 
        company="Tech Corp"
        position="Senior Developer"
        years="2020-2023"
      />
    </View>
  );
}
```

## Part 4: Basic Styling

React Native uses JavaScript objects for styling. StyleSheet.create() helps optimize styles and provides better error checking.

```javascript
// Example with styles
import { View, Text, StyleSheet } from 'react-native';

const Header = ({ name, title }) => {
  return (
    <View style={styles.container}>
      <Text style={styles.name}>{name}</Text>
      <Text style={styles.title}>{title}</Text>
    </View>
  );
};

// StyleSheet.create makes styles more efficient
// It's like creating a stylesheet in CSS
const styles = StyleSheet.create({
  container: {
    padding: 20,          // Adds space inside the container
    marginTop: 40,        // Adds space above the container
  },
  name: {
    fontSize: 24,         // Sets text size
    fontWeight: 'bold',   // Makes text bold
  },
  title: {
    fontSize: 18,         // Smaller text size
    color: '#666',        // Gray text color
  },
});

export default Header;
```

## Part 5: Understanding State

State is for data that changes over time in a component. Unlike props (which are passed from parent), state is managed inside a component.

### Creating a Counter Component
```javascript
// src/components/Counter.js
import { View, Text, Button } from 'react-native';
// Import useState hook from React
import { useState } from 'react';

const Counter = () => {
  // useState returns:
  // 1. The current state value (count)
  // 2. A function to update it (setCount)
  // useState(0) sets initial value to 0
  const [count, setCount] = useState(0);

  return (
    <View>
      <Text>Count: {count}</Text>
      
      {/* When button is pressed, update state */}
      <Button 
        title="Increase" 
        onPress={() => setCount(count + 1)} 
      />
      
      <Button 
        title="Decrease" 
        onPress={() => setCount(count - 1)} 
      />
    </View>
  );
};

export default Counter;
```

Add Counter to App.js:
```javascript
// App.js
// ... other imports
import Counter from './src/components/Counter';

export default function App() {
  return (
    <View>
      {/* ... other components */}
      <Counter />
    </View>
  );
}
```

## Understanding useState

1. What is useState?
   - A Hook that lets you add state to functional components
   - Returns an array with two items: current state and update function
   - The update function triggers a re-render when called

2. Why use useState?
   - To handle data that changes over time
   - To make components interactive
   - To update the UI when data changes

3. useState Rules:
   - Can only be called inside components
   - Must be called at the top level (not in loops or conditions)
   - Initial value is only used on first render

Example with multiple states:
```javascript
const Counter = () => {
  // You can have multiple state variables
  const [count, setCount] = useState(0);
  const [step, setStep] = useState(1);

  return (
    <View>
      <Text>Count: {count}</Text>
      <Text>Step Size: {step}</Text>
      <Button 
        title="Increase" 
        onPress={() => setCount(count + step)} 
      />
      <Button 
        title="Change Step"
        onPress={() => setStep(step + 1)}
      />
    </View>
  );
};
```

## Practice Exercises

1. Add a Skills component that takes an array of skills as props
2. Add a reset button to the Counter component
3. Try combining props and state in a new component
4. Add a toggle button that shows/hides contact information

## Key Takeaways

1. Components are reusable UI pieces
2. Props pass data down from parent to child
3. State manages data that changes within a component
4. useState is the hook for managing state in functional components
13. Our Dark mode should be working across all of our components.
14. If you needed a dark/light mode theme beyond just a few components you may want to use a global state container.
15. Take a screenshot of your final functioning app add it to the screenshots folder.
16. `git add .`
17. `git commit -m "Assignment Complete"`
18. `git push`

If you have any questions about this assignment please reach out to myself or our TA for this course.
https://expo.dev/
