# TODO — Koalect

I use Vue-cli

[result](https://gracious-northcutt-914478.netlify.com/)

## Project setup
```
npm install
```

## Docs
I created one list in the app.vue to simulate data (todoList), I pass this to a component "todo" that I created. Into this component I make a loop on the computed data (filteredTask), a class is apply if task is completed. If I have not tasks so I show "Nothing to do"

Minimum data in each task: value = string, edit = boolean, completed = boolean

I used a component to have a reusable code and I try to make ES6 to be in the trend

DELETE & ADD: If I do an action on the state of the application (data), I work with the function in the app.vue to have all the code corresponding to the data in the same file

EDIT: it is only a switch that I made online because a method is not necessary. I use v-if and not v-show to not display the code in html by default.

FILTER: I make function directly inline because if i made a method I should have make a big condition
