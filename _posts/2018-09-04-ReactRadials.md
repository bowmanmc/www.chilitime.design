---
layout: post
title:  "Radial Dials with React"
date:   2018-08-03
---

# Building Radial Dials with React

https://codepen.io/webslingerm/pen/RYVBGw

```jsx
const Radial = (props) => {

    const BAR_WIDTH = 5;

    const amt = props.completed || 0;
    const dashString = `${amt}, 100`;

    let text = null;
    if (props.showPercentage) {
        text = (<text x='50%' y='50%'>{amt}%</text>);
    }

    return (
        <svg className='Radial' viewBox='0 0 36 36'>
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
            { text }
        </svg>
    );
};
```
