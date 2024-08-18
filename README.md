# preact-headquarters

preact-headquarters is a lightweight, high-performance header component for Preact applications. It allows you to create a dynamic header that hides when scrolling down and shows when scrolling up, providing a smooth and intuitive user experience.

## Table of Contents

- [Installation](#installation)
- [Basic Usage](#basic-usage)
- [Examples](#examples)
  - [Simple Static Header](#simple-static-header)
  - [Custom Styling](#custom-styling)
  - [With Callbacks](#with-callbacks)
  - [Sticky on Scroll Up](#sticky-on-scroll-up)
  - [Dynamic Styles](#dynamic-styles)
  - [Disabling on Large Screens](#disabling-on-large-screens)
  - [Sidebar Implementation](#sidebar-implementation)
- [API](#api)
- [Styling](#styling)

## Installation

```bash
npm install preact-headquarters
```

or

```bash
yarn add preact-headquarters
```

## Basic Usage

```jsx
import { h } from 'preact';
import HeadQuarters from 'preact-headquarters';
import 'preact-headquarters/style.css';

function App() {
  return (
    <div>
      <HeadQuarters>
        <header style={{ backgroundColor: '#f0f0f0', padding: '1rem' }}>
          <h1>My Website</h1>
          <nav>
            <a href="#home">Home</a>
            <a href="#about">About</a>
            <a href="#contact">Contact</a>
          </nav>
        </header>
      </HeadQuarters>
      {/* Rest of your app content */}
    </div>
  );
}

export default App;
```

## Examples

### Simple Static Header

```jsx
import { h } from 'preact';
import HeadQuarters from 'preact-headquarters';
import 'preact-headquarters/style.css';

function App() {
  return (
    <div>
      <HeadQuarters pinStart={0}>
        <header style={{ backgroundColor: '#f0f0f0', padding: '1rem' }}>
          <h1>Static Header</h1>
        </header>
      </HeadQuarters>
      {/* Content */}
    </div>
  );
}
```

### Custom Styling

```jsx
import { h } from 'preact';
import HeadQuarters from 'preact-headquarters';
import 'preact-headquarters/style.css';

function App() {
  return (
    <div>
      <HeadQuarters
        className="custom-header"
        pinnedClassName="header-pinned"
        unpinnedClassName="header-unpinned"
        wrapperStyle={{ boxShadow: '0 2px 4px rgba(0,0,0,0.1)' }}
      >
        <header style={{ backgroundColor: '#f0f0f0', padding: '1rem' }}>
          <h1>Custom Styled Header</h1>
        </header>
      </HeadQuarters>
      {/* Content */}
    </div>
  );
}
```

### With Callbacks

```jsx
import { h } from 'preact';
import HeadQuarters from 'preact-headquarters';
import 'preact-headquarters/style.css';

function App() {
  const handlePin = () => console.log('Header pinned');
  const handleUnpin = () => console.log('Header unpinned');

  return (
    <div>
      <HeadQuarters onPin={handlePin} onUnpin={handleUnpin}>
        <header style={{ backgroundColor: '#f0f0f0', padding: '1rem' }}>
          <h1>Header with Callbacks</h1>
        </header>
      </HeadQuarters>
      {/* Content */}
    </div>
  );
}
```

### Sticky on Scroll Up

```jsx
import { h } from 'preact';
import HeadQuarters from 'preact-headquarters';
import 'preact-headquarters/style.css';

function App() {
  return (
    <div>
      <HeadQuarters stickyOnScrollUp={true} upTolerance={5}>
        <header style={{ backgroundColor: '#f0f0f0', padding: '1rem' }}>
          <h1>Sticky on Scroll Up Header</h1>
        </header>
      </HeadQuarters>
      {/* Content */}
    </div>
  );
}
```

### Dynamic Styles

```jsx
import { h } from 'preact';
import HeadQuarters from 'preact-headquarters';
import 'preact-headquarters/style.css';

function App() {
  const dynamicStyles = (state) => ({
    opacity: state.pinned ? 1 : 0.8,
    backgroundColor: state.top ? 'transparent' : '#f0f0f0',
  });

  return (
    <div>
      <HeadQuarters dynamicStyles={dynamicStyles}>
        <header style={{ padding: '1rem' }}>
          <h1>Dynamic Styled Header</h1>
        </header>
      </HeadQuarters>
      {/* Content */}
    </div>
  );
}
```

### Disabling on Large Screens

```jsx
import { h } from 'preact';
import { useState, useEffect } from 'preact/hooks';
import HeadQuarters from 'preact-headquarters';
import 'preact-headquarters/style.css';

function App() {
  const [isLargeScreen, setIsLargeScreen] = useState(window.innerWidth > 1024);

  useEffect(() => {
    const handleResize = () => setIsLargeScreen(window.innerWidth > 1024);
    window.addEventListener('resize', handleResize);
    return () => window.removeEventListener('resize', handleResize);
  }, []);

  return (
    <div>
      <HeadQuarters disable={isLargeScreen}>
        <header style={{ backgroundColor: '#f0f0f0', padding: '1rem' }}>
          <h1>Responsive Header</h1>
        </header>
      </HeadQuarters>
      {/* Content */}
    </div>
  );
}
```

### Sidebar Implementation

```jsx
import { h } from 'preact';
import HeadQuarters from 'preact-headquarters';
import 'preact-headquarters/style.css';

function App() {
  return (
    <div style={{ display: 'flex' }}>
      <HeadQuarters
        wrapperStyle={{
          position: 'fixed',
          top: 0,
          left: 0,
          width: '250px',
          height: '100vh',
          transform: 'translateX(-100%)',
        }}
        unpinnedClassName="sidebar-unpinned"
      >
        <nav style={{ backgroundColor: '#f0f0f0', height: '100%', padding: '1rem' }}>
          <h2>Sidebar</h2>
          {/* Sidebar content */}
        </nav>
      </HeadQuarters>
      <main style={{ marginLeft: '250px' }}>
        {/* Main content */}
      </main>
    </div>
  );
}
```

## API

HeadQuarters accepts the following props:

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `children` | Node | - | The content to be rendered inside the header |
| `pinStart` | Number | 0 | The scroll position at which the header should start pinning/unpinning |
| `height` | Number | 60 | The height of the header in pixels |
| `unpinTolerance` | Number | 6 | The number of pixels to scroll before unpinning the header |
| `className` | String | '' | Additional CSS class for the component |
| `pinnedClassName` | String | '' | CSS class applied when the header is pinned |
| `unpinnedClassName` | String | '' | CSS class applied when the header is unpinned |
| `disableInlineStyles` | Boolean | false | If true, disables all inline styles |
| `onPin` | Function | - | Callback function called when the header is pinned |
| `onUnpin` | Function | - | Callback function called when the header is unpinned |
| `disable` | Boolean | false | If true, disables the HeadQuarters functionality |
| `downTolerance` | Number | 5 | The number of pixels to scroll down before unpinning |
| `upTolerance` | Number | 10 | The number of pixels to scroll up before pinning |
| `stickyOnScrollUp` | Boolean | false | If true, keeps the header visible when scrolling up |
| `transitionDuration` | Number | 200 | The duration of the pin/unpin animation in milliseconds |
| `wrapperStyle` | Object | {} | Additional inline styles for the wrapper element |
| `wrapperClassName` | String | '' | Additional CSS class for the wrapper element |
| `calcHeightOnResize` | Boolean | false | If true, recalculates the header height on window resize |
| `pinOnReset` | Boolean | true | If true, pins the header when scrolling back to the top of the page |
| `dynamicStyles` | Function | null | A function that returns an object of styles based on the current state |

## Styling

HeadQuarters comes with a set of default styles and utility classes. You can customize these or add your own classes as needed.

### Default Classes

- `.headquarters`: Applied to the wrapper div of the component.
- `.headquarters--pinned`: Applied when the header is pinned (visible).
- `.headquarters--unpinned`: Applied when the header is unpinned (hidden).
- `.headquarters--top`: Applied when the header is at the top of the page.
- `.headquarters--not-top`: Applied when the header is not at the top of the page.
- `.headquarters--scrolling-up`: Applied when scrolling up.
- `.headquarters--scrolling-down`: Applied when scrolling down.

### Utility Classes

- `.hq-shadow`: Adds a subtle box shadow to the header.
- `.hq-transparent`: Makes the header background transparent.
- `.hq-solid`: Gives the header a solid white background.
- `.hq-animated`: Adds a transition effect to all properties.
- `.hq-disable-large`: Disables the HeadQuarters effect on larger screens (use with a media query).
- `.hq-sidebar`: Styles for using HeadQuarters with a sidebar instead of a top header.
