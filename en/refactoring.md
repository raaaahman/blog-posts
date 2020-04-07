# Refactoring: Fix your bugs before they occur

## A new story

> Once upon a time, there was a feature request for an application. But the application had a legacy code base...

![Once upon a time, in a galaxy far far away...]

This opening sounds familiar, doesn't it? In the life cycle of an application, it is more than expected to add features on an existing code base. Most of the time, the programmer of such code base would just have not planned for such a feature to be requested.

For this reason, every new feature should be an opportunity to question the actual design of this code base. There's two benefits from a better design that could satisfy both the _Product Owner_/Client and the developers team to be gained here:

- A suited design may allow for the feature to be built **faster**
- A good design may generate **less bugs** in the long run

## Legacy code strikes back

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

## Return of the clean code

Thankfully, there are not only the smells that are well known, but also the methods to counter them: the **refactorings**! While the word has been used to define any modification of code that doesn't add feature to a code base, it used in the aforementioned book in a very specific sense:

> _Refactoring_ (noun): a change made to the internal structure of software to make it easier to understand and cheaper to modify without changing its observable behavior.

This book contains a wide catalog of such refactorings, that are like "recipes" to be applied step by step. And each of them can be composed of several smaller refactorings.

Let's take the data clump sniffed earlier as an example. The book precognizes a refactoring named _Extract Class_: we'd rather have all the related data bound together in instances that can represent each individual player. So if a player leaves, he takes all his coins with him.

![Cliffhanger rope bounded alpinists]

But replacing every references to `places`, `purses` and `inPenaltyBox` right off the bat would be quite risky. So we will take a securing step first, in the form of the _Encapsulate field_ refactoring: 

```php
public function getPursesForCurrentPlayer() {
    return $this->purses[$this->currentPlayer];
}

public function addPurseForCurrentPlayer()
{
    $this->purses[$this->currentPlayer]++;
}

public function isCurrentPlayerInPenaltyBox() {
    return $this->inPenaltyBox[$this->currentPlayer];
}

public function setCurrentPlayerInPenaltyBox() {
    $this->inPenaltyBox[$this->currentPlayer] = true;
}

public function getPlaceForCurrentPlayer() {
    return $this->places[$this->currentPlayer];
}

public function movePlayerBy($roll) {
    $this->places[$this->currentPlayer] = $this->places[$this->currentPlayer] + $roll;
    if ($this->places[$this->currentPlayer] > 11) $this->places[$this->currentPlayer] = $this->places[$this->currentPlayer] - 12;
}
```

Each one of these functions are simple **getters and setters**: they wrap the access to the current player's data (position on the board, coins in purse, if she is in penalty box...), but the arrays still exists individually! What I can do now is replacing each call to these arrays to a call to the adequate function instead, one by one, testing between each replacement that I didn't break anything. With a smart IDE or a little search & replace, I can also speed up the process by a lot.

![Indiana Jones golden statue]

Now that I have my access to player data secured, I can create the awaited `Player` class:

```php
class Player
{
    private $name;
    private $place = 0;
    private $coins = 0;
    private $inPenaltyBox = false;

    public function __construct($playerName) {
        $this->name = $playerName;
    }

    public function getName() {
        return $this->name;
    }

    public function getPlace() {
        return $this->place;
    }

    public function moveBy($number) {
        $this->place = $this->place + $number;
        if ($this->place > 11) $this->place = $this->place - 12;
    }

    public function getCoins() {
        return $this->coins;
    }

    public function addCoin() {
        $this->coins++;
    }

    public function isInPenaltyBox() {
        return $this->inPenaltyBox;
    }

    public function setInPenaltyBox() {
        $this->inPenaltyBox = true;
    }
}
```

Because the values for a new player's place, coins and penalty status are always the same, I can simply set them with default values in the class, only the player's name need to be passed in the class constructor. The rest of the class methods are simple getters and setters to access these values. Yes, this is a lot of getters and setters in the project, but we will replace the former with the newer in a few minutes. But before that, I need to change how the player data is stored.

```php
 function add($playerName) {
 	$player = new Player($playerName);
    array_push($this->players,$player);

    echoln($player->getName() . " was added");
    echoln("They are player number " . count($this->players));
	return true;
}
```

This function is already becoming simpler. Now the `$players` array stores `Player` instances instead of strings for players' names. This means that I have to change the immediate following code to display the name of the new player by calling the `Player::getName()` method instead of directly accessing to the array values.

But wait a minute, since `$players` now stores objects instead of strings, wouldn't it just break my whole application? The answer is yes, but as sharp as you are, you surely know where I'm going next: all the data access have been encapsulated in getters and setters! This means I just have to change the code inside these getters and setters, and voilà, I have now completely changed how the player data are stored and accessed in my whole application.

```php
public function getNameForCurrentPlayer() {
    return $this->players[$this->currentPlayer]->getName();
}

public function getPursesForCurrentPlayer() {
    return $this->players[$this->currentPlayer]->getCoins();
}

public function addPurseForCurrentPlayer()
{
    $this->players[$this->currentPlayer]->addCoin();
}

public function isCurrentPlayerInPenaltyBox() {
    return $this->players[$this->currentPlayer]->isInPenaltyBox();
}

public function setCurrentPlayerInPenaltyBox() {
    $this->players[$this->currentPlayer]->setInPenaltyBox();
}

public function getPlaceForCurrentPlayer() {
    return $this->players[$this->currentPlayer]->getPlace();
}

public function movePlayerBy($roll)
{
    $this->players[$this->currentPlayer]->moveBy($roll);
}
```

I could have stopped here, but these getters and setters only delegates to `Player` class getters and setters... and that's a bit too much **indirection** for my liking. So I did a little clean up by:

- Extracting the access to the current player instance in a `getCurrentPlayer()` function that should be more explicit.
- Inlining all the getters and setters at the game level, which mean I replaced each of these calls by the code that is inside the function

These last steps are really a matter of style and preference, so I won't drag on too long on them[^8]. The important consideration here, is that I've applied each of these steps to have my application back to a stable state as quickly as possible, by making the smaller steps I could imagine. That's why this practice goes very well along **automated tests**[^9], which make inquiring the stability of your code a very trivial task.

[^8]: If you want a follow through my whole kata, you can explore the pull request I made about it on GitHub.

Knowing the specific refactorings helps a lot in defining the steps to take (but I won't lie, I had the book on the table during the whole exercise). And the smaller of them are built to be done by most of the recent IDEs on a simple shortcut, which speeds up the process by a whole lot while making it error prone!

Although, this doesn't mean that these recipes are the end-all be-all to solve the sniffed code smells, and each proposed solution is to be adapted to your application and feature context. In fact, the book proposes several ways to apply each refactoring, and emphasize on the fact that it is not an exhaustive list.

## A hack for the future

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