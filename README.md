## 402.- 50 Projects 50 Days - Progress Steps

### What was the project about?

The project is part of the 50 Projects in 50 Days with Brad Travesy via Udemy. The course is a code-a-long to further cement skills used within HTML, CSS, and Vanilla JavaScript.

This particular project was making progress steps, such as that used to purchase an item, place it into the shopping basket, go to checkout, and add payment.

[Progress Steps](https://totallysly.github.io/402.-50PROJECTS-50DAYS--progress-steps/)

### What did I learn?

#### CSS

This project was more complex than the first one, in regards to CSS and JavaScript.

This project used pseudo-elements, particularly the '_::before_' pseudo-element. I had seen and used pseudo-elements before, mainly within code-a-long tutorials. During this project I paused to really try and learn about pseudo-elements.

[Kevin Powell - Pseudo-elements PART ONE](https://www.youtube.com/watch?v=zGiirUiWslI&ab_channel=KevinPowell)

[Kevin Powell - Pseudo-elements PART TWO](https://www.youtube.com/watch?v=xoRbkm8XgfQ&ab_channel=KevinPowell)

[Kevin Powell - Pseudo-elements PART THREE](https://www.youtube.com/watch?v=djbtPnNmc0I&ab_channel=KevinPowell)

My take away knowledge of the pseudo element is much better. This project used only _::before_, but the some methods apply to _::after_ as well.

The most important aspect of a pseudo element is using _content: ' ';_ within the CSS. Often, the space remains blank, but you input other content.

    p::before {
    	    content: ' ';
    	    background: red;
    	    display: block;
    		width: 10px;
    		height: 10px
    }

_This is taken from the first Kevin Powell video._

A tiny 10px by 10px red square is placed just **before** the **content** of that element. In this example, the `<p>`. And the opposite if **after** is used instead. In the image below, specifically looking at the dev inspector window, you can see that the _::before_ is within the `<p>` element, and before. It is important to remember that they are inline by default. The `content: '';` can contain images, emojis, or text etc.

[![kevinpowell-psuedoelement-tutorial.png](https://i.postimg.cc/Sxv42PRx/kevinpowell-psuedoelement-tutorial.png)](https://postimg.cc/jDPmBZyp)

In the Kevin Powell example, he uses it to enhance the design of his title. It adds a red stripe before and after the main text.

Within the context of this project, the _::before_ was used to create the grey progress bar that runs across all the progress steps. It is then filled with the blue colour, as the user clicks next and progresses to the next step.

    .progress-container::before {
    content: ' ';
    bbackground-color: var(--line-border-empty);
    position: absolute;
    top: 50%;
    left: 0;
    transform: translateY(-50%);
    height: 4px;
    width: 100%;
    z-index: -1;
    }

#### JavaScript

The JavaScript within this project had some interesting logic, which turned out to be rather simple.

    const next = document.getElementById('next')
    const circles = document.querySelectorAll('.circle');

    let currentActive = 1;

    next.addEventListener('click', () => {
        currentActive++

    	if currentActive > circles.length {
    		currentActive = circles.length
    	}
    }

As `const circles` becomes a node list, which is effectively an array, then this can by used dynamically within the _if_ statement, regardless of how many steps there are to progress through.

Also, bysetting _currentActive_ to 1, and incrementing this upon each _click_ of _next_ will progress the bar to each step. I liked the simplicity of making the counter stop, but changing currentActive to the length of the circles node list. Making the code dynamic, and a clever way of ending the click sequence.

This logic is applied for the _prev_ button. But instead of increamenting, the _click_ decrements the _currentActive._ However, the _if_ statement changes slightly.

    if(currentActive < 1 {
        currentActive = 1;
    }

Therefore, whenever the _currentActive_ goes below one, it is just reset back to 1.

    function update () {
        circles.forEach((circle, index) => {
    	    if (index < currentActive {
    		   circle.classList.add('active')
    	    } else {
    		    circle.classList.remove('active')
    	    }
        }
        function update()
    })

    const actives = document.querySelectorAll('.active')
    progress.style.width = ((actives.length - 1) / (circles.length - 1)) * 100 + '%'

    if (currentActive === 1) {
        prev.disabled = true
    } else if (currentActive === circles.length) {
        next.disabled = true
    } else {
        prev.disabled = false
        next.disabled = false
    }

As previously, stated, _circles_ is a node list and as such we can access its _index_ (with the _index_ always starting at **0**. So _for each_ circle, if it is **less** **than** the _index_, then **add** the _class list._

Therefore, if the _index_ at **0** is **less than** the _currentActive_ (which is set to **1**) then _add_ the _classList_ of active. If not, remove the _classList_.

    const actives = document.querySelectorAll('.active')
    progress.style.width = ((actives.length - 1) / (circles.length - 1)) * 100 + '%';

The tutorial demonstated the logic behind the equation with the following steps.

1.  `console.log(actives.length, circles.length)`
    which prints out (2, 4), (3, 4), (4, 4).

2.  `console.log(actives.length / circles.length)`
    prints (0.5), (0.75), (1)
    The goal is to get the above numbers as a % for the CSS _width_ property.

3.  `console.log((actives.length / circles.length) * 100)`
    prints (50), (75), (100)

4.  `progress.style.width = (actives.length / circles.length) * 100 + '%'`
    _progress_ is the class we created in the CSS where we require the _width_ property. At the moment it is set to **0**. However, we require it to move along as a % toward each stage. `+ '%'` is string concatenation. However, this will go to **50%**, when, with the 4 different stages we require roughly 33%.

5.  `progress.style.width = (actives.length - 1) / (circles.length - 1) * 100 + '%'`
    By **minus 1** from each will create, roughly **33%**, _width_ movement of the **blue progress colour**. Thus, meaning that it was get to each circle correctly, and not beyond.

--

The latter part of the update function relates to the buttons that cause the progress upon click.

    if (currentActive === 1) {
        prev.disabled = true
    } else if (currentActive === circles.length) {
        next.disabled = true
    } else {
        prev.disabled = false
        next.disabled = false
    }

**If** the _currentActive_ is **strictly equal** to **1**, then the _prev_ button should be **disabled**. **Else**, **if** the _currentActive_ is **strictly equal** to the **circles.length**, then the _next_ button should be **disabled**. **Else**, neither of the statements are **true**, then neither the _prev_ or _next_ button should be set to **disabled**.

> Written with [StackEdit](https://stackedit.io/).
