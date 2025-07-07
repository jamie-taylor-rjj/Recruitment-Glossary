---
title: "What is React?"
description: "Just what is React, and what can developers do with it?"
lead: "Just what is React, and what can developers do with it?"
date: 2020-10-06T08:49:31+00:00
lastmod: 2023-12-04T11:30:00+01:00
draft: false
images: []
menu:
  docs:
    parent: "react"
weight: 100
toc: true
---

## 10,000 ft Overview

React is a [JavaScript]({{< relref "what-is-javascript" >}}) library for building user interfaces, particularly web applications. Created by Facebook (now Meta) in 2013, React has become one of the most popular frontend frameworks in the world. It allows developers to create interactive, dynamic web applications using a component-based architecture.

React's key innovation is the Virtual DOM, which makes applications fast and efficient by minimizing direct manipulation of the browser's DOM. Instead of updating the entire page when data changes, React intelligently updates only the parts that need to change.

React applications are typically built using [Node.js]({{< relref "what-are-npm-and-nodejs" >}}) and can be enhanced with [TypeScript]({{< relref "what-is-typescript" >}}) for better developer experience and type safety. React focuses solely on the view layer, making it flexible enough to integrate with various backends and state management solutions.

{{< alert icon="💡" text="React is a library, not a framework. This means it provides the core functionality for building UIs but gives developers flexibility in choosing additional tools for routing, state management, and other concerns." />}}

## Beginner Information

React is built around the concept of components - reusable pieces of UI that manage their own state and can be composed together to build complex applications.

**Basic React Component:**

{{< highlight jsx "linenos=inline">}}
import React, { useState } from 'react';

// Functional component with hooks
function Welcome({ name }) {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h1>Hello, {name}!</h1>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}

// Using the component
function App() {
  return (
    <div>
      <Welcome name="Alice" />
      <Welcome name="Bob" />
    </div>
  );
}

export default App;
{{< /highlight >}}

**JSX Syntax:**

React uses JSX, which allows you to write HTML-like syntax directly in JavaScript:

{{< highlight jsx "linenos=inline">}}
// JSX allows mixing HTML and JavaScript
function UserProfile({ user }) {
  return (
    <div className="user-profile">
      <img src={user.avatar} alt={user.name} />
      <h2>{user.name}</h2>
      <p>Joined: {new Date(user.joinDate).toLocaleDateString()}</p>
      {user.isOnline && <span className="online-indicator">Online</span>}
    </div>
  );
}

// Conditional rendering
function LoginStatus({ isLoggedIn, user }) {
  if (isLoggedIn) {
    return <h1>Welcome back, {user.name}!</h1>;
  }
  return <h1>Please sign up.</h1>;
}

// Lists and keys
function TodoList({ todos }) {
  return (
    <ul>
      {todos.map(todo => (
        <li key={todo.id}>
          {todo.completed ? '✓' : '○'} {todo.text}
        </li>
      ))}
    </ul>
  );
}
{{< /highlight >}}

**React Hooks (Modern React):**

{{< highlight jsx "linenos=inline">}}
import React, { useState, useEffect } from 'react';

function UserData({ userId }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);

  // useEffect for side effects (data fetching, subscriptions, etc.)
  useEffect(() => {
    async function fetchUser() {
      setLoading(true);
      try {
        const response = await fetch(`/api/users/${userId}`);
        const userData = await response.json();
        setUser(userData);
      } catch (error) {
        console.error('Failed to fetch user:', error);
      } finally {
        setLoading(false);
      }
    }

    fetchUser();
  }, [userId]); // Re-run when userId changes

  if (loading) return <div>Loading...</div>;
  if (!user) return <div>User not found</div>;

  return (
    <div>
      <h1>{user.name}</h1>
      <p>{user.email}</p>
    </div>
  );
}
{{< /highlight >}}

**Getting Started:**

{{< highlight bash >}}
# Create a new React app
npx create-react-app my-app
cd my-app

# Start development server
npm start

# Build for production
npm run build
{{< /highlight >}}

**Key React Concepts:**

- **Components**: Reusable UI building blocks
- **Props**: Data passed to components from parent
- **State**: Internal component data that can change
- **Hooks**: Functions that let you "hook into" React features
- **Virtual DOM**: React's efficient rendering system

## Intermediary Information

React's component architecture and ecosystem provide powerful patterns for building scalable applications.

**Component Patterns:**

{{< highlight jsx "linenos=inline">}}
// Higher-Order Component (HOC)
function withLoading(WrappedComponent) {
  return function WithLoadingComponent({ isLoading, ...props }) {
    if (isLoading) {
      return <div>Loading...</div>;
    }
    return <WrappedComponent {...props} />;
  };
}

// Render Props Pattern
function DataFetcher({ url, children }) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    fetch(url)
      .then(response => response.json())
      .then(setData)
      .catch(setError)
      .finally(() => setLoading(false));
  }, [url]);

  return children({ data, loading, error });
}

// Usage
function App() {
  return (
    <DataFetcher url="/api/users">
      {({ data, loading, error }) => {
        if (loading) return <div>Loading...</div>;
        if (error) return <div>Error: {error.message}</div>;
        return <UserList users={data} />;
      }}
    </DataFetcher>
  );
}

