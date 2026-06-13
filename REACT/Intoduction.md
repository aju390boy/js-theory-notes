# REACT

## Vite + React Setup

```js
npm create vite@latest my-sample-vedikett -- --template react
cd my-sample-vedikett
npm install 
npm run dev

```
## Folder Structure

```js
mini-store-react/
  src/
    components/
    pages/
    data/
    assets/

// components/ = for reusable UI parts (like buttons, cards, navbar)
// pages/ = for main pages like Home, About, Cart
// data/ = for data (like your product list)
// assets/ = for images/fonts
```

## Components

* App.jsx = the main root component

* Home.jsx = the Home page

* ProductCard.jsx = a card to show one product

In React, a component is just a JavaScript function that returns HTML. Like this:
```js
function ProductCard({ name, price }) {
  return <div>{name} - ₹{price}</div>
}
```

## Props

 Props = data you pass into a component.

```js
<ProductCard name="Axor Helmet" price={3500} />
```

##  .map() – Render Lists

You used .map() to turn your product list into cards:

```js
products.map((product) => (
  <ProductCard key={product.id} name={product.name} price={product.price} category={product.category} />
))
```
"For each product in the list, create a ProductCard."



## useState

useState is a special function in React that lets you store data that can change over time, and when that data changes, React automatically updates the UI for you.

* useState is ONLY for Function Components
* useState is a hook, and hooks only work in function components.
* Class components use this.state and this.setState() instead.
* Normal variable: If you change it, the UI doesn't update.
* useState variable: If you change it, React automatically re-renders the component with the new value.
* useState = how to store changing data in React
* Two values: current value + function to update it
* When state changes → React automatically updates the UI


# 🚀 Now Let's Add Search + Filter to Your App

* check mini-store-react-2 folder!

 ### What Just Happened? (Explanation)

**1**  We Imported useState
```js 
import { useState } from 'react';

// This gives us access to the hook
```
**2** We Created Two State Variables

```js
const [searchQuery, setSearchQuery] = useState('')
const [selectedCategory, setSelectedCategory] = useState('ALL')

// searchQuery = stores what the user typed in the search box
// selectedCategory = stores which category is selected
// Both start with empty/default values.


```

**3**  We Updated State When User Types/Selects

```js
<input
  value={searchQuery}
  onChange={(e) => setSearchQuery(e.target.value)}
/>

// value={searchQuery} = show current state in the input
// onChange = when user types, call setSearchQuery with new value
// React automatically re-renders when state changes!

<select
  value={selectedCategory}
  onChange={(e) => setSelectedCategory(e.target.value)}
/>

// Same thing for the dropdown
```

**4** We Filter Products Based on State

```js
const filteredProducts = products.filter((product) => {
  const matchesSearch = product.name.toLowerCase().includes(searchQuery.toLowerCase())
  const matchesCategory = selectedCategory === 'ALL' || product.category === selectedCategory
  return matchesSearch && matchesCategory
})

// filter() loops through products
// Returns only products that match BOTH search AND category
// When searchQuery or selectedCategory changes, this runs again automatically
```
**5** We Show Filtered Products

```js
{filteredProducts.map((product) => (
  <ProductCard key={product.id} name={product.name} price={product.price} category={product.category} />
))}

// When state changes → filtered list changes → UI updates automatically!
```
## 🎯 Key Points About useState

```js
| Concept                 | What It Means                                           |
| ----------------------- | ------------------------------------------------------- |
| useState(initialValue)  | Creates a state variable with a starting value          |
| [value, setValue]       | Returns 2 things: current value + function to update it |
| setValue(newValue)      | When you call this, React re-renders the component      |
| State is local          | Each component has its own state, doesn't affect others |
| State updates are async | React batches updates for performance                   |
```


🚀 My Recommendation for You
Learn this order:

✅ useState (state in function components)

✅ useEffect (lifecycle/data fetching)

✅ React Router (navigation)

✅ Optional: learn class components later if you see them in old code