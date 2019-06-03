# Test Driven Development, a practical start

**Automated testing**, sometimes clumsily referred as *unit testing* (because *unit tests* are a part of the broader concept of*automated test*), is a practice in development in which I'm really interested. Its point is to have code that inspect your code to see if the former behave like you expect. While it obviously makes you write more code, its goal is to pay back the time you've invested into writing your *test code* by helping you discovering the bugs you may introduce during your development iterations.

More specifically, what I will demonstrate in this post is how to start using practicing a quite rigorous approach of this practice which is called **Test Driven Development**. This specific way of thought advocates to write your tests before you start writing your *production code*. This might seems a little weird when you hear about it the first time, because you will basically be testing something that doesn't exist yet. So I will use a practical case where I implemented it to let you understand how it works and how it benefited me.
 
## About the context

Before jumping into the geeky details, let me explain to you in which context I decided to use this practice: an activity that I appear to be liking a lot, is to compete in *artificial intelligence* challenges brought by the site [CodinGame](https://www.codingame.com/contests/finished). These challenges last about 10 days and ask you to write an *artificial intelligence* for a game that the *CodinGame* team or community has developed for such occasion. The *AI* of each player is then drawn to play matches against others developers' *AI*s in order to rank every one of them through different leagues.  Don't freak out on the buzz words, their challenges are open to every level of programmers (notably thanks to their league system), and I know very little in the *AI* department myself.

The game that my *AI* had to play in this challenge was something like chess, but with some resources management and territory control mixed in. To sum it up, player can use gold to spawn units, that will capture tiles of the board they are walking on, thus increasing the players' gold income. There's a little more in it, but I will deconstruct it in the following paragraphs.

![Code Of Ice and Fire, a game AI challenge](../assets/tdd-000_codingame.png)

Between the short duration of the 'project', and the fact that I was not going to allocate the most of my time to it, I wasn't really thinking into using *Test Driven Development* in the first place. But then I watched a talk by Grégory Ribéron[^1] which made me change my mind. In this talk, he explains the four distinct parts of writing *AIs*.

He clearly made a distinction between **modeling the context**, and the actual *AI* computing process. His point was that you want to avoid having an *AI* that is taking wrong decisions because of how you coded your context model. If you're not aware about having done a mistake in modeling the context, you can try to optimize your *AI* with all your heart and soul, but it will still take sub-optimal decisions. That was the selling point for me.

## About the technology in use

As *CodinGame* let us choose between a wide variety of languages in their online *IDE*, I've decided to use *Javascript*, because I know it sufficiently to write code fluently with it. Moreover, I've chosen to use the **test automation framework** *Jest*. 

What's a *test automation framework*, and why did I use it? Basically, I could have written my tests in plain old *Javascript*. But such thing is quite cumbersome to do, and the basics of *automated tests* are so common that developers have made tools to fasten the whole process.

Actually, *Jest* is pretty easy to install, because it is simply a [Node.Js](https://nodejs.org/) module. And  [Jest's official documentation](https://jestjs.io/docs/en/getting-started.html) is pretty clear as well. If you're not familiar with it, don't be afraid, just follow the steps written in their *Getting Started* guide. I'll show you how to use it immediately.

## My first test case

Because of *TDD* works, it will force me to go through inspecting closely the rules before writing code. Indeed, I will have to write a test to ensure that my program conform to those rules. So, I will start to inquire how unit movement works. Here's what the rules said:

> The map is a grid of size 12x12, where the top-left corner is the cell (0,0). The map is randomly generated at the start of each game. 

Okay, everything is very well understandable for a human, but a computer needs much more specific instructions. So my first decision is to write a test that will verify that a unit won't effectively try to move outside of the map.

Here's how Robert C. Martin ( alias *Uncle Bob* ), a famous *TDD* evangelist, worded the first step in a *TDD* process, that he calls *Three laws of Test Driven Development*[^2] :

>  1. You must write a failing test before you write any production code.
   2. You must not write more of a test than is sufficient to fail, or fail to compile.

I'm keeping rule number 3 aside for now, but if I apply this two first rules by the book, my first test (and even first lines of code written, because I have to write test before production code), looks like that :

	const Unit = require('./Unit')
	
	test( 'A unit cannot move outside of the map', ()=> {
	  let unit = new Unit()
	  expect(unit.canMove()).toBe(false)
	})

Actually, that code does not really makes sense by itself, it just seem that our unit will not ever be able to move. But anyway, it should be enough to have a failing test, and when I run my tests with the command `npm run test`, here's what Jest answer me back :

	 FAIL  ./Unit.test.js
	 ✕ A unit cannot move on another unit (2ms)
	 ● A unit cannot move on another unit
	 TypeError: unit.canMove is not a function

Which is logical, because I did not implement the `canMove()` function in my class `Unit`! Wait, I have a class `Unit` ? Yep, because I did not start *TDD* when I started this project, so I have a bit of already existing code. In a 100% *TDD* scenario, my test would have failed right at the first line, so, by the *Second Law of TDD*, I should have written only the first line.

Okay, let's look at rule number 3 now, it says :

> 3. You must not write more production code than is sufficient to make the currently failing test pass. 

I guess the minimal code to write would be pretty simple, here's what I think of:

	class Unit {
	    canMove() {
	      return false;
	    }
	}

And the test pass, obviously. Well, is that all ? I have a function that validates a test, but its result is always `false`, not pretty helpful at this stage. Well, this test only verifies **one case** (which is not very well defined now, I must admit). I will develop other cases in the following paragraphs, and they will be handled by other tests. This will help me identify more clearly what's wrong with my production code.


## More tests!

As I don't have any failing test anymore, the *Third Law of Test Driven Development* forbids me to write anymore production code, so I will write the test for another case, the case when our  unit can actually move. Let's look into the `Tile` class I have made prior to switching to *TDD* :

	class Tile {
	    constructor(x, y, type, data = null) {
	        this.x = x
	        this.y = y
	        this.type = type
	        this.data = data
	    }
	    
	    // ...
	    
	}


The `type` parameter here refers to a character that corresponds to the entries my program reads from *Codingame*'s API, which I'll copy right here :

> A map cell can be either:
- void (#): not a playable cell.
- neutral (.): doesn't belong to any player.
- captured (O or X): belongs to a player.
- inactive (o or x): belongs to a player but inactive.

By definition, a neutral tile cannot contain any unit, otherwise it would be a tile controlled by a player. So I guess I could test that my units can always move on a neutral tile. This should be a fairly easy test :

	const Tile = require('./Tile')
	
	test( 'A unit can move on a neutral tile', () => {
	    let unit = new Unit(1)
	    let tile = new Tile(0, 0, '.')
	    expect(unit.canMove(tile)).toBe(true)
	})

See ? Pretty easy : I instantiate a new `Tile`, for which I give coordinates and a `type` parameter. Then I run my tests, and as expected, the new test fails (because my `canMove` method always returns `false`). So, time to change my production code, since I have a failing test to solve. I'll make it quick and dirty :

	canMove( tile ) {
      if ( tile.type === '.' ) {
        return true
      }
      return false
    }

Okay, time to run my tests again. My new test passes, but my first tests fails!

	    TypeError: Cannot read property 'type' of undefined

Of course it does, since I have not have instantiated a tile in this test, and now my production code needs to be given a parameter representing the tile. So I'll modify it, but I need to do it with a bit of thoughts here, because our test is called 'A unit cannot move outside of the map'. So it won't just be any tile that I will instantiate, but a tile outside of the map coordinates. Well, since there is four direction in which I can get out of the map, I might as well try it with four different tiles, in the same test.

	test( 'A unit cannot move outside of the map', ()=> {
	  let unit = new Unit()
	
	  let tileNorth = new Tile(0, -1, '.')
	  let tileWest = new Tile(-1, 0, '.')
	  let tileSouth = new Tile(0, 13, '.')
	  let tileEast = new Tile(13, 0, '.')
	
	  expect(unit.canMove(tileNorth)).toBe(false)
	  expect(unit.canMove(tileWest)).toBe(false)
	  expect(unit.canMove(tileSouth)).toBe(false)
	  expect(unit.canMove(tileEast)).toBe(false)
	})

Which still fails, because I still didn't update my production code in consequence. Here it is :

    canMove( tile ) {
      if ( tile.type === '.' &&
      tile.x <= 12 && tile.x >= 0 &&
      tile.y <= 12 && tile.y >= 0) {
        return true
      }
      return false
    }

That seems to be a lot of code for testing such a simple function, I admit. But I need to be sure that I'm not letting cases in which my code may break without being noticed by my automated tests. In fact, to assist me in this task, every test automation framework I know of implements a feature called **code coverage.**

> Note: Notice how I have instantiated my tiles with the type parameter set to '.'. Indeed, I didn't want my test to fail because of the wrong value for that parameter, but only with coordinates outside of the map. 

## Testing with coverage

That nice feature is provided by *Jest* if I ask him nicely with the option `--coverage`. But I don't want to check for the coverage every time I run my tests, because it has an overcharge on performance. So I create another script that I add in my `package.json` :

	"scripts": {
	    "test": "jest",
	    "test-coverage": "jest --coverage"
	  },

Now if I run the command `npm run test-coverage` in my console, the output will include a nice table that shows me how much percent of my production code I covered with my tests. But it's not all, I will also have a more detailed report that will be generated in the subfolder `coverage/lcov-report` as a bunch of HTML files. I can open them with my web browser and it will show me the exact lines of code which are covered by my tests, and those which are not. Let's open the report for my `Unit.js` file.

![Jest coverage report](../assets/tdd-001_coverage.png)

As you can see, the green marks indicate that my lines are covered here. But there's something bothering me: you can see that line 21 is calculated to have been covered 5 times (the little '5x' next to it). Since *Jest* is an automated tool, it has limitations in understanding the code that humans wrote. Here, it doesn't make a difference if my condition fails because the tile is not of the right type, nor the tile is too far East, West, North or South... It's all the same line of code for him.

This outline two facts. Firstly, that a code coverage report, while helpful, is by no means an insurance of your whole code being absolutely tested in all cases that may exist. And so, bugs may still exists in hidden parts of it. And secondly, that if I want to benefit the most from my tests, I will have to write my production code with less concision, so it can be analyzed with the more efficiency by my automated test framework (that's not *Jest* specific). Let's try:

	canMove( tile ) {
      if ( tile.x <= 12 ) {
        return false;
      } else if ( tile.x >= 0 ) {
        return false;
      }
      
      if ( tile.y <= 12 ) {
        return false;
      } else if ( tile.y >= 0 ) {
        return false;
      }
      
      if ( tile.type === '.' ) {
        return true
      }
      return false
    }

I must concede, this is ugly code, though it ... Oops! Tests fails. Let's see what happened... Ah! I modified the logic, making the method returns false if any of the coordinate verification notice an incorrect value, but I didn't reverse the comparison signs when refactoring. That's a great benefit of *TDD* shown here: I can refactor my code at will, and I will be warned each time I break something by doing so. The great thing is that it is immediate, and because I test frequently, I know the bug must have been created in the few minutes interval between my last passing test and now. And that's also why it is important to always make all your test pass before writing more production code: it narrows the leads to fix the issues when you create them. Correcting it, let's take a look at my code coverage here:

![Jest coverage report](../assets/tdd-001_coverage.png)

Much better, we can see that each one of my `return` for an incorrect coordinate value is tested at least once. But it also outlines that the last `return`, the default behavior is not tested. We can do it easily, by testing the case where the tile is a 'void tile' (see the rules), which means the character '#'. I believe you get the point now, and I won't just demonstrate every test case for this project.

> Note : In my previous note, I was worried that testing with tiles of another type than neutral (the '.') might pass the test but for the bad reason. As my production code is written now, the coordinates are checked before the tile type, so it doesn't matter anymore which type I instantiate the tile in my test. But I'll keep it that way, just to be perfectly clear. (Of course, I could have solved this problem by getting advantage of javascript's *lazy evaluation*.)

## Getting fancier

Let's look a bit further into this development. Units have special rules, that allow them to 'kill' another unit depending on its level. Here's what the rules say:

> Army units can only destroy units of inferior level, except level 3 units which can destroy any unit. 

So I started to write the test for my level 1 unit: 

	test( 'A level 1 unit cannot move wherever there is a unit of its level or above', () => {
	  let unitLvl1 = new Unit(1)
	  let tileWithUnitLvl1 = new Tile(0,0, 'O', new Unit(1))
	  let tileWithUnitLvl2 = new Tile(0, 1, 'O', new Unit(2))
	  let tileWithUnitLvl3 = new Tile(1, 1, 'O', new Unit(3))
	
	  expect(unitLvl1.canMove(tileWithUnitLvl1)).toBe(false)
	  expect(unitLvl1.canMove(tileWithUnitLvl2)).toBe(false)
	  expect(unitLvl1.canMove(tileWithUnitLvl3)).toBe(false)
	})

Well, you would have guessed, the parameter given to the `Unit` *constructor* is the level of the `Unit` *instance*. Now, I could totally copy/paste this code and change the values for level 2 and level 3, but as with every copy/pasted piece of code, it wouldn't feel right... Rejoice, because *Jest* has our back covered here (and probably many other test automation frameworks would do as well). The syntax may vary for each test automation framework, but the concept is the same, and it's called **parameterized tests**. Let's see how it looks like.

	test.each([
	  [1, false, false, false],
	  [2, true, false, false],
	  [3, true, true, true]
	])(
	  'A level %i unit cannot move wherever there is a unit of its level or above',
	  (level, expectLvl1,expectLvl2, expectLvl3) => {
	    let unitLvl1 = new Unit(level)
	    let tileWithUnitLvl1 = new Tile(0,0, 'O', new Unit(1))
	    let tileWithUnitLvl2 = new Tile(0, 1, 'O', new Unit(2))
	    let tileWithUnitLvl3 = new Tile(1, 1, 'O', new Unit(3))
	    
	    expect(unitLvl1.canMove(tileWithUnitLvl1)).toBe(expectLvl1)
	    expect(unitLvl1.canMove(tileWithUnitLvl2)).toBe(expectLvl2)
	    expect(unitLvl1.canMove(tileWithUnitLvl3)).toBe(expectLvl3)
	  }
	)

There's quite some novelties here. I will deconstruct it, but what you shall understand, is that it basically works like a parameterized function at its core.

First thing first, the array of arrays passed to the function `each` define values for our **parameters**. Each of the inner arrays is describing one execution of the test. As I have three inner arrays, my test will be executed three times. The values that the parameters will take are the values inside those arrays. Which parameters, may you ask?

That's our third point, as you can see, after the name of the test, I've named those said parameters. Order is important here, as the first value in each of my inner arrays would be passed as the first parameter I've named, the second to the second, and so on...

But it seems that I've skipped the second point. You may have noticed it already, but the name of the test contains a special expression, which is `%i`. This expects a parameter, and the `i` specifies that it will be formatted as an integer. So each time the test is run, it will change its name according to the first parameter which is passed to it. I could absolutely have left the same name for each execution of this test, but it would have been harder to guess the conditions under which my tests fail or pass.

Then in the body of the test function, you can see that I call for the parameter to be replaced by the set of values I passed to it. Obviously, first parameter is used to changed the level of the `Unit` I instantiate. Then the three following ones are used as the values I expect in my *assertions*.

A great benefit of that syntax, is that I could easily check whether my is correct or not. In the parameters, I can quickly verify that my calculations are correct. And in the function body, I only have to inspect that my logic is right. Speaking about ease of reading ...

> Note: Pay close attention to the syntax here. The `each` method ends after the array of parameters, but as it returns a function, I had to open a new parenthesis directly after closing the one from that method to give the parameters to my dynamically created test function.

## A clearer syntax for writing tests

When you start writing test, and moreover, doing test driven development, there's a high probability it's because you are writing code that you will be reusing and modifying it in the future (or you maybe you are just a 'test everything' maniac like I am). You can be sure that you will have to modify your tests accordingly. Because some functions will become obsoletes, other will need more specific testing, when you're not just changing the parameters type you expect in such functions... You better be able to understand what you have been testing pretty fast, otherwise the whole process will be a drag towards exhaustion. It is even more important when your code as to be reused and modified by other developers!

Now that you've been warned, I'd like to propose you a pretty common way of structuring your tests into three steps:

1. The context : When you are writing test, you are creating a specific context in which your program is run. **You have to be in total control of that context**, I can't stress enough how important it is. Because whether your tests pass or fail, you have to be know the exact details about the state in which your program was, otherwise you won't be able to deduce the reasons it failed (or it may pass but with an unnoticed bug). We'll label this step with the word `Given`.
2. The action : Well, you are testing some behavior of a part of your program, so you call for execution of that function or method you are testing. We use the label `When` here.
3. The assertion(s) : That's when you compare the values you've got from the previous step with the values you expected. That's the `Then` step.

Here's what it looks like If I modify my test for clarity' sake:

	(
	  'A level %i unit cannot move wherever there is a unit of its level or above',
	  (level, expectLvl1,expectLvl2, expectLvl3) => {
	    // Given
	    let unitLvl1 = new Unit(level)
	    let tileWithUnitLvl1 = new Tile(0,0, 'O', new Unit(1))
	    let tileWithUnitLvl2 = new Tile(0, 1, 'O', new Unit(2))
	    let tileWithUnitLvl3 = new Tile(1, 1, 'O', new Unit(3))
	
	    // When
	    let canMoveOnLvl1 = unitLvl1.canMove(tileWithUnitLvl1)
	    let canMoveOnLvl2 = unitLvl1.canMove(tileWithUnitLvl2)
	    let canMoveOnLvl3 = unitLvl1.canMove(tileWithUnitLvl3)
	
	    // Then
	    expect(canMoveOnLvl1).toBe(expectLvl1)
	    expect(canMoveOnLvl2).toBe(expectLvl2)
	    expect(canMoveOnLvl3).toBe(expectLvl3)
	  }
	)

Notice how I changed my code to make a distinction between the action and the assertion (which I previously have written on the same line for concision). Although my test code is more verbose, it is also easier to understand with a quick look.

You can use this structure to help you planning on the test you'll write by writing it in plain English first (or any human readable language you are speaking). For example, I could (and should) have written the following comment at first:

	/* Given that I have a unit of certain level, and three tiles on which stands respectively:
		- a level 1 unit
		- a level 2 unit
		- a level 3 unit
	*/
	
	/* When I try to move my unit on each of these tiles */
	
	/* Then I expect my unit to be able to move only on the tiles with a unit of an inferior level,
	excepted if my unit is level 3, in which case it should be able to move on every tile */

This is a good practice because writing automated test shouldn't be an automatic process in itself. In fact, if you have carefully thought out your tests, you may already have done 80% of the thinking for the production code that will be tested as well. The goal, input and output for your *system under test* will already be planned, you'll just have to mingle with implementation details then.

## Wrapping it up

Well, I hope that *TDD* makes a little more sens to you now, and that you will be eager to start implementing it in your own projects, even gradually. In fact, that's something developers may not realize immediately, but it's not because you've decided to do some *TDD*, that every little bit of your application needs to be covered by tests!

I admit, judging which parts would benefits more from *automated testing* than others would be not that easy when you are just beginning, and in case of doubt, you really should just try to write some tests. But don't push it too hard! *TDD* is supposed to be a tool to save you time, so if you're hustling with writing your test, step back, analyze if you really need it, and decide if you can't just write it later.

All in all, it is as much a skill as developing software, and you'll get better at it with **consistent practice**. So start now, try to push a little further each time, and soon you'll build sturdy *tests suites* helping you solve bugs in the minute they are introducing in your applications. You have my word!

## Resources 
 
[^1] Grégory Ribéron - De bronze à légendaire, comment réussir vos AIs ?[youtube video](https://www.youtube.com/watch?v=8kBQMQyLHME)
[^2] The Clean Code Blog - The Cycles of TDD, [clean coder blog](https://blog.cleancoder.com/uncle-bob/2014/12/17/TheCyclesOfTDD.html)