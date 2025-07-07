---
title: "What is Svelte?"
description: "Just what is Svelte and how does it differ from traditional JavaScript frameworks?"
lead: "Just what is Svelte and how does it differ from traditional JavaScript frameworks?"
date: 2023-05-01T04:46:31+00:00
lastmod: 2023-12-04T11:30:00+01:00
draft: false
images: []
menu:
  docs:
    parent: "svelte"
weight: 100
toc: true
---

## 10,000 ft Overview

Svelte is a radical new approach to building user interfaces that shifts the work from the browser to a compile step. Unlike traditional frameworks like [React]({{< relref "what-is-react" >}}) and [Angular]({{< relref "what-is-angular" >}}) that do most of their work in the browser, Svelte compiles your components into highly optimized vanilla [JavaScript]({{< relref "what-is-javascript" >}}) at build time.

Created by Rich Harris at The New York Times, Svelte has gained significant traction for its innovative approach to web development. Instead of using techniques like virtual DOM diffing, Svelte writes code that surgically updates the DOM when the state of your app changes, resulting in exceptionally fast and efficient applications.

Svelte applications can be built using [Node.js]({{< relref "what-are-npm-and-nodejs" >}}) and enhanced with [TypeScript]({{< relref "what-is-typescript" >}}) for improved developer experience. The framework is often paired with SvelteKit, a full-stack application framework that provides routing, server-side rendering, and other advanced features.

{{< alert icon="💡" text="Svelte is both a compile-time tool and a runtime library. It transforms your declarative components into efficient JavaScript code that manipulates the DOM directly, eliminating the need for a virtual DOM." />}}

## Beginner Information

Svelte components are written in `.svelte` files that combine HTML, CSS, and JavaScript in a single file. The syntax is designed to be intuitive and close to standard web technologies.

**Basic Svelte Component:**

{{< highlight svelte "linenos=inline">}}
<script>
  // Component logic
  let name = 'World';
  let count = 0;
  
  function increment() {
    count += 1;
  }
</script>

<!-- HTML template -->
<main>
  <h1>Hello {name}!</h1>
  <button on:click={increment}>
    Clicked {count} {count === 1 ? 'time' : 'times'}
  </button>
</main>

<!-- Component styles -->
<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }
  
  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }
  
  button {
    background: #ff3e00;
    color: white;
    border: none;
    padding: 0.5em 1em;
    border-radius: 4px;
    cursor: pointer;
  }
</style>
{{< /highlight >}}

**Reactive Programming:**

{{< highlight svelte "linenos=inline">}}
<script>
  let firstName = 'John';
  let lastName = 'Doe';
  
  // Reactive declaration - automatically updates when dependencies change
  $: fullName = `${firstName} ${lastName}`;
  
  // Reactive statement - runs when dependencies change
  $: {
    console.log(`Full name changed to: ${fullName}`);
  }
  
  // Reactive statement with condition
  $: if (fullName.length > 10) {
    console.log('That\'s a long name!');
  }
</script>

<div>
  <input bind:value={firstName} placeholder="First name">
  <input bind:value={lastName} placeholder="Last name">
  <p>Hello {fullName}!</p>
</div>
{{< /highlight >}}

**Props and Component Communication:**

{{< highlight svelte "linenos=inline">}}
<!-- Child.svelte -->
<script>
  export let message = 'Default message';
  export let count = 0;
  
  import { createEventDispatcher } from 'svelte';
  
  const dispatch = createEventDispatcher();
  
  function handleClick() {
    dispatch('clicked', {
      message: 'Button was clicked!',
      count: count + 1
    });
  }
</script>

<button on:click={handleClick}>
  {message} (clicked {count} times)
</button>

<!-- Parent.svelte -->
<script>
  import Child from './Child.svelte';
  
  let count = 0;
  
  function handleChildClick(event) {
    count = event.detail.count;
    console.log(event.detail.message);
  }
</script>

<Child 
  message="Click me!" 
  {count} 
  on:clicked={handleChildClick} 
/>
{{< /highlight >}}

**Getting Started:**

{{< highlight bash >}}
# Create a new Svelte project
npm create svelte@latest my-app
cd my-app
npm install

# Start development server
npm run dev

# Build for production
npm run build
{{< /highlight >}}

**Key Svelte Concepts:**

