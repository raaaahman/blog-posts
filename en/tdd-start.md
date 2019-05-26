# Test Driven Development, a practical start

## My first test case

Because of *TDD* works, it will force me to go through inspecting the rule before writing code. Indeed, I will have to write a test to ensure that my program conform to those rules. So, I will start to inquire how unit movement works. Here's what the rules said:

> The map is a grid of size 12x12, where the top-left corner is the cell (0,0). The map is randomly generated at the start of each game. 

Okay, everything is very well understandable for a human, but a computer needs much more specific instructions. So my first decision is to write that will verify that a unit won't effectively try to move outside of the map.

Here's how Robert C. Martin ( alias *Uncle Bob* ), a famous *TDD* evangelist, worded the first step in a *TDD* process, in what he calls *Three laws of Test Driven Development*[^1] :

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


## Moar tests!

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
 
## Resources 
 
[^1]  The Clean Code Blog - The Cycles of TDD, [clean coder blog](https://blog.cleancoder.com/uncle-bob/2014/12/17/TheCyclesOfTDD.html)