# Functional Programming, Asynchronous Programming, learnRx 
This repository is for my notes and solutions as I work through the [*learnRx*](http://reactivex.io/learnrx/) exercises, along with Jafar Husain's course on [Frontend Masters](frontendmasters.com/) "Asynchronous Programming in JavaScript".

## Exercise 1: 
### Print all names in array to console
`names` is an array with 5 names in it.  
`printWithForLoop()` takes an array, and loops over it and prints every item to the console. 

```js
var names = ["Ben", "Jafar", "Matt", "Priya", "Brian"];

function printWithForLoop(arr) {
    for (var i = 0; i < arr.length; i++) {
      console.log(arr[i]);
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
## Exercise 9
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


___