- **Components**: Single-file components with HTML, CSS, and JavaScript
- **Reactivity**: Automatic updates when data changes using `$:` syntax
- **Props**: Data passed to components via `export let`
- **Events**: Custom events dispatched from child to parent components
- **Stores**: Global state management with built-in reactivity
- **Transitions**: Built-in animations and transitions

## Intermediary Information

Svelte provides advanced features for building sophisticated applications with excellent performance characteristics.

**Stores for State Management:**

{{< highlight javascript "linenos=inline">}}
// stores.js
import { writable, readable, derived } from 'svelte/store';

// Writable store
export const count = writable(0);

// Readable store
export const time = readable(new Date(), function start(set) {
  const interval = setInterval(() => {
    set(new Date());
  }, 1000);

  return function stop() {
    clearInterval(interval);
  };
});

// Derived store
export const elapsed = derived(
  time,
  $time => Math.round(($time - start) / 1000)
);

// Custom store with methods
function createCounter() {
  const { subscribe, set, update } = writable(0);

  return {
    subscribe,
    increment: () => update(n => n + 1),
    decrement: () => update(n => n - 1),
    reset: () => set(0)
  };
}

export const counter = createCounter();
{{< /highlight >}}

**Using Stores in Components:**

{{< highlight svelte "linenos=inline">}}
<script>
  import { count, time, counter } from './stores.js';
  
  // Auto-subscription with $
  $: console.log('Count is:', $count);
  
  // Manual subscription
  let unsubscribe = count.subscribe(value => {
    console.log('Count changed to:', value);
  });
  
  // Cleanup subscription
  import { onDestroy } from 'svelte';
  onDestroy(unsubscribe);
</script>

<div>
  <h2>Count: {$count}</h2>
  <button on:click={() => count.update(n => n + 1)}>+</button>
  <button on:click={() => count.set(0)}>Reset</button>
  
  <h2>Time: {$time}</h2>
  
  <h2>Counter Store</h2>
  <p>{$counter}</p>
  <button on:click={counter.increment}>+</button>
  <button on:click={counter.decrement}>-</button>
  <button on:click={counter.reset}>Reset</button>
</div>
{{< /highlight >}}

**Advanced Component Features:**

{{< highlight svelte "linenos=inline">}}
<script>
  import { onMount, onDestroy, beforeUpdate, afterUpdate } from 'svelte';
  
  let mounted = false;
  
  // Lifecycle hooks
  onMount(() => {
    console.log('Component mounted');
    mounted = true;
  });
  
  onDestroy(() => {
    console.log('Component destroyed');
  });
  
  beforeUpdate(() => {
    console.log('Before update');
  });
  
  afterUpdate(() => {
    console.log('After update');
  });
  
  // Conditional rendering
  let showDetails = false;
  
  // Each blocks for lists
  let items = ['Apple', 'Banana', 'Orange'];
  
  // Await blocks for promises
  let promise = fetchData();
  
  async function fetchData() {
    const response = await fetch('/api/data');
    return response.json();
  }
</script>

