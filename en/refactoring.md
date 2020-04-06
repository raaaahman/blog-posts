# Refactoring: Fix your bugs before they occur

## A new story

> Once upon a time, there was a feature request for an application. But the application had a legacy code base...

![Once upon a time, in a galaxy far far away...]

This opening sounds familiar, doesn't it? In the life cycle of an application, it is more than expected to add features on an existing code base. Most of the time, the programmer of such code base would just have not planned for such a feature to be requested.

For this reason, every new feature should be an opportunity to question the actual design of this code base. There's two benefits from a better design that could satisfy both the _Product Owner_/Client and the developers team to be gained here:

- A suited design may allow for the feature to be built **faster**
- A good design may generate **less bugs** in the long run

## When your code smells

Speaking of bugs, they usually come when a user uses the application for an use case that the developer didn't plan. This means that a developer can't really prevent them before the user find them, except...

... we actually can (for specific cases)! Experienced programmers have noticed anti-patterns that have been repeated through numerous software; anti-patterns that usually lead to bugs in a more a less expected manner. A great deal of these anti-patterns have been compiled by Martin Fowler[^1] and Kent Beck[^2] in a book named _Refactoring: Improving the Design of Existing Code[^3]_, under the term of **Code Smells**.

The following example comes from the _Bug Zero Kata_[^4] by Johan Martinsson[^5]. This code kata[^6] aims to prevent bugs happening with the implementation of new features by refactoring an application close to a _Trivial Pursuit_[^7] game.

```php
function add($playerName) {
   array_push($this->players, $playerName);
   $this->places[$this->howManyPlayers()] = 0;
   $this->purses[$this->howManyPlayers()] = 0;
   $this->inPenaltyBox[$this->howManyPlayers()] = false;

    echoln($playerName . " was added");
    echoln("They are player number " . count($this->players));
	return true;
}
```

The above lines (in PHP) show an example of _Data Clump_. This is a typical code smell: you can see that, whenever a new player enters the game, four values are added in four different arrays:

- `players` : the new player's name, passed as parameter.
- `places` : the new player's position on the board, `0` by default.
- `purses` : the new player's amount of collected coins (when she answers correctly to a question), also `0` by default. 
- `inPenaltyBox` : whether a new player is in the penalty box (when he answers incorrectly to a question), `false` by default.

While all these values are related to a same player, they are distributed across four different arrays! We can easily see how it can cause a bug by a carefree future development: imagine one player is removed from the `players` list by a new function like this one: 

```php
function remove($playerNumber) {
    $playerName = $this->players[$playerNumber];
    array_splice($this->players, $playerNumber, 1);

    echoln( $playerName . " leaved");
    for( $i = 0; $i < $this->howManyPlayers(); $i++ ) {
        echoln($this->players[$i] . " is now number " . $i );
    }
}
```


You can see the developer forgot to also remove the corresponding values in the `places`, `purses` and `inPenaltyBox` arrays... What happen here if we remove the second player in a four players game? Well the third player will now have the previous second player's position, coins and penalty state, and the fourth will have the previous third player's values for these! Obviously, some players will be happier than others...

## Applying the recipes

Thankfully, there are not only the smells that are well known, but also the methods to counter them: the _refactoring_ recipes! While the word has been used to define any modification of code that doesn't add feature to a code base, it used in the aforementioned book in a very specific sense:

> 

This book contains a wide catalog of such refactorings, that are like "recipes" to be applied step by step. And each of them can be composed of several smaller refactorings.

This doesn't mean that these recipes are the end-all be-all to solve the sniffed code smells, and each proposed solution is to be adapted to your application and feature context. In fact, the book proposes several ways to apply each refactoring, and emphasize on the fact that it is not an exhaustive list.

The important consideration here, is to apply these refactorings in several small steps, and test between each step that you didn't break your application. That's why it goes very well along with **automated tests** that will speed your process when applying them.

## Profit!

Now that you have a way cleaner code base, implementing the mentioned feature should be easier. And even if it may have you write more code in the end, you will certainly be more aware of what each part of this code is about. So don't let this awareness fade out! There is a still some easy and very valuable refactorings to be performed: _Rename function_ and _Rename variable_.

These very simple constructs of every programming language are not to be treated likely! Because we, programmers, **spend more time reading code than writting it**, being able to understand what a function/method does and what data a variable holds is very valuable in our everyday jobs. So be nice to your colleagues, and to yourself from the future, and find explicit names for each of those. If you've written a comment above such a function or variable, you might find the words you're looking for in this comment (and probably will not need it anymore afterwards)...

![Marty McFly]

With all that time spent in rewriting existing code, you might have overreached the time estimated to implement the feature. Don't worry though, because you have still made valuable progress:

- You have solved some bugs before anyone (QA or end customer) stumble on them
- With a more understandable code base, the eventual other bugs will still be easier to track and fix
- Refactoring is as much a skill as implementing feature, and each time you do it, you get better -and faster!- at it
- The cleaner code base may make implementing the next features faster as well

If you are unsure about trying it in your production environment, that is understandable, and I advise you to train yourself with some **coding dojos**. But that will be the topic for another post...

Until then, keep coding!