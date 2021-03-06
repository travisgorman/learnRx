# Functional Programming, Asynchronous Programming, learnRx 
This repository is for my notes and solutions as I work through the [*learnRx*](http://reactivex.io/learnrx/) exercises, along with Jafar Husain's course on [Frontend Masters](frontendmasters.com/) "Asynchronous Programming in JavaScript".

## Exercise 1: 
### Print all names in array to console

```js
function printNames() {
  var names = ["Ben", "Jafar", "Matt", "Priya", "Brian"];

  for(var i = 0; i < names.length; i++) {
    console.log(names[i]);
  }
}
```
`printNames()` does one very specific thing only. It prints the items in the `names` array declared in its own function scope. If you need the names 

>
Ben  
Jafar  
Matt  
Priya  
Brian  

printed out to the console in exactly that order, `printNames()` is the function to call.  

I'd like to take this idea, and make a more useful function. 

#### `printWithForLoop()`
`printWithForLoop()` does the exact same thing, except instead of declaring the array it loops and print, it takes any array passed in as an argument, and loops it, printing each item to the console. 
This is for just illustrative purposes, playing with the idea of array traversal, and assumes the array is in a scope where it can be accessed

```js
var names = ["Ben", "Jafar", "Matt", "Priya", "Brian"];
var otherNames = ["Travis", "Desdemona", "Des", "The Skoog", "Doogin" ]

function printWithForLoop(array) {
    for (var i = 0; i < array.length; i++) {
      console.log(array[i]);
    };
}
```
Pass `names` into `printWithForLoop()` 

```js
printWithForLoop(names);
```
>
Ben  
Jafar  
Matt  
Priya  
Brian  

Pass `otherNames` into `printWithForLoop()` 

```js
printWithForLoop(otherNames);
```
>
Travis
Desdemona
Des
The Skoog
Doogin

___
## Exercise 2
### Use forEach to print all the names in an array

```js
var names = ["Ben", "Jafar", "Matt", "Priya", "Brian"];

function printWithForEach (arr) {
  arr.forEach(function(item) {
    console.log(item);
  });
}
```
Pass `names` into `printWithForEach()`

```js
printWithForEach(names);
```
>Ben  
Jafar  
Matt  
Priya  
Brian  


___
## Exercise 3
### Project an array of videos into an array of {id,title} pairs using forEach()
For each video, add a projected {id, title} pair to the `videoAndTitlePairs` array.

```js
function getIdAndTitle () {
  
  var newReleases = [
    {
      "id": 70111470,
      "title": "Die Hard",
      "boxart": "http://cdn-0.nflximg.com/images/2891/DieHard.jpg",
      "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
      "rating": [4.0],
      "bookmark": []
    },
    {
      "id": 654356453,
      "title": "Bad Boys",
      "boxart": "http://cdn-0.nflximg.com/images/2891/BadBoys.jpg",
      "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
      "rating": [5.0],
      "bookmark": [{ id:432534, time:65876586 }]
    },
    {
      "id": 65432445,
      "title": "The Chamber",
      "boxart": "http://cdn-0.nflximg.com/images/2891/TheChamber.jpg",
      "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
      "rating": [4.0],
      "bookmark": []
    },
    {
      "id": 675465,
      "title": "Fracture",
      "boxart": "http://cdn-0.nflximg.com/images/2891/Fracture.jpg",
      "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
      "rating": [5.0],
      "bookmark": [{ id:432534, time:65876586 }]
    }
  ],
  videoAndTitlePairs = [];

  newReleases.forEach( (video) =>
    videoAndTitlePairs.push({id: video.id,title: video.title}) );
  return videoAndTitlePairs;
}
```
In the above function, as it appears in the exercise,  the array `newReleases` is declared inside the function. If this weren't the case, the function could be modified to take an `arr` parameter to be more flexible. 
```js
function projectWithForEach (arr) {
  var videoAndTitlePairs = [];

  arr.forEach(item => videoAndTitlePairs.push({ 
    id:item.id, title:item.title 
  }));
  return videoAndTitlePairs;
}
```
pass in `newReleases` as the `arr` argument to return an array with only the id's and titles  
```js
projectWithForEach (newReleases);
``` 
>```js
[
  Object {
    id: 70111470,
    title: "Die Hard" }, 
  Object {
    id: 654356453,
    title: "Bad Boys" }, 
  Object {
    id: 65432445,
    title: "The Chamber" },
  Object {
    id: 675465,
    title: "Fracture" }
]
```


___
## Exercise 4
### Implement map()
Add a map() function to the Array type. `map()` accepts the projection function to be applied to each item in the source array, and returns the projected array.   
```js
Array.prototype.map = function(projectionFunction) {
  var results = [];
  this.forEach(function(itemInArray) {
    results.push(projectionFunction(itemInArray));
  });
  return results;
};
```
1. Declare a function on the `Array.prototype` called `map()`
  * `map()` takes a `projectionFunction()` argument. 
  * `projectionFunction()` is any function you want it to be
  * You can pass in a helper function or create a funcion on the spot
1. Declare `results` array
1. Call `forEach()` that traverses `this`
1. performing  the `projectionFunction()` on each item in the array
1. pushing the result into the `results` array
1. and **return** `results`

___
## Exercise 5
### Use map() to project an array of videos into an array of {id,title} pairs
Repeat the exercise of collecting {id, title} pairs for each video in the `newReleases` array, but this time we'll use `map()`.

```js
function mapVideoTitlePairs2 (arr) {
  return arr.map(item => ({id:item.id, title:item.title}));
}
```
1. `mapVideoTitlePairs2()` takes an array `arr` and calls `map()` on it
1. For each item in `arr`, the `id` and `title` value/pairs are projected into a new array and returned. 

Pass the `newReleases` array into `mapVideoTitlePairs2()`
```js
mapVideoTitlePairs2(newReleases);
```
>
[  
  { id: 70111470, title: 'Die Hard' },  
  { id: 654356453, title: 'Bad Boys' },  
  { id: 65432445, title: 'The Chamber' },  
  { id: 675465, title: 'Fracture' }  
]
  
My version above is modified for flexibility, so it can take any collection of videos, `newReleases`, `oldReleases`, `travisFavorites`, etc.  In the exercise, the array `newReleases` was declared inside the function and it looked like this

```js
function mapVideoTitlePairs() {
  var newReleases = [
    {
      "id": 70111470,
      "title": "Die Hard",
      "boxart": "http://cdn-0.nflximg.com/images/2891/DieHard.jpg",
      "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
      "rating": [4.0],
      "bookmark": []
    },
    {
      "id": 654356453,
      "title": "Bad Boys",
      "boxart": "http://cdn-0.nflximg.com/images/2891/BadBoys.jpg",
      "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
      "rating": [5.0],
      "bookmark": [{ id:432534, time:65876586 }]
    },
    {
      "id": 65432445,
      "title": "The Chamber",
      "boxart": "http://cdn-0.nflximg.com/images/2891/TheChamber.jpg",
      "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
      "rating": [4.0],
      "bookmark": []
    },
    {
      "id": 675465,
      "title": "Fracture",
      "boxart": "http://cdn-0.nflximg.com/images/2891/Fracture.jpg",
      "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
      "rating": [5.0],
      "bookmark": [{ id:432534, time:65876586 }]
    }
  ];

  return newReleases.map(video => ({id:video.id, title:video.title}))
}
```

___
## Exercise 6
### Use forEach() to collect only those videos with a rating of 5.0
Use `forEach()` to loop the `newReleases` array and, if a video has a rating of 5.0, add it to the videos array.  

```js
(function filterWithForEach() {
  var newReleases = [
    {
      "id": 70111470,
      "title": "Die Hard",
      "boxart": "http://cdn-0.nflximg.com/images/2891/DieHard.jpg",
      "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
      "rating": 4.0,
      "bookmark": []
    },
    {
      "id": 654356453,
      "title": "Bad Boys",
      "boxart": "http://cdn-0.nflximg.com/images/2891/BadBoys.jpg",
      "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
      "rating": 5.0,
      "bookmark": [{ id:432534, time:65876586 }]
    },
    {
      "id": 65432445,
      "title": "The Chamber",
      "boxart": "http://cdn-0.nflximg.com/images/2891/TheChamber.jpg",
      "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
      "rating": 4.0,
      "bookmark": []
    },
    {
      "id": 675465,
      "title": "Fracture",
      "boxart": "http://cdn-0.nflximg.com/images/2891/Fracture.jpg",
      "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
      "rating": 5.0,
      "bookmark": [{ id:432534, time:65876586 }]
    }
  ],
  videos = [];

  newReleases.forEach( video => {
      if ( video.rating === 5.0) {
        videos.push( video);
      } } );
    return videos;
  })();
```
>
```js
[ { id: 654356453,
    title: 'Bad Boys',
    boxart: 'http://cdn-0.nflximg.com/images/2891/BadBoys.jpg',
    uri: 'http://api.netflix.com/catalog/titles/movies/70111470',
    rating: 5,
    bookmark: [ [Object] ] },
  { id: 675465,
    title: 'Fracture',
    boxart: 'http://cdn-0.nflximg.com/images/2891/Fracture.jpg',
    uri: 'http://api.netflix.com/catalog/titles/movies/70111470',
    rating: 5,
    bookmark: [ [Object] ] } ]
```
This is the interesting part. 

```js
  newReleases.forEach( video => {
      if ( video.rating === 5.0) {
        videos.push( video);
      } } );
    return videos;
```
1. Call `forEach` on the `newReleases` array 
1. loop through the collection of videos, taking each video
1. If the rating value is 5, push it into the `videos` array.
1. Return the `videos` array.

___
## Exercise 7
### Add a filter() function to the Array type
The `filter()` function accepts a predicate callback. A predicate is a function that accepts an item in the array, and returns a boolean indicating whether the item should be retained in the new array.

```js
Array.prototype.filter = function(predicateFunction) {
  var results = [];
  this.forEach(function(itemInArray)){
    if (predicateFunction(itemInArray)) {
      results.push(itemInArray);
    }
  });
    return results;
};
```
##### Array.prototype.filter
1. Declare a function on the `Array.prototype` called `filter()`
  * `filter()` takes a `predicateFunction()` argument
  * `predicateFunction()` acts as a criteria that returns a boolean
1. An empty array, `results`, is declared 
1. `forEach` loops an array, calling `predicateFunction()` on each item
1. If the item passes the test, returning `true`,  
1. It is pushed into the `results` array
1. The `results` array is returned

___
## Exercise 8
### Query Data by Chaining Method Calls
Chain filter and map to collect the ids of videos that have a rating of 5.0

```js
function mapAndFilter() {
  var newReleases = [
    {
      "id": 70111470,
      "title": "Die Hard",
      "boxart": "http://cdn-0.nflximg.com/images/2891/DieHard.jpg",
      "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
      "rating": 4.0,
      "bookmark": []
    },
    {
      "id": 654356453,
      "title": "Bad Boys",
      "boxart": "http://cdn-0.nflximg.com/images/2891/BadBoys.jpg",
      "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
      "rating": 5.0,
      "bookmark": [{ id:432534, time:65876586 }]
    },
    {
      "id": 65432445,
      "title": "The Chamber",
      "boxart": "http://cdn-0.nflximg.com/images/2891/TheChamber.jpg",
      "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
      "rating": 4.0,
      "bookmark": []
    },
    {
      "id": 675465,
      "title": "Fracture",
      "boxart": "http://cdn-0.nflximg.com/images/2891/Fracture.jpg",
      "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
      "rating": 5.0,
      "bookmark": [{ id:432534, time:65876586 }]
    }
  ];

  return newReleases.
      filter( video => video.rating === 5).map( video => video.id);
}
```
1. `filter()` returns an array of all the 5 star videos
1. which it then calls `map()` on
1. `map()` takes each video object in the array
1. and projects the id value into a new array
1. returning an array with the id's of videos with 5 star ratings

`mapAndFilter();`
>
[654356453, 675465]
___

```js
function fiveStarVids (array) {
  return array.filter( video => video.rating === 5)
              .map( video => video.id);
}
```
Pass any array of videos into `fiveStarVids()` to get the ids of all the 5 star videos in the collection. 

```js
fiveStarVids(newReleases);
```
Returns "Fracture" and "Bad Boys", the two with 5 star ratings. 
>[654356453, 675465]

How about adding a second parameter to make something more flexible. This limits us to only 5 stars.  
It might be useful to group videos by other ratings as well. 
`vidsByRating()` has a second parameter for you to plug in a rating value to return an array with all videos in a collection with that rating.

```js
function vidsByRating (array, rating) {
  return array.filter( video => video.rating === rating)
              .map( video => video.id);
}
```
Call vidsByRating on the `newReleases` collection, passing in 4 as the `rating` argument

```js
vidsByRating(newReleases, 4);
```
And we get the id's for "Die Hard" and "The Chamber", the 4 star videos. 
>[70111470, 65432445]


___
## Exercise 9
### Flatten a 2D array, `movieLists`, into an array of each videos `id` value

`movieLists` is an array with more than one collection in it— a nested collection, 2D array, or tree. For brevity, I'm good with "tree", so let's go with that. This tree here, has length of 2. Both items are objects, containing collections of their own. Each of their `videos` property holds an inner array. 

What I want to do specifically is return an array with the `id` of all 4 movies in a flat (one dimensional) array.  
Since there are no parameters at play here, I've got my code wrapped up as an IIFE. 

```js
(function() {
  var movieLists = [
    {
      name: "New Releases",
      videos: [
        {
          "id": 70111470,
          "title": "Die Hard",
          "boxart": "http://cdn-0.nflximg.com/images/2891/DieHard.jpg",
          "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
          "rating": 4.0,
          "bookmark": []
        },
        {
          "id": 654356453,
          "title": "Bad Boys",
          "boxart": "http://cdn-0.nflximg.com/images/2891/BadBoys.jpg",
          "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
          "rating": 5.0,
          "bookmark": [{ id:432534, time:65876586 }]
        }
      ]
    },
    {
      name: "Dramas",
      videos: [
        {
          "id": 65432445,
          "title": "The Chamber",
          "boxart": "http://cdn-0.nflximg.com/images/2891/TheChamber.jpg",
          "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
          "rating": 4.0,
          "bookmark": []
        },
        {
          "id": 675465,
          "title": "Fracture",
          "boxart": "http://cdn-0.nflximg.com/images/2891/Fracture.jpg",
          "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
          "rating": 5.0,
          "bookmark": [{ id:432534, time:65876586 }]
        }
      ]
    }
  ],

// query this tree above (2D array) for video id's

allVideoIdsInMovieLists = [];

  movieLists.forEach (list => {
    list.videos.forEach (video => {
      allVideoIdsInMovieLists.push(video.id);
    });
  });

  return allVideoIdsInMovieLists;

})();
```
Drop that into the console, and you'll get 
>[70111470, 654356453, 65432445, 675465]

Slow up. Let's take a closer look at that last part

```js
allVideoIdsInMovieLists = [];

  movieLists.forEach (list => {
    list.videos.forEach (video => {
      allVideoIdsInMovieLists.push(video.id);
    });
  });

  return allVideoIdsInMovieLists;
```
1. Declare `allVideoIdsInMovieLists`, an empty array
1. Call `forEach()` on the `movieLists` array. 
1. `forEach` takes a `list` item and on each item
1. Call `forEach()` which takes a `video` item 
  * Now we're two layers deep, in the `videos` inner-array
1. Push the `id` value into `allVideoIdsInMovieLists` 

>[70111470, 654356453, 65432445, 675465]

1. return `allVideoIdsInMovieLists` 


___
## Exercise 10
### Add the concatAll method to the Array prototype
`concatAll()` is a custom method that does exactly what we just did in exercise 9. It flattens 2D arrays.  
Nested collections are common. Flattening a 2D array is so useful, there ought to be method on the Array prototype for it. Unlike `map()` and `filter()`, there isn't a built-in method for flattening trees, so we should add one ourselves.  

```js
Array.prototype.concatAll = function() {
  var results = [];
  this.forEach(function(subArray) {
    subArray.forEach(function(item) {
      results.push(item);
    });
  });

  return results;
};
```
1. Declare a function on `Array.prototype` called `concatAll()`
1. In the scope of `concatAll()` declare an empty array, `results`
1. call `forEach()` on `this` - refering to the outermost array
1. which calls `forEach()` on the inner-array 
1. On the inner-array `forEach()` takes an `item`,
1. pushes that `item` into the `results` array, and
1. returns `results`


___
## Exercise 11
### Project and flatten `movieLists` into an array of video ids
`movieLists` is an array containing two collections, "New Releases" and "Dramas", each with their own separate arrays of movies. I need dig two levels deep, retrieve the `id` value of all the movies in both lists, and return them in a flattened array.  

This is done with two nested calls to `map()` and one call to `concatAll()`.

```js
(function() {
  var movieLists = [
      {
        name: "New Releases",
        videos: [
          {
            "id": 70111470,
            "title": "Die Hard",
            "boxart": "http://cdn-0.nflximg.com/images/2891/DieHard.jpg",
            "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
            "rating": 4.0,
            "bookmark": []
          },
          {
            "id": 654356453,
            "title": "Bad Boys",
            "boxart": "http://cdn-0.nflximg.com/images/2891/BadBoys.jpg",
            "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
            "rating": 5.0,
            "bookmark": [{ id:432534, time:65876586 }]
          }
        ]
      },
      {
        name: "Dramas",
        videos: [
          {
            "id": 65432445,
            "title": "The Chamber",
            "boxart": "http://cdn-0.nflximg.com/images/2891/TheChamber.jpg",
            "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
            "rating": 4.0,
            "bookmark": []
          },
          {
            "id": 675465,
            "title": "Fracture",
            "boxart": "http://cdn-0.nflximg.com/images/2891/Fracture.jpg",
            "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
            "rating": 5.0,
            "bookmark": [{ id:432534, time:65876586 }]
          }
        ]
      }
    ];

return movieLists.map( list => 
  list.videos.map( video => video.id ))
  .concatAll();
})();

```
>```js 
[70111470, 654356453, 65432445, 675465]
```

Let's look at that last bit of code and see what's going on here

```js
return movieLists.map( list => 
  list.videos.map( video => video.id ))
  .concatAll();
```
* `map()` over `movieLists` 
  - with an anonymous callback function that takes a `list` item
  - That maps over the individual movie lists
  - First `map()` is called on "New Releases", and then "Dramas"
  - For each movie in each collection, we want only the `id` value 
* Nest another `map()` expression 
  - This `map()` calls an anonymous function that takes a `video` item
  - `map()` over all the videos in each movie list 
  - and returns the `id` of each video. 
* At this point I have a 2 dimensional array
  - For each movie list, we returned a transformed array
  - `map()` always returns an array 
  - What we have looks like this

>```js
[ [70111470, 654356453], [65432445, 675465] ]
```

* Finally, chain `concatAll()` onto this 2D array to flatten it 

>```js
[ 70111470, 654356453, 65432445, 675465 ]
```

#### footNotes
* `concatAll()` only works on 2D arrays. It **doesn't** work on objects containing arrays. 
* use `map()` to transform an object to an array *(with what you want in it)*
* If `movielists` were not divided into the two named genre objects, meaning if it were an array of arrays, we could flatten it with `concatAll()` first and then use `map()` to project the `id` values onto an array, returning the same result. 

___
## Exercise 12
### Query a 3 dimensional array
This tree just got a bit raunchier. Now every movie in `movieLists` has an array containing objects of varying box art sizes.  

Retrieve `id`, `title`, and a 150x200 boxart `url` for every video.  Here, we'll use `map()`, `filter()` and `concatAll()`.  

```js
(function() {
  var movieLists = [
      {
        name: "Instant Queue",
        videos : [
          {
            "id": 70111470,
            "title": "Die Hard",
            "boxarts": [
              { width: 150, height:200, url:"http://cdn-0.nflximg.com/images/2891/DieHard150.jpg" },
              { width: 200, height:200, url:"http://cdn-0.nflximg.com/images/2891/DieHard200.jpg" }
            ],
            "url": "http://api.netflix.com/catalog/titles/movies/70111470",
            "rating": 4.0,
            "bookmark": []
          },
          {
            "id": 654356453,
            "title": "Bad Boys",
            "boxarts": [
              { width: 200, height:200, url:"http://cdn-0.nflximg.com/images/2891/BadBoys200.jpg" },
              { width: 150, height:200, url:"http://cdn-0.nflximg.com/images/2891/BadBoys150.jpg" }

            ],
            "url": "http://api.netflix.com/catalog/titles/movies/70111470",
            "rating": 5.0,
            "bookmark": [{ id:432534, time:65876586 }]
          }
        ]
      },
      {
        name: "New Releases",
        videos: [
          {
            "id": 65432445,
            "title": "The Chamber",
            "boxarts": [
              { width: 150, height:200, url:"http://cdn-0.nflximg.com/images/2891/TheChamber150.jpg" },
              { width: 200, height:200, url:"http://cdn-0.nflximg.com/images/2891/TheChamber200.jpg" }
            ],
            "url": "http://api.netflix.com/catalog/titles/movies/70111470",
            "rating": 4.0,
            "bookmark": []
          },
          {
            "id": 675465,
            "title": "Fracture",
            "boxarts": [
              { width: 200, height:200, url:"http://cdn-0.nflximg.com/images/2891/Fracture200.jpg" },
              { width: 150, height:200, url:"http://cdn-0.nflximg.com/images/2891/Fracture150.jpg" },
              { width: 300, height:200, url:"http://cdn-0.nflximg.com/images/2891/Fracture300.jpg" }
            ],
            "url": "http://api.netflix.com/catalog/titles/movies/70111470",
            "rating": 5.0,
            "bookmark": [{ id:432534, time:65876586 }]
          }
        ]
      }
    ];

  return movieLists.map( movieList =>
    movieList.videos.map( video =>
      video.boxarts.filter( boxart =>
        boxart.width === 150 && boxart.height === 200).map( boxart => 
          ({ id:video.id, title:video.title, boxart:boxart.url }) 
  ))) 
    .concatAll()
      .concatAll();

})();
```

>```js
[ { 
      boxart: "http://cdn-0.nflximg.com/images/2891/DieHard150.jpg"
      id: 70111470
      title: "Die Hard" 
    }, 
  { 
      boxart: "http://cdn-0.nflximg.com/images/2891/BadBoys150.jpg"
      id: 654356453
      title: "Bad Boys" 
    },
  { 
      boxart: "http://cdn-0.nflximg.com/images/2891/TheChamber150.jpg"
      id: 65432445
      title: "The Chamber" 
    },
  { 
      boxart: "http://cdn-0.nflximg.com/images/2891/Fracture150.jpg"
      id: 675465
      title: "Fracture" 
    }
]
```
Three layers deep, get what we want, and return a flat array.  

## Break it Down
```js
  return movieLists.map( movieList =>
    movieList.videos.map( video =>
      video.boxarts.filter( boxart =>
        boxart.width === 150 && boxart.height === 200).map( boxart => 
          ({ id:video.id, title:video.title, boxart:boxart.url }) 
  ))) 
    .concatAll()
      .concatAll();
```

* `map()` over `movieList`
  - mapping through each `list`, return the `videos` inner-array and
* `map()` over each `video` item, passing in a call to
* `filter()` the `boxarts` array. 
  - if the `width` is 150 and the `height` is 200
    + `map()` over the `boxarts` array (_now on the third level_)
* Reurn an object 
  - with the `id`, and `title` from the `video` array, and 
  - the `url` from the `boxarts` array
  - At this point, we have a 3 dimensional array. An array of two arrays
    + inside if which are 2 inner-arrays
    + each 1 item long, holding a single video object

>```js
[ [[{...}],[{...}]], [[{...}],[{...}]] ]
```

* `concatAll()` to flatten it out

>```js
[ [{...}],[{...}],[{...}],[{...}] ]
```

* That only flattens it from a 3D array to a 2D array
* `concatAll()` again
* And get exactly what we want

>```js
[ {...},{...},{...},{...} ]
```

As we see, `concatAll()` only flattens one level of nesting. Since `map()` was called 3 times, we must `concatAll()` twice. `concatAll()` can take us from a 2D to 1D, or from 3D to 2D and so on.


___
## Exercise 13
### Implement `concatMap()`
This is just a convenience function that flattens multi-dimensional arrays.  Usually when we use `map()` on nested collections we will want to flatten out the returned array. 

```js
Array.prototype.concatMap = function(projectionFunctionThatReturnsArray) {
  return this.
    map(function(item) {
    return projectionFunctionThatReturnsArray(item);
    }).
    concatAll();
};
```
* Declare a function on the Array protype called `concatMap()`
* `concatMap()` takes a predicate function that expects to return an array
* Just a `map()` followed by `concatAll()`


___
## Exercise 14
### Query a 3D tree with `concatMap()`
Use `concatMap()` to retrieve `id`, `title`, and 150x200 box art `url` for every video

He're we're doing the same thing we did before, excpet with a little less code, since we've abstracted projection and flattening into one function.

```js
(function() {
  var movieLists = [
      {
        name: "Instant Queue",
        videos : [
          {
            "id": 70111470,
            "title": "Die Hard",
            "boxarts": [
              { width: 150, height:200, url:"http://cdn-0.nflximg.com/images/2891/DieHard150.jpg" },
              { width: 200, height:200, url:"http://cdn-0.nflximg.com/images/2891/DieHard200.jpg" }
            ],
            "url": "http://api.netflix.com/catalog/titles/movies/70111470",
            "rating": 4.0,
            "bookmark": []
          },
          {
            "id": 654356453,
            "title": "Bad Boys",
            "boxarts": [
              { width: 200, height:200, url:"http://cdn-0.nflximg.com/images/2891/BadBoys200.jpg" },
              { width: 150, height:200, url:"http://cdn-0.nflximg.com/images/2891/BadBoys150.jpg" }

            ],
            "url": "http://api.netflix.com/catalog/titles/movies/70111470",
            "rating": 5.0,
            "bookmark": [{ id:432534, time:65876586 }]
          }
        ]
      },
      {
        name: "New Releases",
        videos: [
          {
            "id": 65432445,
            "title": "The Chamber",
            "boxarts": [
              { width: 150, height:200, url:"http://cdn-0.nflximg.com/images/2891/TheChamber150.jpg" },
              { width: 200, height:200, url:"http://cdn-0.nflximg.com/images/2891/TheChamber200.jpg" }
            ],
            "url": "http://api.netflix.com/catalog/titles/movies/70111470",
            "rating": 4.0,
            "bookmark": []
          },
          {
            "id": 675465,
            "title": "Fracture",
            "boxarts": [
              { width: 200, height:200, url:"http://cdn-0.nflximg.com/images/2891/Fracture200.jpg" },
              { width: 150, height:200, url:"http://cdn-0.nflximg.com/images/2891/Fracture150.jpg" },
              { width: 300, height:200, url:"http://cdn-0.nflximg.com/images/2891/Fracture300.jpg" }
            ],
            "url": "http://api.netflix.com/catalog/titles/movies/70111470",
            "rating": 5.0,
            "bookmark": [{ id:432534, time:65876586 }]
          }
        ]
      }
    ];
  return movieLists.
    concatMap(movieList =>
      movieList.videos.concatMap( video =>
        video.boxarts. filter( boxart =>
          boxart.width === 150 && boxart.height === 200).map( boxart => 
            ({
              id:video.id,
              title:video.title,
              boxart:boxart.url
            }) 
    ) ) );
})();
```
Let's have a look at that. I think this is the tastiest bit of code so far. 
## Break it Down

* Call `map()` on the `movieLists` array, mapping over each `list`
* Then call `map()` over the `videos` array, mapping over each `video`
* This time we flatten as we go
  - `concatMap()` each `list`
  - `concatMap()` each `video`
  - `filter()` to find the right boxart `url`
  - `map()` to project the `title`, `id` and `url` into an array

```js
return movieLists.
    concatMap(movieList =>
      movieList.videos.concatMap( video =>
        video.boxarts. filter( boxart =>
          boxart.width === 150 && boxart.height === 200).map( boxart => 
            ({
              id:video.id,
              title:video.title,
              boxart:boxart.url
            }) 
    ) ) );
```
Nice. And as expected, this returns a one dimensional array with just what we want. 
>```js
[ { 
      boxart: "http://cdn-0.nflximg.com/images/2891/DieHard150.jpg"
      id: 70111470
      title: "Die Hard" 
    }, 
  { 
      boxart: "http://cdn-0.nflximg.com/images/2891/BadBoys150.jpg"
      id: 654356453
      title: "Bad Boys" 
    },
  { 
      boxart: "http://cdn-0.nflximg.com/images/2891/TheChamber150.jpg"
      id: 65432445
      title: "The Chamber" 
    },
  { 
      boxart: "http://cdn-0.nflximg.com/images/2891/Fracture150.jpg"
      id: 675465
      title: "Fracture" 
    }
]
```

___
## Exercise 15
### Use forEach to find the largest box art
Here, I'm using `forEach()` to show how you might go through a collection, comparing one item to another.

```js
function bigBox() {
  var boxarts = [
      { width: 200, height:200, url:"http://cdn-0.nflximg.com/images/2891/Fracture200.jpg" },
      { width: 150, height:200, url:"http://cdn-0.nflximg.com/images/2891/Fracture150.jpg" },
      { width: 300, height:200, url:"http://cdn-0.nflximg.com/images/2891/Fracture300.jpg" },
      { width: 425, height:150, url:"http://cdn-0.nflximg.com/images/2891/Fracture425.jpg" }
    ],
    currentSize,
    maxSize = -1,
    largestBoxart;

    boxarts.forEach( boxart => {
      currentSize = boxart.width * boxart.height;
      if (currentSize > maxSize) {
        largestBoxart = boxart;
        maxSize = currentSize;
      } 
    });
    return largestBoxart;
  }
```

> {
  width: 425, 
  height: 150, 
  url: "http://cdn-0.nflximg.com/images/2891/Fracture425.jpg"
}

#### Break it Down

* Declare Variables
  - `boxarts` - an array of box art items of varying sizes
  - `currentSize` - an undefined variable
    + holds the current item in the array, comparing to `maxSize`
  - `maxSize` - a number, initialized to -1
    + holds the previous item, until replaced by larger value
  - `largestBoxart` - an undefined variable
    + will hold the `boxart` object of the current largest 

```js
    boxarts.forEach( boxart => {
      currentSize = boxart.width * boxart.height;
      if (currentSize > maxSize) {
        largestBoxart = boxart;
        maxSize = currentSize;
      } 
    });
    return largestBoxart;
```

* `forEach()` over `boxarts`, taking each `boxart` item and
  - multiply width times height and assign value to `currentSize`
  - also assign that value to `maxSize` 
  - assign the current `boxart` object to `largestBoxart`
  - Contine this process for each item, effectively replacing all values whenever a larger item is found
* Return `largestBoxart` as it holds the largest item in the collection

___
## Exercise 16
### Implement `reduce()` 
`reduce()` is for when you need to look at at least two values at the same time to do your job.   

Add the `reduce()` function to the Array prototype. This version differs from the `reduce()` built into JavaScript in that it returns the value inside an array. For example `[5]` instead of `5`.  
This makes it easy to continue chaining method calls. It also returns an empty array rather than an error if you attempt to reduce over an empty array.  

It also helps with asyncronous programming because you cant return a single value from an observable, as this would require you to block.  



```js
Array.prototype.reduce = function(combiner, initialValue) {
  var counter, accumulatedValue;
  if (this.length === 0) {
    return this;
  }
  else {
    if (arguments.length === 1) {
      counter = 1;
      accumulatedValue = this[0];
      else if {
        (arguments.length >= 2) {
          counter = 0;
          accumulatedValue = initialValue;
      } 
      else {
          throw "Invalid arguments.";
        }
  while (counter < this.length) {
    accumulatedValue = combiner(accumulatedValue, this[counter] )
    counter++;
  }
  return [accumulatedValue];
      }
    }
  }
}
```

* If the array is empty, do nothing
* If the user didn't pass an initial value, use the first item.
* If there are two arguments (the first is `combiner` and second is `initalValue`)
  - set `counter` to 0, and
  - set `accumulatedValue` to the value of the the `initialValue`
* The first argument `combiner` is a function that takes in the `accumulated value`  and the current item in the array. 
* Loop through the array, feeding the current value and the result of the previous computation back into the `combiner` function until  we've exhausted the entire array and are left with only one item.
* Return the final `accumulatedValue` inside an array (one item long)

___
## Exercise 17
### Retrieve the Largest Rating
Let's use our new reduce function to isolate the largest value in an array of ratings.

```js
function LargestRating() {
  var ratings = [2,3,1,4,5];
  return ratings.reduce((acc, curr) => {
    if (acc > curr) {
      return acc
    }
    else {
      return curr;
    } 
    });
}
```

* Declare variable `ratings`, an array 5 items long, each holding a number
* call `reduce()` on `ratings` passing in an anonymous callback (combiner function)
  - No initial value, so we start at the beginning and loop all the way through
  - Pass two arguments into combiner, `acc` and `curr` for accumulated and current value
* Loop through `ratings` and on each item
  - if the item is larger than the one before, return the larger item
  - on the final return, you've got the largest item in an array

> [5]

___
## Exercise 18
### Retrieve url of the largest boxart (with `reduce()`)

Let's try combining `reduce()` with `map()` to reduce multiple boxart objects to a single value: the url of the largest box art.

```js
function box() {
  var boxarts = [
      { width: 200, height:200, url:"http://cdn-0.nflximg.com/images/2891/Fracture200.jpg" },
      { width: 150, height:200, url:"http://cdn-0.nflximg.com/images/2891/Fracture150.jpg" },
      { width: 300, height:200, url:"http://cdn-0.nflximg.com/images/2891/Fracture300.jpg" },
      { width: 425, height:150, url:"http://cdn-0.nflximg.com/images/2891/Fracture425.jpg" }
    ];
    
    return boxarts.reduce(( acc, curr) => 
      (( acc.width * acc.height > curr.width * curr.height) ? acc : curr ))
        .map( boxart => boxart.url );
}

```

#### Break it Down

* `reduce()` the boxarts array passing in a combiner callback 
  - the callback takes two arguments
    + `acc` - the accumulated value, and 
    + `curr` - the current value
  - On each item, if the box is bigger than the current biggest box return `curr`
* `map()` over the boxart object and project the `url` value into a new array. 

>```js
box();
--> ["http://cdn-0.nflximg.com/images/2891/Fracture425.jpg"]
```


___
## Exercise 19
### Reducing with an initial value
Sometimes when we reduce an array, we want the reduced value to be a different type than the items stored in the array. Let's say we have an array of videos and we want to reduce them to a single map where the key is the video id and the value is the video's title.

This function takes an array, `videos` 

```js
var videos = [
    {
      "id": 65432445,
      "title": "The Chamber"
    },
    {
      "id": 675465,
      "title": "Fracture"
    },
    {
      "id": 70111470,
      "title": "Die Hard"
    },
    {
      "id": 654356453,
      "title": "Bad Boys"
    }
  ];
```

and returns an accumulated map 

>```js
 [
     {
         "65432445": "The Chamber",
         "675465": "Fracture",
         "70111470": "Die Hard",
         "654356453": "Bad Boys"
     }
 ]
```

Use an empty map as the initial value instead of the first item in the list.
Object.create() makes a fast copy of the accumulatedMap by creating a new object and setting the eacumulatedMap to be the new object's prototype.   

>**"empty map"** = {}

Initially the new object is empty and has no members of its own except a pointer to the object on which it was based. If an attempt to find a member on the new object fails, the new object silently attempts to find the member on its prototype. This process continues recursively, with each object checking its prototype until the member is found or we reach the first object we created.  

If we set a member value on the new object, it is stored directly on that object, leaving the prototype unchanged.  

Object.create() is perfect for functional programming because it makes creating a new object with a different member value almost as cheap as changing the member on the original object. 

```js
function() {
  var videos = [
    {
      "id": 65432445,
      "title": "The Chamber"
    },
    {
      "id": 675465,
      "title": "Fracture"
    },
    {
      "id": 70111470,
      "title": "Die Hard"
    },
    {
      "id": 654356453,
      "title": "Bad Boys"
    }
  ];

  return videos.reduce( (accumulatedMap, video)  => {

    var copyOfAccumulatedMap = Object.create(accumulatedMap);

    copyOfAccumulatedMap[ video.id] = video.title;

    return copyOfAccumulatedMap;
    }, {} 
  );
}

```
#### Break it Down

All we're doing here is calling `reduce()` on the `videos` array. 
Like this: 

```js
videos.reduce ( callback, initalValue )
```
**callback** is an anonymous reduction function taking an accumulated value and current value, `accumulatedMap` and `video`, makes an object and assigns the `accumulatedMap` to the prototype, creating a copy called `copyOfAccumulatedMap` 

```js
return videos.reduce( (accumulatedMap, video)  => {
  var copyOfAccumulatedMap = Object.create(accumulatedMap);
  copyOfAccumulatedMap[ video.id] = video.title;
  return copyOfAccumulatedMap;
}
```
**initalValue** is the empty map. `reduce()` will use this instead of the first item in the array. 

```js
  ,{} );
```
### Notes
This would actually work. Without making a copy using `Object.create()`

```js
  return videos.reduce( (accumulatedMap, video)  => {
    accumulatedMap[ video.id] = video.title;
    return accumulatedMap;
    }, {} 
  );
}
)();

```
You could still get an array containing a map with video `id` and `title` value pairs.  

>```js
  [
      {
        675465: "Fracture"
        65432445: "The Chamber"
        70111470: "Die Hard"
        654356453: "Bad Boys"
      }
  ]
```

But it is important, inside of our functions, to **never changing values**
Never change a variable, ever. In this version above, we are changing a value. Allowing mutability creates a lot of complexity inside programs.   

By using prototypal inheritance, you can create a new object, that looks like a clone, but is actually a new object. 

```js
person = {name: "Jim"};
```
> Object {name: "Jim"}

```js
anotherPerson = Object.create(person);
```
> Object {}

This creates an empty object. There are no properties.
However, if I call for the name property on `anotherPerson` 

```js
anotherPerson.name;
```
I see this returns 

>"Jim"

This is because it points to the `person` prototype I just created, which has the name "Jim".  

One more time, just for fun...

```js
(function() {
  var videos = [
    {
      "id": 65432445,
      "title": "The Chamber"
    },
    {
      "id": 675465,
      "title": "Fracture"
    },
    {
      "id": 70111470,
      "title": "Die Hard"
    },
    {
      "id": 654356453,
      "title": "Bad Boys"
    }
  ];

    return videos.reduce( (acc, curr) => {
      var clone;
      clone = Object.create(acc);
      clone[curr.id] = curr.title;
    return clone;
    }, {} );

})();
```

___
## Exercise 20
### Retrieve the id, title, and smallest box art url for every video with `reduce()`
This is a variation of the problem we solved earlier, where we retrieved the url of the boxart with a width of 150px.  
This time we'll use `reduce()` instead of `filter()` to retrieve the smallest box art in the boxarts array.  

Take this 3D array, and return an array with the following

>```js
  [
       {id, title, url },
       {id, title, url },
       {id, title, url },
       {id, title, url }
   ];
```

New Releases [{},{}]
    "Die Hard"
        boxarts
    "Bad Boys"
        boxarts
Thrillers [{},{}]
    "The Chamber"
        boxarts
    "Fracture"
        boxarts

First, go from 3D to 2D  to 1D with `concatMap()`

>[ { "New Releases" }, { "Thrillers" } ];  
>[ {"Die Hard"},{"Bad Boys"},{"The Chamber"},{"Fracture"} ]





#### Pseudocode
1. `concatMap()` over `movieLists` taking `movidLists` and
1. `concatMap()` over `videos` taking `boxarts` and 
1. `reduce()` the `boxarts` array returning smallest boxart `url`
1. `map()` to project `videos.id`, `videos.title`, and `boxart.url`


```js
function smallBox() {
  var movieLists = [
    {
      name: "New Releases",
      videos: [
        {
          "id": 70111470,
          "title": "Die Hard",
          "boxarts": [
            { width: 150, height:200, url:"http://cdn-0.nflximg.com/images/2891/DieHard150.jpg" },
            { width: 200, height:200, url:"http://cdn-0.nflximg.com/images/2891/DieHard200.jpg" }
          ],
          "url": "http://api.netflix.com/catalog/titles/movies/70111470",
          "rating": 4.0,
          "bookmark": []
        },
        {
          "id": 654356453,
          "title": "Bad Boys",
          "boxarts": [
            { width: 200, height:200, url:"http://cdn-0.nflximg.com/images/2891/BadBoys200.jpg" },
            { width: 140, height:200, url:"http://cdn-0.nflximg.com/images/2891/BadBoys140.jpg" }

          ],
          "url": "http://api.netflix.com/catalog/titles/movies/70111470",
          "rating": 5.0,
          "bookmark": [{ id:432534, time:65876586 }]
        }
      ]
    },
    {
      name: "Thrillers",
      videos: [
        {
          "id": 65432445,
          "title": "The Chamber",
          "boxarts": [
            { width: 130, height:200, url:"http://cdn-0.nflximg.com/images/2891/TheChamber130.jpg" },
            { width: 200, height:200, url:"http://cdn-0.nflximg.com/images/2891/TheChamber200.jpg" }
          ],
          "url": "http://api.netflix.com/catalog/titles/movies/70111470",
          "rating": 4.0,
          "bookmark": []
        },
        {
          "id": 675465,
          "title": "Fracture",
          "boxarts": [
            { width: 200, height:200, url:"http://cdn-0.nflximg.com/images/2891/Fracture200.jpg" },
            { width: 120, height:200, url:"http://cdn-0.nflximg.com/images/2891/Fracture120.jpg" },
            { width: 300, height:200, url:"http://cdn-0.nflximg.com/images/2891/Fracture300.jpg" }
          ],
          "url": "http://api.netflix.com/catalog/titles/movies/70111470",
          "rating": 5.0,
          "bookmark": [{ id:432534, time:65876586 }]
        }
      ]
    }
  ];


return movieLists.
  concatMap( movieList => 
    movieList.videos.concatMap( video =>
      video.boxarts.
        reduce(( acc, curr) => 
          acc.width * acc.height < curr.width * curr.height ? acc : curr)
        .map( boxart => 
            ({
              id: video.id,
              title: video.title, 
              boxart: boxart.url
            })
      )))
}

```

___
# Zipping Arrays
Sometimes we need to combine two arrays by progressively taking an item from each and combining the pair. If you visualize a zipper, where each side is an array, and each tooth is an item, you'll have a good idea of how the zip operation works.  
## Exercise 21: 
### Combine videos and bookmarks by index with For Loops
Use a for loop to traverse the videos and bookmarks array at the same time. For each video and bookmark pair, create a {videoId, bookmarkId} pair and add it to the videoIdAndBookmarkIdPairs array.


```js
function() {
  var videos = [
      {
        "id": 70111470,
        "title": "Die Hard",
        "boxart": "http://cdn-0.nflximg.com/images/2891/DieHard.jpg",
        "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
        "rating": 4.0,
      },
      {
        "id": 654356453,
        "title": "Bad Boys",
        "boxart": "http://cdn-0.nflximg.com/images/2891/BadBoys.jpg",
        "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
        "rating": 5.0,
      },
      {
        "id": 65432445,
        "title": "The Chamber",
        "boxart": "http://cdn-0.nflximg.com/images/2891/TheChamber.jpg",
        "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
        "rating": 4.0,
      },
      {
        "id": 675465,
        "title": "Fracture",
        "boxart": "http://cdn-0.nflximg.com/images/2891/Fracture.jpg",
        "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
        "rating": 5.0,
      }
    ],
    bookmarks = [
      {id: 470, time: 23432},
      {id: 453, time: 234324},
      {id: 445, time: 987834}
    ],
  counter,
  videoIdAndBookmarkIdPairs = [];

  for( counter = 0; counter < Math.min( videos.length, bookmarks.length); counter++){
    videoIdAndBookmarkIdPairs.push(
      {
        videoId: videos[ counter].id, 
        bookmarkId: bookmarks[ counter].id
      })
  }
  return videoIdAndBookmarkIdPairs;
}
    
```

* Declare new variable, `videoIdAndBookmarkIdPairs`, an empty array
  - this is where the zipped objects go
* Loop over the videos array
  - set the loop boundry to the length of the shorter array 
    + `counter < Math.min(array1.length, array2.length)`
  - Push thing from array1 and thing from array2 into `videoIdAndBookmarkIdPairs`
* Return `videoIdAndBookmarkIdPairs`

___

## Implement Zip

Let's add a static `zip()` function to the Array type. The `zip()` function accepts a combiner function, traverses each array at the same time, and calls the combiner function on the current item on the left-hand-side and right-hand-side. The `zip()` function requires an item from each array in order to call the combiner function, therefore the array returned by `zip()` will only be as large as the smallest input array.

```js
Array.zip = function(left, right, combinerFunction){
  var counter, results = [];
  
  for( counter = 0; counter < Math.min( left.length, right.length ); counter++){
    results.push( combinerFunction( left[ counter], right[ counter] ));
  }
  return results;
};
```

The combiner function takes a left array, and a right array and the two are always coordinated by the counter

___
## Implement Zip
Let's add a static `zip()` function to the Array type. The `zip()` function accepts a combiner function, traverses each array at the same time, and calls the combiner function on the current item on the left-hand-side and right-hand-side. The `zip()` function requires an item from each array in order to call the combiner function, therefore the array returned by `zip()` will only be as large as the smallest input array.

```js
Array.zip = function(left, right, combinerFunction){
  var counter, results = [];
  
  for( counter = 0; counter < Math.min( left.length, right.length ); counter++){
    results.push( combinerFunction( left[ counter], right[ counter] ));
  }
  return results;
};
```
The combiner function takes a left array, and a right array and the two are always coordinated by the counter

___
## Exercise 23 
### Combine videos and bookmarks by index with `zip()`
Let's repeat exercise 21, but this time lets use your new zip() function. For each video and bookmark pair, create a {videoId, bookmarkId} pair.

```js
function() {
  var videos = [
      {
        "id": 70111470,
        "title": "Die Hard",
        "boxart": "http://cdn-0.nflximg.com/images/2891/DieHard.jpg",
        "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
        "rating": 4.0,
      },
      {
        "id": 654356453,
        "title": "Bad Boys",
        "boxart": "http://cdn-0.nflximg.com/images/2891/BadBoys.jpg",
        "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
        "rating": 5.0,
      },
      {
        "id": 65432445,
        "title": "The Chamber",
        "boxart": "http://cdn-0.nflximg.com/images/2891/TheChamber.jpg",
        "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
        "rating": 4.0,
      },
      {
        "id": 675465,
        "title": "Fracture",
        "boxart": "http://cdn-0.nflximg.com/images/2891/Fracture.jpg",
        "uri": "http://api.netflix.com/catalog/titles/movies/70111470",
        "rating": 5.0,
      }
    ],
    bookmarks = [
      {id: 470, time: 23432},
      {id: 453, time: 234324},
      {id: 445, time: 987834}
    ];
 
    return Array.zip( videos, bookmarks, ( video, bookmark ) =>
      ({ videoId : video.id, bookmarkId : bookmark.id }));
}
```
### Break it Down
I've got two arrays that need to be zipped up. 3 of the 4 videos have corresponding bookmarks. 
Rather than chaining `zip()`, we tell it which two arrays to work with, giving it a left and a right array. 
* Return Array.zip and pass in the left array, right array, and combiner function
  - The left array is videos
  - The right array is bookmarks
  - The combiner is an anonymous function that returns an object with the desired item from each array

___
## Exercise 24: 
### Retrieve each video's id, title, middle moment time, and smallest box art url.
This is a variation of the problem we solved earlier. This time each video has an interesting moments collection, each representing a time during which a screenshot is interesting or representative of the title as a whole. Notice that both the boxarts and interestingMoments arrays are located at the same depth in the tree. Retrieve the time of the middle interesting moment and the smallest box art url simultaneously with zip().  

Return an {id, title, time, url} object for each video.

videos.id
videos.title
videos.boxarts.url
videos.interestingMoments


* `concatMap()` over `movieLists` (movieList)
* `concatMap()` over `videos` (video)
* `zip()` boxarts and interestingMoments arrays 
  - `reduce()` over `boxarts` (boxart) foer smallest
  - `filter()` over `interestingMoments` (type === "Middle")
  - combiner function that puts all the pieces together


```js
 return movieLists.
   concatMap( movieList => 
     movieList.videos.
       concatMap( video => 

         Array.zip( 
           video.boxarts.reduce( ( acc, curr) =>
             (acc.width*acc.height < curr.width*curr.height) ? acc : curr ), 
               video.interestingMoments.filter( interestingMoment =>
                 interestingMoment.type === "Middle" ), 
                   ( boxart, interestingMoment ) => 
                      ({id: video.id, title: video.title, time: interestingMoment.time, url: boxart.url })
        )
    )
  );

```
___