{#if mounted}
  <div>
    <h2>Component is mounted!</h2>

    <button on:click={() => showDetails = !showDetails}>
      {showDetails ? 'Hide' : 'Show'} Details
    </button>
    
    {#if showDetails}
      <div transition:slide>
        <h3>Details</h3>
        <ul>
          {#each items as item, i}
            <li>{i + 1}: {item}</li>
          {/each}
        </ul>
      </div>
    {/if}
    
    {#await promise}
      <p>Loading...</p>
    {:then data}
      <p>Data: {JSON.stringify(data)}</p>
    {:catch error}
      <p>Error: {error.message}</p>
    {/await}
  </div>
{/if}
{{< /highlight >}}

**Transitions and Animations:**

{{< highlight svelte "linenos=inline">}}
<script>
  import { fade, fly, slide, scale } from 'svelte/transition';
  import { flip } from 'svelte/animate';
  import { quintOut } from 'svelte/easing';
  
  let visible = true;
  let items = [1, 2, 3, 4, 5];
  
  function remove(item) {
    items = items.filter(i => i !== item);
  }
  
  function add() {
    items = [...items, Math.max(...items) + 1];
  }
</script>

<button on:click={() => visible = !visible}>
  {visible ? 'Hide' : 'Show'}
</button>

{#if visible}
  <div transition:fade={{ duration: 300 }}>
    <h2>Animated Content</h2>
  </div>
{/if}

<div>
  <button on:click={add}>Add item</button>
  {#each items as item (item)}
    <div 
      animate:flip={{ duration: 300 }}
      in:fly={{ x: 200, duration: 300 }}
      out:scale={{ duration: 300, easing: quintOut }}
    >
      {item}
      <button on:click={() => remove(item)}>Remove</button>
    </div>
  {/each}
</div>
{{< /highlight >}}

**Slots and Component Composition:**

{{< highlight svelte "linenos=inline">}}
<!-- Modal.svelte -->
<script>
  export let title = 'Modal';
  export let visible = false;
</script>

{#if visible}
  <div class="modal-backdrop">
    <div class="modal">
      <header>
        <h2>{title}</h2>
        <slot name="header"></slot>
      </header>

      <main>
        <slot></slot>
      </main>
      
      <footer>
        <slot name="footer">
          <button on:click={() => visible = false}>Close</button>
        </slot>
      </footer>
    </div>
  </div>
{/if}

<!-- Usage -->
<script>
  import Modal from './Modal.svelte';
  let showModal = false;
</script>

<Modal bind:visible={showModal} title="Confirm Action">
  <p>Are you sure you want to proceed?</p>
  
  <div slot="footer">
    <button on:click={() => showModal = false}>Cancel</button>
    <button on:click={() => { showModal = false; confirm(); }}>Confirm</button>
  </div>
</Modal>
{{< /highlight >}}

## Advanced Information

Advanced Svelte development involves performance optimization, architectural patterns, and integration with modern development tooling.

**SvelteKit - Full-Stack Framework:**

{{< highlight javascript "linenos=inline">}}
// src/routes/+layout.svelte
<script>
  import { page } from '$app/stores';
  import { navigating } from '$app/stores';
</script>

<nav>
  <a href="/" class:active={$page.url.pathname === '/'}>Home</a>
  <a href="/about" class:active={$page.url.pathname === '/about'}>About</a>
  <a href="/blog" class:active={$page.url.pathname.startsWith('/blog')}>Blog</a>
</nav>

{#if $navigating}
  <div class="loading">Loading...</div>
{/if}

<main>
  <slot />
</main>

<style>
  nav {
    display: flex;
    gap: 1rem;
    padding: 1rem;
    background: #f0f0f0;
  }
  
  .active {
    font-weight: bold;
    color: #ff3e00;
  }
  
  .loading {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    background: #ff3e00;
    color: white;
    padding: 0.5rem;
    text-align: center;
  }
</style>
{{< /highlight >}}

**Server-Side Rendering and API Routes:**

{{< highlight javascript "linenos=inline">}}
// src/routes/blog/+page.server.js
import { error } from '@sveltejs/kit';

export async function load({ fetch }) {
  try {
    const response = await fetch('/api/posts');
    const posts = await response.json();

    return {
      posts
    };
  } catch (err) {
    throw error(500, 'Failed to load posts');
  }
}

// src/routes/api/posts/+server.js
import { json } from '@sveltejs/kit';

export async function GET() {
  const posts = await getPosts(); // Your data fetching logic
  return json(posts);
}

export async function POST({ request }) {
  const data = await request.json();
  const post = await createPost(data);
  return json(post, { status: 201 });
}

// src/routes/blog/+page.svelte
<script>
  export let data;
  
  $: ({ posts } = data);
</script>

<h1>Blog Posts</h1>
{#each posts as post}
  <article>
    <h2><a href="/blog/{post.slug}">{post.title}</a></h2>
    <p>{post.excerpt}</p>
  </article>
{/each}
{{< /highlight >}}

**Advanced State Management Patterns:**

{{< highlight javascript "linenos=inline">}}
// Advanced store with persistence
import { writable } from 'svelte/store';
import { browser } from '$app/environment';

function createPersistedStore(key, initialValue) {
  let stored = initialValue;
  
  if (browser) {
    const item = localStorage.getItem(key);
    if (item) stored = JSON.parse(item);
  }
  
  const store = writable(stored);
  
  return {
    subscribe: store.subscribe,
    set: (value) => {
      if (browser) localStorage.setItem(key, JSON.stringify(value));
      store.set(value);
    },
    update: (fn) => {
      store.update((value) => {
        const newValue = fn(value);
        if (browser) localStorage.setItem(key, JSON.stringify(newValue));
        return newValue;
      });
    }
  };
}

// Store with async actions
function createAsyncStore(initialValue, asyncFn) {
  const store = writable(initialValue);
  const loading = writable(false);
  const error = writable(null);
  
  return {
    subscribe: store.subscribe,
    loading: { subscribe: loading.subscribe },
    error: { subscribe: error.subscribe },

    async load(...args) {
      loading.set(true);
      error.set(null);
      
      try {
        const result = await asyncFn(...args);
        store.set(result);
        return result;
      } catch (err) {
        error.set(err);
        throw err;
      } finally {
        loading.set(false);
      }
    }
  };
}

// Usage
export const userStore = createAsyncStore(null, async (userId) => {
  const response = await fetch(`/api/users/${userId}`);
  return response.json();
});
{{< /highlight >}}

**Performance Optimization:**

{{< highlight svelte "linenos=inline">}}
<script>
  import { onMount } from 'svelte';
  
  // Lazy loading components
  let LazyComponent;
  
  onMount(async () => {
    const module = await import('./LazyComponent.svelte');
    LazyComponent = module.default;
  });
  
  // Virtual scrolling for large lists
  import { createVirtualList } from '@sveltejs/svelte-virtual-list';
  
  const items = Array.from({ length: 10000 }, (_, i) => `Item ${i}`);
  
  // Memoization pattern
  let expensiveResult;
  let lastInput;
  
  function expensiveComputation(input) {
    if (input === lastInput) return expensiveResult;

    // Expensive calculation
    expensiveResult = input.split('').reverse().join('');
    lastInput = input;

    return expensiveResult;
  }
  
  // Component-level optimization
  export let data;
  
  // Only re-render when specific props change
  $: processedData = expensiveComputation(data.input);
</script>

<!-- Conditional component loading -->
{#if LazyComponent}
  <svelte:component this={LazyComponent} />
{:else}
  <div>Loading component...</div>
{/if}

<!-- Virtual list for performance -->
<div class="container">
  <svelte:component 
    this={createVirtualList(items)} 
    let:item
  >
    <div class="item">{item}</div>
  </svelte:component>
</div>
{{< /highlight >}}

**Testing Svelte Applications:**

{{< highlight javascript "linenos=inline">}}
// Component.test.js
import { render, fireEvent, screen } from '@testing-library/svelte';
import { expect, test } from 'vitest';
import Component from './Component.svelte';

test('renders component with props', () => {
  render(Component, { props: { name: 'Test' } });
  
  expect(screen.getByText('Hello Test!')).toBeInTheDocument();
});

test('handles user interaction', async () => {
  render(Component);
  
  const button = screen.getByRole('button');
  await fireEvent.click(button);
  
  expect(screen.getByText('Button clicked!')).toBeInTheDocument();
});

// Store testing
import { get } from 'svelte/store';
import { counter } from './stores.js';

test('counter store increments correctly', () => {
  counter.reset();
  expect(get(counter)).toBe(0);
  
  counter.increment();
  expect(get(counter)).toBe(1);
  
  counter.decrement();
  expect(get(counter)).toBe(0);
});
{{< /highlight >}}

**Build and Deployment Optimization:**

{{< highlight javascript "linenos=inline">}}
// vite.config.js
import { sveltekit } from '@sveltejs/kit/vite';
import { defineConfig } from 'vite';

export default defineConfig({
  plugins: [sveltekit()],
  build: {
    rollupOptions: {
      output: {
        manualChunks: {
          vendor: ['svelte', '@sveltejs/kit'],
          utils: ['lodash', 'date-fns']
        }
      }
    }
  },
  optimizeDeps: {
    include: ['lodash', 'date-fns']
  }
});

// svelte.config.js
import adapter from '@sveltejs/adapter-auto';
import { vitePreprocess } from '@sveltejs/kit/vite';

export default {
  preprocess: vitePreprocess(),
  kit: {
    adapter: adapter(),
    prerender: {
      entries: ['*']
    }
  },
  compilerOptions: {
    hydratable: true
  }
};
{{< /highlight >}}

Svelte represents a paradigm shift in frontend development, offering exceptional performance through compile-time optimization while maintaining developer-friendly syntax. Its growing ecosystem, including SvelteKit for full-stack development, makes it an increasingly popular choice for modern web applications.

## External Links

- [Svelte Documentation](https://svelte.dev/docs) @ Svelte
- [SvelteKit Documentation](https://kit.svelte.dev/docs) @ SvelteKit
- [Svelte Tutorial](https://svelte.dev/tutorial) @ Svelte