# rnp

As far as the vacancy which i am applying is Senior Software Engineer and the primary stack is 
(VueJS, SolidJS, TailwindCSS) i decided to use VueJs 3 and tailwindcss together. 
The architecture of the application is a typical view component using the state and methods for working with it, 
as well as event handlers for DOM elements. Since this test task, I did not create a separate component, but wrote 
the code in App.vue. As far as I can tell from my manual testing, I covered 4 cases described in the test task description.
As for the things that I would have completed if I had more time, then this is a check for the correctness of entering 
numbers or an expression from the user. I did some basic validation checks. For a real application in production, 
the checkCorrectInput method must of course be extended.
How to install and run the code is described below, this was generated automatically via vue-cli.

Please note that i tried to emulate a console so to enter expression in Input you should click on Enter.

Link to the hosted application is https://denys-vladymyrov.com/rnp/

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
