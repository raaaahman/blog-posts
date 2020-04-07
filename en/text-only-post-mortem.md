# Avoid these pitfalls during your next game jam (as I wish I did)

Game jams are events I do really enjoy. I'm not a professional game developer, but they tend to push my programming knowledge, development workflow and problem solving skills to test. Last week, I registered for [8 Bit to Infinity's Text Only Jam](https://itch.io/jam/text-only-jam), but failed to submit a game before the deadline. In this post I'm gonna share with you the lessons I've drawn from this experience, trying to warn you against the mistakes I did during this game jam.

## Not meeting the requirements from the start

As the rules were to build a game that only uses text as graphics, I came with the idea that I can develop my game testing it only through command line interface. After all, it is going to be a textual game, right? Well, the **requirements** were clear: the submission must have to be a game running at least on Windows 10, without the need for installing external tools. I didn't really bother with it until the very last hours, but I then had to learn how to create a GUI and export my game to an executable file in these last three hours, which I failed to complete in time...

It turns out it isn't enough to build with release in mind. You need to have a valid release **in your hands** as soon as possible. Even if it's just a program printing 'Hello World!' on a black screen. It is important because at that point you know that your build process is working, and you know how much time it's gonna take you. Joshua McLean, our jam host, was quite forgiving with people that might have run into compilation troubles, but some other jam might be more strict regarding the **deadline**. And what would be more frustrating than not qualifying for a jam with a fully playable game just because you couldn't compile it in time?

## Trying out new tools

For this jam, I decided to code my game in Python, as I have accumulated a whole lot of e-books about it and it seemed to be an easy language to learn. In fact, I even used it some time ago, during a three days course at school. Needless to say, I spent more time re-reading the chapters of these e-books and searching through the documentation than coding features... when I wasn't just debugging without dedicated tools (because I don't know none yet in Python)!

There is a time for learning, and a time for applying what you've learned. Jams fall in the second category. I'm not saying here that you shouldn't try something new, as it is always fun to **experiment** with fun new ways to make stuff on such occasion. But this is not a time to study a new language, framework or IDE. The words are important here, *try* and *experimenting* relates to a practice, whereas *learn* and *study* lean more towards theory. Think of it as guided or independent practice versus lesson time where you were in school. Even use the bare programming language if it's the only thing  you know for now, you will have plenty of time to learn new tools until the next jam.

## Failing to plan

The *Text Only Jam* had that advantage over most of the jams that its theme and limitations were known before the jam even started. So I figured out that I should take a bit of time to write a **to do list** for the development of my game. That way, I could have compared my progress to my expectations and then re-evaluated my **priorities** as the time fleets. But I've been occupied  and then the jam started before I wrote my plan, so I just dove right into the development process. After all, I was following the steps from a book titled *Learning Python Application Development*, which uses the building of a text based game as a guideline, so what could go wrong? Well, apart that the book is more than 400 pages long and doesn't include a chapter about exporting the application in a Windows executable format I mean...

Whatever the duration of the jam, you must be extra careful about how much time you are actually gonna put into the development process. If the jam is 48 hours long, you just don't code, write, design and brainstorm 48 hours straight. There are pauses, obligations and, you know, just life going its way... Jamming is just like any other activity you do, you have to **allocate time** to it. And that time will define how much you can build before the bell rings. If you're used to *agile development*, just think about it as a *sprint* (this depends on jams though, some may be -very- short sprints, other may be several sprints, but you get the picture...). If you don't know about how agile development works, a sprint is a very simple process: You define the **tasks** (or *user stories*) you will do beforehand, in order to produce a **deliverable** product in a given **time frame**. That may seem too obvious to even bother with, but my consistent failures to meet deadlines are becoming a strong motivation not to overlook this practice in the future.

## Continue your life as normal

As I still have my job that couldn't be skipped during the week, and some family visits that were planned ahead during the week-end, I decided to go all out during my remaining free time and put it into the jam. Coding even just before bed time, when I usually forbid myself to. As a result, I built up fatigue and had to struggle with willpower to put **consistent effort** until the finish line.

There is a reason why we build our **habits**. These are where we draw our energy, our curiosity and our stillness from. Don't give up on them! If you need a 8 hour sleep to get your brain refreshed, get these sleep hours. If you need a 30 minutes morning meditation to think clearly through the day, thinking clearly will get you further into the jam than 30 minutes of messy coding. If they are important enough to carry out your regular day, how are you gonna go through stressing periods (like game jams are) without them? When  you put *extra* work, this means that you also need the get the *normal* work done. So definitely don't skip on your energy and focus sources!

## Prioritize player experience

The mistakes I've talked about so far, I've already done them several times. And I hope that writing them out will help me improve on these areas next time. But there's also a trap that I'm starting to recognize and anticipate: it is **overscoping** your game.

Temptation is always very high to try to shine on each evaluation criterion written in the jam rules. But in the end, it has to be a game. That seems silly to point out, but games are **valued by players** with specific considerations like overall fun, instinctive controls and fulfilling experience, even if it is not stated in the jams evaluation criteria. And there's a very high probability that the judges will be playing your games rather than just reading your code or staring at your design documents (you wrote design documents? Congrats then, you may probably not need my advice ;)).

So I'm starting to fiddle with the following five **incremental steps** that one should try to validate during a game jam. Beware the word 'incremental' here, as it don't necessarily translate in the addition of new features for your game. Sometimes getting rid of the 'noise' to focus on the essential is more of an increment in value than shiny unique features. I'm no game design specialist, but still let me expose my draft for *Five Steps to Succeed a Game Jam*:

1. Make something **functional**: Obviously, you have to produce a working piece of software, something that doesn't need too specific requirements to run and doesn't crash on a regular basis. Otherwise, players will quickly quit your game.
2. Make something **playable**: You are not making just any software, you are making a game. This means it has to have some winning and loosing conditions that are understandable by the player. Or at least some feeling of progression, like in incremental/idle games (like *Cookie Clicker* or *Candy Box*).
3. Make your game **fun**: What does fun means, and how one could infuse its game with it is a debatable topic. But something has to motivate your player to keep interacting with your game. There's no magic formula here, but if you are reluctant to play your own game, there may not be a lot of people willing to play it neither.
4. Make your game **original**: While not strictly required for players to enjoy your game (think about sequels, they are usually improved versions of the same mechanics than their predecessors), a game jam might have a lot of entries. It might not be very enticing to play 'Diablo clone #3413', especially if there are other Diablo clones competing in the same jam. Although, originality is a tough subject, and I don't believe something shouldn't be done just for originality's sake. But yeah, opinions...
5. Make your game **impressive**: This step, very few might achieve it. Either on a technical, artistic, narrative or whatever standpoint. In fact, I make it a step in my proposed process just to make it the last. If you happen to reach  impressiveness, congratulations. If not, that's no big deal.

Order is crucial here, as players won't get much value of an original idea if the game refuse to launch. And they won't stare too long at your breakthrough in particle physics if there isn't any gamey mechanic to exploit it... You get the point, have your jam entry validate these steps progressively. You might not end up in the top ranks, but you might be able to submit something usable when time is over, as I wish I did...

## Final words

Even through this bitter end, I still do enjoy jamming. I'm still really disappointed to not have overcome these pitfalls which I've already stumble upon in previous jams. But this is a worthy reminder that both programming and learning are **iterative processes**, and failures are just part of them. So maybe I'll meet you in a next game jam! 