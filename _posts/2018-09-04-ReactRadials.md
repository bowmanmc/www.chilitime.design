---
layout: post
title:  "Radial Dials with React"
date:   2018-09-04
---

# Building Radial Dials with React
2018-09


## What we're building
![Animated React Radial Dial](/images/201809-ReactRadials/radial-complete.gif "Animated React Radial Dial")

We're going to be building a reusable react component for animated radial dials.
* Straight lines are easier to interpret (bar chart)
* These are used for aesthetic reasons
* Apple watch


## SVG
* https://css-tricks.com/using-svg/
* https://abookapart.com/products/practical-svg
* Sara Soueidan - https://www.sarasoueidan.com/tags/svg/
* Joni Trythall - http://svgpocketguide.com/
* Mozilla 


## ViewBox
* https://www.sarasoueidan.com/blog/svg-coordinate-systems/


## Magic radius calculation
The circumference of a circle ``` C ``` equals two, multiplied by pi, multipled 
the radius of the circle. 

``` C = 2πr ```

Since we're using our radial to display percentages, we want to set things up 
so that if we send it 50, it draws half a circle. Sending it 25 would draw
a quarter of a circle, and 100 would draw a comnplete circle.
There are several ways to make this happen, but the most straight-forward way 
is to set the circumference of the circle equal to 100. 

Working backwards, that gives us:

``` 100 = 2πr ``` so that ``` r = 100 / 2π ``` 

Which means that our magic number
for the radius of a circle with a circumference equal to 100 is:

``` r = 15.915 ```


## Setting the Viewbox
With a radius of 15.915, we'll come out with a diameter of about 32.
This means the svg itself renders 32 viewbox units wide and tall.
We have our stroke-width set to 5 viewbox units, so to prevent the circle
from being clipped by the viewbox, we'll need to add 2.5 units on all sides.
That gives us a viewBox attribute:
``` viewbox="0 0 37 37" ``` 


## Stroke Dash Array
* https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/stroke-dasharray
* https://css-tricks.com/almanac/properties/s/stroke-dasharray/

The ```stroke-dasharray``` style attribute will allow us to control how much of
the circle to draw. This property allows developers to have a large amount
of control over how dashed lines are rendered in SVG.
We'll be using it to draw the "filled" part of our circle.

``` stroke-dasharray="50 100" ```

The first number tells the browser how much to draw. In our case, since the
circumference of the entire circle is 100, we can set this equal to the 
percentage and it will draw a line for the right amount! The second number is
how long to make the gap in-between the dashes. We can just set this to 100 so 
that no matter what percentage we're displaying, we'll just get one line.


## Animating it


## Static Code
### Markup

### Styling


## Making a React Component
### JavaScript


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
