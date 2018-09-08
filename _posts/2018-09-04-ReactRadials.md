---
layout: post
title:  "Radial Dials with React"
date:   2018-09-04
---

# Building Radial Dials with React
2018-09

## What we're building

## SVG

## ViewBox

## Magic radius calculation

## stroke dash array

## Animating it

## Example references

## References and further reading

https://codepen.io/webslingerm/pen/RYVBGw

```jsx
const Radial = (props) => {
  const BAR_WIDTH = 5;

  const amt = props.completed || 0;
  const dashString = `${amt}, 100`;

  return (
    <svg className='Radial' 
      viewBox='0 0 36 36'>
      
      <g className='dials'>
        <circle strokeWidth={BAR_WIDTH} 
          r="15.915" 
          cx="50%" cy="50%" 
          className="background" />
        
        <circle strokeWidth={BAR_WIDTH} 
          r="15.915" 
          cx="50%" cy="50%" 
          className="completed" 
          strokeDasharray={dashString} />
      </g>
    </svg>
  );
};
```
