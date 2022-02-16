[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)

# JavaScript Objects: Referencing Own Properties


## Objectives

- Contrast the definitions of "property" and "method".
- Access properties within a method of the same object using `this`.

## Preparation

1. [Fork and clone](https://git.generalassemb.ly/ga-wdi-boston/meta/wiki/ForkAndClone)
    this repository.
1. Create a new branch, `training`, for your work.
1. Checkout to the `training` branch.


## Kinds of Properties

Suppose we have the following object literal:

```js
{
  foo: 'bar',
  baz: function () {
    // How do I access the value stored in 'foo' above?
  }
}
```

`foo` and `baz` are both **properties**, also known as keys. We typically use
the term "keys" when object literals are used as dictionaries. When we mix data
and methods, we should prefer the term "object" over "dictionary". So, we'll
also call the accessor name a "property" instead of a "key".

`foo` is a data item, referred to as a _property_. On the other hand, `baz`
points to a function that can be invoked, and is known as a _method_.

For the remainder of this talk, we will be focusing exclusively on how we can
use `this` inside of a method to point to value defined elsewhere in an object
literal. All other uses of `this` are out-of-scope.

The answer to the question posed in the previous code snippet is that we use
`this` to refer to the object's own properties. That is to say, when we use
`this` inside a method, that method is contained within an object. For the
patterns used in this talk, the containing object is what `this` refers to.

```js
{
  foo: 'bar',
  baz: function () {
    return this.foo
  }
}
```

*Do not over-generalize*. We usually *cannot know what `this` refers to* until
the code runs.

## `this`

One way to break up the complexity of a problem is by using multiple kinds of
objects together, and having each object be responsible for representing a small
part of the problem. But these objects don't need to exist in isolation -
objects can have other objects (or even collections of other objects) as
properties.

Suppose that we wanted to create a simple program ('RunTracker') that helps
people prepare for running a 5k. Each day that a person runs, they create a
record of their run which contains:

- the date and time of the run
- the distance covered, in meters
- the time taken, in seconds

The program also stores information about the user (the user's name and email
address) and can perform some calculations (total distance run, longest distance
run so far, and average speed).

## Lab: Diagram and Model

Using the description of the program above, create an entity diagram.

1. Identify the entities (kinds of objects) needed in the program.
1. Draw a box for each entity and label it with the singular, capitalized
    entity name.
1. Connect any entities that are related using a line.
1. List attributes and methods of each entity separately within each entity's
    box.

## Demo: Write Methods With `this`

When we start thinking about how the methods for 'User' will work, we run into a
difficulty. A method for calculating the longest distance run so far needs to be
able to access, and refer to, all of the runs associated with that particular
user. We will use `this` to make that connection.

> avgSpeed = totalDist / totalTime

Watch as I demonstrate how to complete writing each method.

```js
const user = {
  name: 'Christopher Robin',
  email: 'sei@christopherRobin.com',
  runs: [
    {
      date: '2017-05-25 15:00',
      distance: 1200,
      timeTaken: 600
    },
    {
      date: '2017-05-25 15:00',
      distance: 1400,
      timeTaken: 800
    }
  ],
  totalDistance: function () {},
  longestRunDistance: function () {},
  averageSpeed: function () {}
}
```

## Lab: Self-Referential Objects

In teams, you're going to work on a similar program to our previous one, this
time for meal tracking. In particular, you're going to create a 'User' object,
complete with several 'Meals'.

Add your code to [`lib/meals.js`](lib/meals.js), structured similarly to
[`lib/runs.js`](lib/runs.js).

A 'User' needs to have:

- a name (`name`)
- a date-of-birth (`bornOn`)
- a target daily calorie intake (`calorieTarget`)
- a list of 'Meals' that they've eaten (`meals`)

Every 'Meal' must have:

- a title (`title`), e.g. 'breakfast', 'lunch', 'dinner'
- a date (`date`), represented as a string e.g. '2016-06-25'
- a description (`description`)
- a number of estimated calories (`calories`)

Then, create the following methods for your instance of a 'User':

- `caloriesEatenOn`, which accepts a date (in the format above) and calculates
    the total number of calories consumed on that date.
- `avgDailyCalories`, which (as indicated), calculates the average number of
    calories consumed per day, rounded down to the nearest whole calorie.
- `onTrack`, which compares averageDailyCalories to the User's target daily
    calorie intake, and returns `true` if average caloric intake is at or below
    the target (or `false` if the reverse is true).

## Additional Resources

- [MDN `this`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)
- [Understanding the `this` Keyword in JavaScript](https://medium.com/better-programming/understanding-the-this-keyword-in-javascript-cb76d4c7c5e8)
- [`this` in JavaScript](https://john-dugan.com/this-in-javascript/)

## [License](LICENSE)

1. All content is licensed under a CC­BY­NC­SA 4.0 license.
1. All software code is licensed under GNU GPLv3. For commercial use or
    alternative licensing, please contact legal@ga.co.
