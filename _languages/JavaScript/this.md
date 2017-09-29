---
layout: feature
language: javascript
name: 'this'
iid: this
status: DOING
abstract: "a variable that’s set when a function is called"
code_:
  gist: ddc99e4e8104ad655fdc083d0bc6734d
links:
 - link:
    name: 'Understanding JavaScript Function Invocation and “this”'
    url: http://yehudakatz.com/2011/08/11/understanding-javascript-function-invocation-and-this/
    description: ''
    type: reference
features:
 - 'Function' 
---

* TOC
{:toc}


TODO

In JavaScript, `this` is a variable that’s set when a function is called. 
It comes at the cost of always having to know about the context that a function is executing in. 
This is notoriously confusing, especially when returning a function or passing a function as an argument.

Let’s look at an example:

```
let deck = {
    suits: ["hearts", "spades", "clubs", "diamonds"],
    cards: Array(52),
    createCardPicker: function() {
        return function() {
            let pickedCard = Math.floor(Math.random() * 52);
            let pickedSuit = Math.floor(pickedCard / 13);

            return {suit: this.suits[pickedSuit], card: pickedCard % 13};
        }
    }
}

let cardPicker = deck.createCardPicker();
let pickedCard = cardPicker();

alert("card: " + pickedCard.card + " of " + pickedCard.suit);
```

If we tried to run the example, we would get an error instead of the expected alert box. This is because the this being 
used in the function created by `createCardPicker` will be set to `window` instead of our `deck` object. That’s because
`this` is captured where it is invoked. A top-level non-method syntax call like this will use `window` for `this`.

We can fix this by making sure the function is bound to the correct `this` before we return the function to be used later. 
To do this, we change the function expression to use the ECMAScript 6 arrow syntax. Arrow functions capture the `this` where 
the function is created rather than where it is invoked:

```
let deck = {
    suits: ["hearts", "spades", "clubs", "diamonds"],
    cards: Array(52),
    createCardPicker: function() {
        // NOTE: the line below is now an arrow function, allowing us to capture 'this' right here
        return () => {
            let pickedCard = Math.floor(Math.random() * 52);
            let pickedSuit = Math.floor(pickedCard / 13);

            return {suit: this.suits[pickedSuit], card: pickedCard % 13};
        }
    }
}
```