// Custom Hooks
function useLocalStorage(key, initialValue) {
  const [storedValue, setStoredValue] = useState(() => {
    try {
      const item = window.localStorage.getItem(key);
      return item ? JSON.parse(item) : initialValue;
    } catch (error) {
      return initialValue;
    }
  });

  const setValue = (value) => {
    try {
      setStoredValue(value);
      window.localStorage.setItem(key, JSON.stringify(value));
    } catch (error) {
      console.error('Error saving to localStorage:', error);
    }
  };

  return [storedValue, setValue];
}
{{< /highlight >}}

**State Management:**

{{< highlight jsx "linenos=inline">}}
// Context API for global state
const ThemeContext = React.createContext();

function ThemeProvider({ children }) {
  const [theme, setTheme] = useState('light');
  
  const toggleTheme = () => {
    setTheme(prev => prev === 'light' ? 'dark' : 'light');
  };

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

// useContext hook
function ThemedButton() {
  const { theme, toggleTheme } = useContext(ThemeContext);
  
  return (
    <button 
      onClick={toggleTheme}
      style={{ 
        backgroundColor: theme === 'light' ? '#fff' : '#333',
        color: theme === 'light' ? '#333' : '#fff'
      }}
    >
      Toggle theme (current: {theme})
    </button>
  );
}

// useReducer for complex state logic
function todoReducer(state, action) {
  switch (action.type) {
    case 'ADD_TODO':
      return [...state, { id: Date.now(), text: action.text, completed: false }];
    case 'TOGGLE_TODO':
      return state.map(todo =>
        todo.id === action.id ? { ...todo, completed: !todo.completed } : todo
      );
    case 'DELETE_TODO':
      return state.filter(todo => todo.id !== action.id);
    default:
      return state;
  }
}

function TodoApp() {
  const [todos, dispatch] = useReducer(todoReducer, []);
  const [inputText, setInputText] = useState('');

  const addTodo = () => {
    if (inputText.trim()) {
      dispatch({ type: 'ADD_TODO', text: inputText });
      setInputText('');
    }
  };

  return (
    <div>
      <input 
        value={inputText}
        onChange={(e) => setInputText(e.target.value)}
        onKeyPress={(e) => e.key === 'Enter' && addTodo()}
      />
      <button onClick={addTodo}>Add Todo</button>
      <ul>
        {todos.map(todo => (
          <li key={todo.id}>
            <span 
              style={{ textDecoration: todo.completed ? 'line-through' : 'none' }}
              onClick={() => dispatch({ type: 'TOGGLE_TODO', id: todo.id })}
            >
              {todo.text}
            </span>
            <button onClick={() => dispatch({ type: 'DELETE_TODO', id: todo.id })}>
              Delete
            </button>
          </li>
        ))}
      </ul>
    </div>
  );
}
{{< /highlight >}}

**React Router for Navigation:**

{{< highlight jsx "linenos=inline">}}
import { BrowserRouter as Router, Routes, Route, Link, useParams } from 'react-router-dom';

function App() {
  return (
    <Router>
      <nav>
        <Link to="/">Home</Link>
        <Link to="/about">About</Link>
        <Link to="/users">Users</Link>
      </nav>

      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/users" element={<Users />} />
        <Route path="/users/:id" element={<UserProfile />} />
      </Routes>
    </Router>
  );
}

function UserProfile() {
  const { id } = useParams();
  return <div>User Profile for ID: {id}</div>;
}
{{< /highlight >}}

**Performance Optimization:**

{{< highlight jsx "linenos=inline">}}
import React, { memo, useMemo, useCallback } from 'react';

// React.memo prevents unnecessary re-renders
const ExpensiveComponent = memo(function ExpensiveComponent({ data, onUpdate }) {
  const processedData = useMemo(() => {
    // Expensive calculation only runs when data changes
    return data.map(item => ({ ...item, processed: true }));
  }, [data]);

  const handleUpdate = useCallback((id) => {
    // Function reference stays stable unless onUpdate changes
    onUpdate(id);
  }, [onUpdate]);

  return (
    <div>
      {processedData.map(item => (
        <div key={item.id} onClick={() => handleUpdate(item.id)}>
          {item.name}
        </div>
      ))}
    </div>
  );
});
{{< /highlight >}}

## Advanced Information

Advanced React development involves sophisticated patterns, performance optimization, and integration with complex tooling ecosystems.

**Advanced Hooks and Patterns:**

{{< highlight jsx "linenos=inline">}}
// useImperativeHandle for exposing component methods
const FancyInput = forwardRef((props, ref) => {
  const inputRef = useRef();

  useImperativeHandle(ref, () => ({
    focus: () => {
      inputRef.current.focus();
    },
    getValue: () => {
      return inputRef.current.value;
    }
  }));

  return <input ref={inputRef} {...props} />;
});

// Custom hook with cleanup
function useWebSocket(url) {
  const [socket, setSocket] = useState(null);
  const [lastMessage, setLastMessage] = useState(null);

  useEffect(() => {
    const ws = new WebSocket(url);

    ws.onmessage = (event) => {
      setLastMessage(JSON.parse(event.data));
    };

    setSocket(ws);

    return () => {
      ws.close();
    };
  }, [url]);

  const sendMessage = useCallback((message) => {
    if (socket && socket.readyState === WebSocket.OPEN) {
      socket.send(JSON.stringify(message));
    }
  }, [socket]);

  return { lastMessage, sendMessage };
}

// Error Boundaries
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    return { hasError: true };
  }

  componentDidCatch(error, errorInfo) {
    console.error('Error caught by boundary:', error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      return <h1>Something went wrong.</h1>;
    }

    return this.props.children;
  }
}
{{< /highlight >}}

