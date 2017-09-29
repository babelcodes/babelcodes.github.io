---
layout: feature
language: typescript
name: 'this'
iid: this
status: DONE
abstract: "a variable that’s set when a function is called"
code_:
  gist: ddc99e4e8104ad655fdc083d0bc6734d
links:
 - link:
    name: 'TypeScriptLang.org | Functions'
    url: https://www.typescriptlang.org/docs/handbook/functions.html
    description: ''
    type: reference
features:
 - 'Function' 
---

* TOC
{:toc}


## JavaScript

See [this in JavaScript](../JavaScript/this)


## Functions

See [Functions](Function)



## Arrow functions
   
In JavaScript the ECMAScript 6 arrow syntax capture the `this` where the function is created rather than where it is invoked:

Even better, TypeScript will warn you when you make this mistake if you pass the `--noImplicitThis` flag to the compiler. 

It will point out that `this` in `this.suits[pickedSuit]` is of type any in the following:

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

let cardPicker = deck.createCardPicker();
let pickedCard = cardPicker();

alert("card: " + pickedCard.card + " of " + pickedCard.suit);
```

## this parameters
   
Unfortunately, the type of `this.suits[pickedSuit]` is still `any`. That’s because `this` comes from the function expression 
inside the object literal. To fix this, you can provide an explicit `this` parameter. `this` parameters are fake parameters 
that come first in the parameter list of a function:

```
function f(this: void) {
    // `this` is unusable in this standalone function
}
```

Let’s add a couple of interfaces to our example above, `Card` and `Deck`, to make the types clearer and easier to reuse:

```
interface Card {
    suit: string;
    card: number;
}
interface Deck {
    suits: string[];
    cards: number[];
    createCardPicker(this: Deck): () => Card;
}
let deck: Deck = {
    suits: ["hearts", "spades", "clubs", "diamonds"],
    cards: Array(52),
    // NOTE: The function now explicitly specifies that its callee must be of type Deck
    createCardPicker: function(this: Deck) {
        return () => {
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

Now TypeScript knows that `createCardPicker` expects to be called on a `Deck` object. That means that `this` is of type 
`Deck` now, not `any`, so `--noImplicitThis` will not cause any errors.


## this parameters in callbacks
   
You can also run into errors with `this` in callbacks, when you pass functions to a library that will later call them. 
Because the library that calls your callback will call it like a normal function, `this` will be `undefined`. With some work 
you can use `this` parameters to prevent errors with callbacks too. 

First, the library author needs to annotate the callback type with `this`:

```
interface UIElement {
    addClickListener(onclick: (this: void, e: Event) => void): void;
}
```

`this: void` means that `addClickListener` expects `onclick` to be a function that does not require a `this` type. 

Second, annotate your calling code with `this`:

```
class Handler {
    info: string;
    onClickBad(this: Handler, e: Event) {
        // oops, used this here. using this callback would crash at runtime
        this.info = e.message;
    }
}
let h = new Handler();
uiElement.addClickListener(h.onClickBad); // error!
```

With `this` annotated, you make it explicit that `onClickBad` must be called on an instance of `Handler`. Then TypeScript 
will detect that `addClickListener` requires a function that has `this: void`. 

To fix the error, change the type of `this`:

```
class Handler {
    info: string;
    onClickGood(this: void, e: Event) {
        // can't use this here because it's of type void!
        console.log('clicked!');
    }
}
let h = new Handler();
uiElement.addClickListener(h.onClickGood);
```

Because `onClickGood` specifies its `this` type as void, it is legal to pass to `addClickListener`. Of course, this also 
means that it can’t use `this.info`. If you want both then you’ll have to use an arrow function:

```
class Handler {
    info: string;
    onClickGood = (e: Event) => { this.info = e.message }
}
```

This works because arrow functions don’t capture `this`, so you can always pass them to something that expects `this: void`. 
The downside is that one arrow function is created per object of type `Handler`. Methods, on the other hand, are only created 
once and attached to `Handler`’s prototype. They are shared between all objects of type `Handler`.

