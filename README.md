###Change Navigation Active Class on Page Scroll with Bootstrap 3 Navigation & jQuery
**Demo**: http://trungk18.github.io/Change-Navigation-Active-Class-on-Page-Scroll/

In this template, I will show you how to create an navigation automatically updating targets based on scroll position. It is similar to [Bootstrap ScrollSpy](http://getbootstrap.com/javascript/#scrollspy)

Its purpose is to improve the user experience on your website and make it easier for the visitors to know where exactly they are browsing

The project structure is based on what I have already created for [Shrinking Navigation Bar When Scrolling Down - Bootstrap 3 Navigation & jQuery](https://github.com/trungk18/Resizing-Header-On-Scroll)

####HTML
We are also using .navbar-fixed-top of Bootstrap to make it stick to the top contains 3 links

```html
    <ul class="nav navbar-nav navbar-right">
        <li class="active">
            <a href="#portfolio">Portfolio</a>
        </li>
        <li>
            <a href="#about">About</a>
        </li>
        <li>
            <a href="#contact">Contact</a>
        </li>
    </ul>
```

Then, we have to create a section for each menu item

```html
    <div class="content">
        <section id="portfolio"></section>
        <section id="about"></section>
        <section id="contact"></section>
    </div>
```
We will leave all sections blank and will make them 100% browser height using CSS, but when applying this technique to your project, you have to add content into section.

```css
	.content {
        position: absolute;
        width: 100%;
        height: 100%;
    }

        .content > section {
            width: 100%;
            height: 100%;
        }

    #portfolio {
        background: #2dbccb;
    }

    #about {
        background-color: #eb7e7f;
    }

    #contact {
        background-color: #415c71;
    }
```

Finally, look at simple jQuery code. What it basically do is iterated through all section when scrolling, check the current position by scrollTop function and compare with <section> position.

If the condition is matched, just added class .active to li tag. 

You can change the scroll speed by editing "300" on animate function if you wish to change how fast the page is scrolling when a link from the navigation is clicked.

```javascript
    $(document).ready(function () {
        //Smooth scrolling when click to nav
        $('#top-nav > ul > li > a').click(function (e) {
            e.preventDefault();
            var curLink = $(this);
            var scrollPoint = $(curLink.attr('href')).position().top;
            $('body,html').animate({
                scrollTop: scrollPoint
            }, 300);
        })

        $(window).scroll(function () {
            onScrollHandle();
        });

        function onScrollHandle() {
            //Navbar shrink when scroll down
            $(".navbar-default").toggleClass("navbar-shrink", $(this).scrollTop() > 50);

            //Get current scroll position
            var currentScrollPos = $(document).scrollTop();

            //Iterate through all node
            $('#top-nav > ul > li > a').each(function () {
                var curLink = $(this);
                var refElem = $(curLink.attr('href'));
                //Compare the value of current position and the every section position in each scroll
                if (refElem.position().top <= currentScrollPos && refElem.position().top + refElem.height() > currentScrollPos) {
                    //Remove class active in all nav
                    $('#top-nav > ul > li').removeClass("active");
                    //Add class active
                    curLink.parent().addClass("active");
                }
                else {
                    curLink.parent().removeClass("active");
                }
            });
        }
    });
```

####Conclusion
Nowadays it is not really hard to search for component we need to use in our front-end project, but the most important thing is you can understand how it’s worked and you can easily implement this animated resizing header into your next project. 
Thanks for checking it out and view the demo, feel free to fork and fix the source code then pull back to me.