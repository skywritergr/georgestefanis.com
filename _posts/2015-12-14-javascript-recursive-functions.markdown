---
layout: post
title:  "The Case of recursive functions in Javascript"
date:   2015-12-14
categories: blog
---
Recursive functions are awesome! It’s one of those concepts that make software development magical. The ability to use a function, inside itself even before you complete the implementation, is mind blowing. Also recursive functions are one of the strong points of functional programming, and let's not forget that Javascript is a functional language.

That been said, outside of algorithmic exercises I haven't found much practical use for recursive functions in real world scenarios. Until last week. At work we had a case of a back-end process that was returning a JSON object that might had child objects. The child objects might had other children themselves.

Here is an example of how an object might look:
{% gist 6bada8e67f82cb836a5c %}

##Recursive functions to the rescue 

The first thing to notice is that the children have the same structure as the parents. That makes our lives easier as we can extract a function that will do all the object processing/manipulation. For traversing the objects we use recursive logic. In this example we want to toggle the watched flag. So if it’s true we want it changed to false and vice versa. Here's the function:

{% gist a1d59e20532694270b69 %}

Here's some things to note. First the declaration. We are not assigning an anonymous function to the recursivelyToggle variable, we are giving our function a name. The question that you might have now is, what name are we supposed to use? The variable declaration recursivelyToggle  is to initially call the function and the named function recursivelyToggleChildren is for internal use. That name is in scope of the function itself. As you can see we use it later in the function to call itself.

The other interesting thing is that we create a local version of the passed array in the function. We are doing this because we don’t want to alter the state of the original object. We want instead our function to return a new version of the object, with the altered variables. This way we just created a [pure function](http://www.nicoespeon.com/en/2015/01/pure-functions-javascript/). Finally the last noteworthy thing to notice is the if statement. In this statement we are checking if the children array is there or not. If it’s not there it will be undefined, which in Javascript terms is falsy. If the array is there it’s truthy and therefore we want to traverse the child object and change it.

As you can see this is a perfect way to traverse an object that doesn't have a specific structure. Also the code is DRY and in general principles, simple to read. On the negative side, debugging that function can be confusing, especially for someone that’s not familiar about recursive functions. I wouldn't use recursive functions in my code unless the benefit is super obvious, like here. As with any powerful tool, use it with care.
