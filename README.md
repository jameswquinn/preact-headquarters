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

## Comparison with headroom.js

preact-headquarters is inspired by the popular headroom.js library but tailored specifically for Preact applications. Here's a comparison between preact-headquarters and headroom.js:

### Similarities

1. **Core Functionality**: Both libraries provide a way to hide the header when scrolling down and show it when scrolling up.
2. **Customizable Tolerances**: Both allow you to set tolerances for when the header should pin/unpin.
3. **Classes for Styling**: Both add classes to the header element to indicate its current state (pinned, unpinned, top, not-top).
4. **Callback Support**: Both provide callbacks for pin and unpin events.

### Differences

1. **Framework**: 
   - preact-headquarters: Built specifically for Preact applications.
   - headroom.js: Framework-agnostic, can be used with vanilla JavaScript or any framework.

2. **Installation and Usage**:
   - preact-headquarters: Installed via npm and used as a Preact component.
   - headroom.js: Can be included via script tag or installed via npm, requires initialization.

3. **Performance**:
   - preact-headquarters: Uses Preact's efficient rendering and state management.
   - headroom.js: Uses vanilla JavaScript, may require additional setup for optimal performance in React-like environments.

4. **Bundle Size**:
   - preact-headquarters: Smaller bundle size when used in Preact applications (as it leverages Preact's existing code).
   - headroom.js: Slightly larger as it's a standalone library.

5. **API and Configuration**:
   - preact-headquarters: Configuration is done via props in a declarative manner.
   - headroom.js: Configuration is done via a options object in an imperative manner.

6. **TypeScript Support**:
   - preact-headquarters: Built with Preact, easy to add TypeScript definitions.
   - headroom.js: Requires separate TypeScript definitions.

7. **Additional Features in preact-headquarters**:
   - Dynamic styles based on scroll state
   - Easy integration with Preact's state management
   - Built-in support for calculating height on resize

### When to Choose preact-headquarters

1. You're building a Preact application.
2. You want a more declarative API that fits well with Preact's component model.
3. You need tight integration with Preact's state management and lifecycle.
4. You want additional features like dynamic styles based on scroll state.

### When to Choose headroom.js

1. You need a framework-agnostic solution.
2. You're working with vanilla JavaScript or a non-React-like framework.
3. You need to support older browsers without transpilation.

### Code Comparison

#### preact-headquarters

```jsx
import { h } from 'preact';
import HeadQuarters from 'preact-headquarters';

function App() {
  return (
    <HeadQuarters
      pinStart={100}
      upTolerance={5}
      downTolerance={10}
      onPin={() => console.log('Pinned')}
      onUnpin={() => console.log('Unpinned')}
    >
      <header>
        <h1>My Website</h1>
      </header>
    </HeadQuarters>
  );
}
```

#### headroom.js

```html
<header id="header"></header>

<script src="https://unpkg.com/headroom.js"></script>
<script>
var myElement = document.querySelector("#header");
var headroom  = new Headroom(myElement, {
  offset : 100,
  tolerance : {
    up : 5,
    down : 10
  },
  onPin : function() {
    console.log('Pinned');
  },
  onUnpin : function() {
    console.log('Unpinned');
  }
});
headroom.init();
</script>
```

In conclusion, while both libraries provide similar core functionality, preact-headquarters offers a more integrated and streamlined experience for Preact applications, with some additional features and a more declarative API.

## FAQ

### Q: How do I change the animation speed of the header?

A: You can adjust the animation speed by setting the `transitionDuration` prop. This value is in milliseconds, so `transitionDuration={500}` would result in a half-second animation.

### Q: Can I use preact-headquarters with a sidebar instead of a top header?

A: Yes, you can adapt preact-headquarters for a sidebar. See the "Sidebar Implementation" example in Part 1 of the README for a basic implementation. You'll need to adjust the styles to translate on the X-axis instead of the Y-axis.

### Q: How can I make the header always visible on larger screens?

A: You can use the `disable` prop in combination with a media query or JavaScript-based check. See the "Disabling on Large Screens" example in Part 1 of the README for an implementation.

### Q: The header flickers on iOS devices. How can I fix this?

A: This is a common issue with fixed positioning on iOS. You can try adding `transform: translateZ(0)` to your header styles to force hardware acceleration:

```jsx
<HeadQuarters wrapperStyle={{ transform: 'translateZ(0)' }}>
  <header>{/* Header content */}</header>
</HeadQuarters>
```

### Q: How do I make the header hide immediately when scrolling down?

A: Set the `downTolerance` prop to 0:

```jsx
<HeadQuarters downTolerance={0}>
  <header>{/* Header content */}</header>
</HeadQuarters>
```

### Q: Can I change the header's appearance based on its state?

A: Yes, you can use the `dynamicStyles` prop to apply different styles based on the header's state. See the "Dynamic Styles" example in Part 1 of the README for an implementation.

### Q: How do I handle content that changes the header's height?

A: Use the `calcHeightOnResize` prop to recalculate the header's height when the window resizes:

```jsx
<HeadQuarters calcHeightOnResize={true}>
  <header>{/* Header content that might change height */}</header>
</HeadQuarters>
```

### Q: Can I use preact-headquarters with other frameworks or vanilla JavaScript?

A: preact-headquarters is designed specifically for Preact. While it's not directly compatible with other frameworks, you could potentially adapt the core logic for use with vanilla JavaScript or other frameworks.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

Please ensure your code adheres to the existing style and that you add or update tests as necessary.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

