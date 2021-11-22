# Scope Homework: Who Dunnit

### Learning Objectives

- Understand function scope
- Know the difference in between the let and const keywords

## Brief

Using your knowledge about scope and variable declarations in JavaScript, look at the following code snippets and predict what the output or error will be and why. Copy the following episodes into a JavaScript file and add comments under each one detailing the reason for your predicted output.

### MVP

#### Episode 1

```js
const scenario = {
  murderer: 'Miss Scarlet',
  room: 'Library',
  weapon: 'Rope'
};

const declareMurderer = function() {
  return `The murderer is ${scenario.murderer}.`;
}

const verdict = declareMurderer();
console.log(verdict);
```

It will print "The murderer is Miss Scarlet". The log is printing "verdict", which is calling the declareMurderer function - which takes the scenario.murderer value as part of the string. A fairly straightforward episode - perhaps we could introduce more complexity or some sort of twist? We need to keep the audience hooked from the first episode.

#### Episode 2

```js
const murderer = 'Professor Plum';

const changeMurderer = function() {
  murderer = 'Mrs. Peacock';
}

const declareMurderer = function() {
  return `The murderer is ${murderer}.`;
}

changeMurderer();
const verdict = declareMurderer();
console.log(verdict);
```

This will throw up an error because you're trying to reassign the const variable "murderer" in the changeMurderer function. A diassappointing end to a promising murder mystery. Perhaps this episode could do with some more work - more character development?

#### Episode 3

```js
let murderer = 'Professor Plum';

const declareMurderer = function() {
  let murderer = 'Mrs. Peacock';
  return `The murderer is ${murderer}.`;
}

const firstVerdict = declareMurderer();
console.log('First Verdict: ', firstVerdict);

const secondVerdict = `The murderer is ${murderer}.`;
console.log('Second Verdict: ', secondVerdict);
```
This will print  "First Verdict:  The murderer is Mrs. Peacock" on one line and "Second Verdict:  The murderer is Professor Plum" on the next line. This is because firstVerdict calls declareMurderer which in turn takes the murderer variable from within the scope of the function. secondVerdict uses the murderer variable as defined globally at the top of the episode, it does this via string interpolation. This provides the audience with dramatic tension as the initial verdict is a red herring. What new information led to the second verdict? A surprise last minute revelation?

#### Episode 4

```js
let suspectOne = 'Miss Scarlet';
let suspectTwo = 'Professor Plum';
let suspectThree = 'Mrs. Peacock';

const declareAllSuspects = function() {
  let suspectThree = 'Colonel Mustard';
  return `The suspects are ${suspectOne}, ${suspectTwo}, ${suspectThree}.`;
}

const suspects = declareAllSuspects();
console.log(suspects);
console.log(`Suspect three is ${suspectThree}.`);
```

This will print out "The suspects are Miss Scarlet, Professor Plum, Colonel Mustard. Suspect three is Mrs. Peacock." This is because suspectThree is redeclared within the block scope of the declareAllSuspects function (inserting Colonel Mustard) but the final line of code is outwith this block so it takes the suspectThree variable as Mrs. Peacock. This is surprising as it implies that Colonel Mustard has secretly been Mrs. Peacock the entire time. Maybe we could rewrite the earlier episodes to include some foreshadowing?

#### Episode 5

```js
const scenario = {
  murderer: 'Miss Scarlet',
  room: 'Kitchen',
  weapon: 'Candle Stick'
};

const changeWeapon = function(newWeapon) {
  scenario.weapon = newWeapon;
}

const declareWeapon = function() {
  return `The weapon is the ${scenario.weapon}.`;
}

changeWeapon('Revolver');
const verdict = declareWeapon();
console.log(verdict);
```

This should print "The weapon is the Revolver" - we're using the function changeWeapon to mutate the value for the scenario.weapon from Candle Stick. This is definitely a positive change - guns are more exciting than candlesticks. We should see if it's possible to show or mention the gun earlier in the series - it's called "Chekovs Gun" for a reason! 

#### Episode 6

```js
let murderer = 'Colonel Mustard';

const changeMurderer = function() {
  murderer = 'Mr. Green';

  const plotTwist = function() {
    murderer = 'Mrs. White';
  }

  plotTwist();
}

const declareMurderer = function () {
  return `The murderer is ${murderer}.`;
}

changeMurderer();
const verdict = declareMurderer();
console.log(verdict);
```
This should print "The murderer is Mrs. White". This is because we're using the declareMurderer function to print the string with the murderer value via string interpolation and we're using the changeMurderer(with nested plotTwist) function to mutate the value of murderer from Colonel Mustard. Great timing for such a twist - a mid-series revelation like this is the perfect cliffhanger to set us up for the back 4 episodes - could it be too unbelivable though? We'll need to make sure we've laid the groundwork in the first few episodes.


#### Episode 7

```js
let murderer = 'Professor Plum';

const changeMurderer = function() {
  murderer = 'Mr. Green';

  const plotTwist = function() {
    let murderer = 'Colonel Mustard';

    const unexpectedOutcome = function() {
      murderer = 'Miss Scarlet';
    }

    unexpectedOutcome();
  }

  plotTwist();
}

const declareMurderer = function() {
  return `The murderer is ${murderer}.`;
}

changeMurderer();
const verdict = declareMurderer();
console.log(verdict);
```
This should print "The murderer is Mr. Green". This is because there is errors in the way that the murderer variable has been declared. Removing the let statement from the plotTwist function should allow this plotline to develop as intended. This feels clunky in it's execution - we need need to stick the landing on these last few episodes so that we can set up series 2!! 

#### Episode 8

```js
const scenario = {
  murderer: 'Mrs. Peacock',
  room: 'Conservatory',
  weapon: 'Lead Pipe'
};

const changeScenario = function() {
  scenario.murderer = 'Mrs. Peacock';
  scenario.room = 'Dining Room';

  const plotTwist = function(room) {
    if (scenario.room === room) {
      scenario.murderer = 'Colonel Mustard';
    }

    const unexpectedOutcome = function(murderer) {
      if (scenario.murderer === murderer) {
        scenario.weapon = 'Candle Stick';
      }
    }

    unexpectedOutcome('Colonel Mustard');
  }

  plotTwist('Dining Room');
}

const declareWeapon = function() {
  return `The weapon is ${scenario.weapon}.`
}

changeScenario();
const verdict = declareWeapon();
console.log(verdict);
```
This shoudl print out "the weapon is Candle Stick". This is because the changeScenario function mutates the room to Dining Room, this then cases the plotTwist IF statement to be true which changes the murderer to Colonel Mustard. In turn this cases the unexpectedOutcome function to return a true for it's IF statement which changes the weapon to a Candle Stick. I know we're trying to be up-market with this show but I think we should give Colonel Mustard a catchphrase? He's clearly the breakout character and marketing would love it! Colonel Mustard spin-off?!?  

#### Episode 9

```js
let murderer = 'Professor Plum';

if (murderer === 'Professor Plum') {
  let murderer = 'Mrs. Peacock';
}

const declareMurderer = function() {
  return `The murderer is ${murderer}.`;
}

const verdict = declareMurderer();
console.log(verdict);
```
This will print "The murderer is Professor Plum". This is because the "let murderer = 'Mrs. Peacock'" only mutates the value within the scope of the block that it's within. Removing the "let" would allow this to function as intended. Is this really the best we can come up with for the PENULTIMATE episode of the season? We need to ramp things up, not slow them down! 

