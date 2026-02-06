# React/JSX Style Guide

_A mostly reasonable approach to React and JSX_

## Table of Contents

1. [Basic Rules](#basic-rules)
2. [Declaration](#declaration)
3. [Ordering](#ordering)

## Basic Rules

- Only include one React component per file. *Mostly*.
- Always use TSX syntax.

## Declaration

- Do not use `displayName` for naming components. Instead, name the component by reference.

  ```jsx
  // bad
  export default React.createClass({
    displayName: 'ReservationCard',
    // stuff goes here
  });

  // good
  export default class ReservationCard extends React.Component {
  }
  ```
## Ordering

- Ordering for component files:

1. prop types
2. component function
3. attach related composite components

- Ordering for component functions:

1. hook calls
2. variables derived from state and/or props (no JSX!)
3. callback definitions
4. useEffects
5. render
   1. try and keep all JSX definitions in a single returned value. This includes returning `null` . Don't store JSX in variables higher up, just define them in the final render.

```tsx
// Bad
function MyComponent(props) {
  
  const query = useReactQuery(props.params)
  
  const companies = query.data.companies.filter(haveOwners)

  const listItems = companies.map(comp => <li>{comp.name}</li>)
  
  function handleFollow(e, companyName) {
    trackEvent(e, companyName)
  }

  const [isOpen, setIsOpen] = useSate(false)
 
  return <ul>{listItems}<ul>
}
```

```tsx
// Good
function MyComponent(props) {
  const [isOpen, setIsOpen] = useSate(false)
  const query = useReactQuery(props.params)
  
  var companies = query.data.companies.filter(haveOwners)
  
  function handleFollow(e, companyName) {
    trackEvent(e, companyName)
  }
 
  return <ul>{companies.map(comp => <li>{comp.name}</li>)}<ul>
}
```