**Server-Side Rendering (SSR) with Next.js:**

{{< highlight jsx "linenos=inline">}}
// pages/users/[id].js in Next.js
import { GetServerSideProps } from 'next';

export default function UserPage({ user }) {
  return (
    <div>
      <h1>{user.name}</h1>
      <p>{user.email}</p>
    </div>
  );
}

export const getServerSideProps: GetServerSideProps = async (context) => {
  const { id } = context.params;
  const res = await fetch(`${process.env.API_URL}/users/${id}`);
  const user = await res.json();

  return {
    props: { user },
  };
};

// Static Generation
export const getStaticProps = async () => {
  const res = await fetch(`${process.env.API_URL}/users`);
  const users = await res.json();

  return {
    props: { users },
    revalidate: 60, // Regenerate every 60 seconds
  };
};
{{< /highlight >}}

**State Management with Redux Toolkit:**

{{< highlight javascript "linenos=inline">}}
import { createSlice, configureStore } from '@reduxjs/toolkit';

const userSlice = createSlice({
  name: 'user',
  initialState: {
    data: null,
    loading: false,
    error: null
  },
  reducers: {
    fetchUserStart: (state) => {
      state.loading = true;
      state.error = null;
    },
    fetchUserSuccess: (state, action) => {
      state.loading = false;
      state.data = action.payload;
    },
    fetchUserFailure: (state, action) => {
      state.loading = false;
      state.error = action.payload;
    }
  }
});

const store = configureStore({
  reducer: {
    user: userSlice.reducer
  }
});

// React component using Redux
import { useSelector, useDispatch } from 'react-redux';

function UserComponent() {
  const { data, loading, error } = useSelector(state => state.user);
  const dispatch = useDispatch();

  useEffect(() => {
    dispatch(fetchUserStart());
    fetch('/api/user')
      .then(res => res.json())
      .then(data => dispatch(fetchUserSuccess(data)))
      .catch(err => dispatch(fetchUserFailure(err.message)));
  }, [dispatch]);

  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error: {error}</div>;
  if (!data) return <div>No user data</div>;

  return <div>Welcome, {data.name}!</div>;
}
{{< /highlight >}}

**Testing React Components:**

{{< highlight javascript "linenos=inline">}}
import { render, screen, fireEvent, waitFor } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import '@testing-library/jest-dom';

// Unit test for a component
test('renders user information', () => {
  const user = { name: 'John Doe', email: 'john@example.com' };
  render(<UserProfile user={user} />);
  
  expect(screen.getByText('John Doe')).toBeInTheDocument();
  expect(screen.getByText('john@example.com')).toBeInTheDocument();
});

// Integration test with user interactions
test('adds todo item when form is submitted', async () => {
  const user = userEvent.setup();
  render(<TodoApp />);
  
  const input = screen.getByLabelText('New todo');
  const button = screen.getByRole('button', { name: 'Add Todo' });
  
  await user.type(input, 'Learn React Testing');
  await user.click(button);
  
  expect(screen.getByText('Learn React Testing')).toBeInTheDocument();
});

// Mocking API calls
test('fetches and displays user data', async () => {
  const mockUser = { id: 1, name: 'Jane Doe' };
  
  global.fetch = jest.fn(() =>
    Promise.resolve({
      json: () => Promise.resolve(mockUser),
    })
  );

  render(<UserData userId={1} />);
  
  await waitFor(() => {
    expect(screen.getByText('Jane Doe')).toBeInTheDocument();
  });
  
  expect(fetch).toHaveBeenCalledWith('/api/users/1');
});
{{< /highlight >}}

**Enterprise React Architecture:**

- **Micro-frontends**: Module federation with Webpack 5
- **Design Systems**: Storybook for component documentation
- **Code Splitting**: Dynamic imports and React.lazy()
- **Performance Monitoring**: React DevTools, Lighthouse
- **Build Optimization**: Webpack, Vite, or Parcel bundlers
- **Deployment**: Vercel, Netlify, or containerized deployments

React's ecosystem continues to evolve with innovations like React Server Components, Concurrent Features, and improved developer tools. Its large community and extensive ecosystem make it a powerful choice for modern web development.

## External Links

- [React Documentation](https://react.dev/) @ React
- [React Tutorial](https://react.dev/learn) @ React
- [Create React App](https://create-react-app.dev/) @ Create React App
