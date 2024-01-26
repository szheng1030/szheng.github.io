---
title: "Picking up Unity again"
layout: post
date: 2024-01-25 18:38
headerImage: true
image: https://szheng1030.github.io/assets/unity-flappyicon.png
tag: 
- unity
- C#
category: blog
author: sam
description: "Some thoughts about while I relearn Unity"
---

### Wow I wrote really shit code 5 years ago

... was my first, visceral reaction after picking Unity back up.

Before that, quick context.<br>
Following some "certain life events", let's just say I found myself with some more free time during my day, hence trying Unity out again.
The game isn't anything unique, just an extra gameplay added onto run-of-the-mill Flappy Bird clones, just so I could familiarize myself with the environment.
Images of obscure birds will appear in the background during regular flappy bird gameplay and you're tasked with guessing the name of the bird between 2 choices.
This extra game mechanic was mostly inspired by this segment from [Game Changer](https://youtu.be/hjmiDzLJ9VQ?si=4wxTBQIRb3O6-kpZ&t=70).

That being said, if you want to learn the names of some obscure birds, you can play the game on [itch.io](https://lostdirectory.itch.io/flappy-trivia).<br>
And the entire project is also uploaded to [GitHub](https://github.com/szheng1030/flappy-trivia).
<div>
    <p>
        <img src="{{ site.url }}/assets/unity-ss1.png" alt="Exhilarating gameplay"/>
        <figcaption>Exhilarating gameplay</figcaption>
    </p>
</div>

### Back to how absolutely abhorrent my code was 5 years ago

For starters, apparently 5-years-ago me didn't know about \[SerializeField\], thus the birth of monstrosities like this:

<div>
    <p style="text-align:center">
        <img src="{{ site.url }}/assets/unity-ss2.png" alt="Surely there's a better name than playerExitSpecialStatus"/>
        <figcaption>Surely there's a better name than "playerExitSpecialStatus"</figcaption>
    </p>
</div>

Can't attest to what these variables are for, but I can say with confidence almost none of these need to be public.
I also wrote no comments at all, fun!
Unsure if it was ignorance, lack of knowledge, or just blatant disregard for writing sensible code.
There are more terrible code examples, such as switch cases longer than the 80ft ethernet cable from Amazon for $15 that is definitely CAT8 as it advertises, 
but there probably isn't much merit delving into them outside of sending myself into a depressive spiral.

### Making a proper state machine

The only state machine needed in this small game was one that controlled the game loop, or rather, the periodic spawning of trivia prompts.
So, if we defined a base template that has abstract enterState and updateState functions, we can easily create new states by overriding and adding functionality to said functions.
This way, all we need to do is to instantiate the states in a state manager and simply call the enter/update as needed.

There are definitely more robust implementations of state machines such as with scriptable objects, behaviour trees, or cool open packages like [UnityHFSM](https://github.com/Inspiaaa/UnityHFSM).
Overkill in our case here though! So for a later time.

<div>
    <p style="text-align:center">
        <img src="{{ site.url }}/assets/unity-ss3.jpg" alt="State machine implementation"/>
        <figcaption>State machine implementation</figcaption>
    </p>
</div>

### The new input system

I didn't realize there was a new input system until I was doing some final code cleanup.
It's an info dump at first but the new system does prove to be much more robust than GetKeyDown().
Especially when supporting multiple control schemes, this system can easily accommodate that with different action maps.
This allows for calls to the action name directly and abstracts away specific keypress, making the script much more robust.
Can't attest to if the performance is any better than the original system, but at this point, anything beats polling for keypresses in an Update() function.

<div>
    <p style="text-align:center">
        <img src="{{ site.url }}/assets/unity-ss4.jpg" alt="Action Maps"/>
        <figcaption>Action maps for different input schemes abstract away keypresses from the script</figcaption>
    </p>
</div>

### More Unity?

To be honest, this small project was very much just to get into the flow of working on silly little games.
I want to try out Godot since it's the cool new kid on the block, it's been praised pretty substantially as well, and it's open source!
Unity sometimes feels sluggish to use, perhaps due to all the systems the default packages comes with.
So that's probably the short-term plan; I will be missing Visual Studio's intellisense though. Rumours say GDScript's version is heavily lacking.

Ending the post with this game dev I stumbled across the other day.<br>
[Daniel Linssen](https://daniellinssen.games/), he's making some insanely cool stuff.