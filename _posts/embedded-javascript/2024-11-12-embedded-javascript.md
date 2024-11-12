---
title: Embedding JavaScript in a Jekyll post
date: 12-11-2024 00:15 CET
modified: 12-11-2024 2:09 CET
tags: [jekyll, javascript, webpage]
description: This post demonstrates how to embed JavaScript in a Jekyll post.
image: "/embedded-javascript/js-logo.png"
---

This post demonstrates how to embed JavaScript in a Jekyll post.

# Embedding JavaScript

In this first demo we will embed JavaScript in a post. To do this we create a small html/javascript snippet and save it in a file called `js-demo.html` in the `_includes` folder:
```html
{% include js-demo.html %}
```
Then we simply add the element with id `js-demo` and embed the JavaScript code:
```html
<div id="js-demo">
    <p> 🚀 Click me! 🚀 </p>
</div>

{% raw %}{% include js-demo.html %}{% endraw %}
```

Instead of using the `js-demo.html` file, we could also embed the JavaScript code directly in the post:
```html
<script type="text/javascript">
window.onload = ...
</script>
```

However, there are three advantages to using the `js-demo.html` file:
1. The code is not reusable. For example, here I simply used `{% raw %}{% include js-demo.html %}{% endraw %}` to embed the code functionally, and 
    ````plain
    ```html
    {% raw %}{% include js-demo.html %}{% endraw %}
    ``` 
    ````
    to display the code. 
2. Your code-linter may not function properly in a markdown code block.
3. Your project becomes more modular and easier to maintain.

## Live Demo
And voilà! Here is the live demo:

<div id="js-demo">
    <p> 🚀 Click me! 🚀 </p>
</div>

{% include js-demo.html %}

## Styling
Now, if we simply did this without any CSS styling it would look very wonky. To fix this, we can add some custom CSS to the post by creating a new SCSS file in the `_sass` folder and importing it in the `main.scss` file:
```scss
#js-demo {
    text-align: center; 
    width: 25%; 
    margin: 0 auto; 
    padding: 5px;
    border-radius: 50%; 
    border: 3px solid black;
    background-color: rgba(0, 0, 0, 0.1);
    
    @include media-query($on-mobile) {
        width: 50%;
    }
}

body[data-theme="dark"] #js-demo {
    border: 3px solid white;
    background-color: rgba(255, 255, 255, 0.1);
}
```
Here I have saved the file as `_sass/posts/_js-demo.scss` and imported it in the `main.scss` file:
```scss
@import "posts/js_demo";
```
I am doing it this way to take advantage of the Jekyll's built-in Sass compiler, and the predefined media queries defined in the project.