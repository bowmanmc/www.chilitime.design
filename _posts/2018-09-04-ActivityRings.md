---
layout: post
title:  "Activity Rings with SVG"
preview: 201809-ActivityRings/rings-complete.gif
date:   2018-09-04
---

# Activity Rings with SVG
2018-09


## What We're Building
![Animated Activity Rings](/images/201809-ActivityRings/rings-complete.gif "Animated Activity Rings")

Activity rings are a visualization made famous by the Apple Watch, 
which encourages you to 
"[close your rings](https://www.apple.com/watch/close-your-rings/)" 
every day by completing activities.

These rings are great for showing a percentage and looking good while doing it,
but are a bad idea if you want your users to compare the rings to each other.
The outer rings will be longer than the inner rings even when they are 
representing the same amount. When used judiciously though, these 
rings are great for showing data in an engaging, interesting, and 
aesthetically pleasing way.

If you'd like to jump straight into the finished code, check it out on
[codepen](https://codepen.io/webslingerm/pen/GXxxVx)

Also, I've put tons of reference material in the 
[References and Further Reading](#references-and-further-reading)
section below. If you're unfamiliar with SVG, CSS, or any of the technologies
used in this tutorial, check them out to get up to speed.


## Magic Radius Calculation
The circumference of a circle ``` C ``` equals two, multiplied by pi, multiplied
the radius of the circle. 

``` C = 2πr ```

Why does this matter to us? Well, since we're using our rings to 
display percentages, we want to set things up 
so that if we send it the number 50, it draws half a circle. Sending 
it 25 would draw a quarter of a circle, and 100 would draw a complete circle.

Working backwards, that gives us:

``` 100 = 2πr ``` so that ``` r = 100 / 2π ``` 

Which means that our magic number
for the radius of a circle with a circumference equal to 100 is:

``` r = 15.915 ```


## Setting the ViewBox
[ViewBox](https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/viewBox) is 
an SVG attribute that allows us to setup drawing coordinates for our image.
This is handy since our SVG may be rendered across thousands of pixels on a 
desktop monitor or a few hundred pixels on a mobile phone. By having a 
ViewBox, we can setup drawing instructions using coordinates separated from the
pixels they are eventually rendered as.

With a radius of 15.915, we'll come out with a diameter of about 32.
This means the svg itself renders 32 viewbox units wide and tall.
We're going to set our stroke-width (the thickness of the ring) to 3 viewbox units, 
so to prevent the circle from being clipped by the viewbox, we'll need to add 1.5 
units on all sides. That gives us a final viewBox attribute of:

``` viewBox="0 0 35 35" ``` 


## Drawing a Circle
Ok, let's put it all together and draw a circle.

### Markup
{% highlight html %}
<svg class="ActivityRings" viewBox='0 0 35 35'>
    <g class="ring ring1">
        <circle class="background"
            cx="50%" cy="50%"
            stroke-width="3" 
            r="15.915" /> 
    </g>
</svg>
{% endhighlight %}

### Styles (scss)
{% highlight scss %}
.ActivityRings {
    height: 100%;
    width: 100%;

    circle {
        fill: none;
    }
}

$color-red: #c53f3d;
.ring1 {
    .background {
        stroke: transparentize($color-red, 0.8);
    } 
}
{% endhighlight %}

The ``` cx="50%" cy="50%" ``` renders the ring in the middle of our ViewBox.
The other items we've already talked about. By adding class names, we can 
style them like we would HTML components, though SVG elements have a few new
attributes to work with such as fill and stroke.

Ok, you should now see something like
![Activity Rings Start](/images/201809-ActivityRings/rings-start.png "Activity Rings Start")


That's not bad, but not very interesting either. Let's add a ring representing
85% completion for this activity. First, we'll add another circle after our
background circle. SVG renders in source order, so the items first in the
markup are rendered behind the items later in the source.

### Markup
{% highlight html %}
<svg class="ActivityRings" viewBox='0 0 35 35'>
    <g class="ring ring1" style="transform: scale(1) rotate(-90deg);">
        <circle class="background"
            cx="50%" cy="50%"
            stroke-width="3" 
            r="15.915" /> 
        <circle class="completed"
            cx="50%" cy="50%"
            stroke-width="3" 
            r="15.915"
            stroke-dasharray="85, 100" />
    </g>
</svg>
{% endhighlight %}

### Styles (scss)
{% highlight scss %}
.ActivityRings {
    height: 100%;
    width: 100%;

    circle {
        fill: none;
    }
}
$color-red: #c53f3d;
.ring1 {
    .background {
        stroke: transparentize($color-red, 0.8);
    }
    .completed {
        stroke: $color-red;
    }   
}
{% endhighlight %}

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


## References and further reading

### SVG
* SVG - https://developer.mozilla.org/en-US/docs/Web/SVG
* SVG - https://css-tricks.com/using-svg/
* SVG - https://abookapart.com/products/practical-svg
* Sara Soueidan - https://www.sarasoueidan.com/tags/svg/
* Joni Trythall - http://svgpocketguide.com/
* ViewBox - https://www.sarasoueidan.com/blog/svg-coordinate-systems/
* ViewBox - https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/viewBox

