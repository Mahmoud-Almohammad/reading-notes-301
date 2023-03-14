# Refactoring Javascript for Readability

## Scenario

We're an URL-shortening website, like TinyURL. We accept a long URL and return a short URL that forwards visitors to the long URL. We have two functions.

    // Unrefactored code

    const URLstore = [];

    function makeShort(URL) {
    const rndName = Math.random().toString(36).substring(2);
    URLstore.push({[rndName]: URL});
    return rndName;
    }

    function getLong(shortURL) {
    for (let i = 0; i < URLstore.length; i++) {
        if (URLstore[i].hasOwnProperty(shortURL) !== false) {
        return URLstore[i][shortURL];
        }
    }
    }

Problem: what happens if `getLong` is called with a short URL that isn't in the store? Nothing is explicitly returned so `undefined` will be returned. Since we're not sure how we're going to handle that, let's be explicit and throw an error so that problems can be spotted during development.

Performance-wise, be careful if you're iterating through a flat array very often, especially if it's a core piece of your program. The refactor here is to change the data-structure of `URLstore`.

Currently, each URL object is stored in an array. We'll visualize this as a row of buckets. When we want to convert short to long, on average we need to check half of those buckets before we find the correct short URL. What if we have thousands of buckets, and we perform this hundreds of times a second?

The answer is to use some form of **hash function**. A hash function is used to map a given key to a location in the hash table. Below, this happens when we place our short URL into the store in `makeShort` and when we get it back out in getLong. Depending on how you're measuring run time, the result is that on average we only need to check one bucket — no matter how many total buckets there are!

    // Refactored code

    const URLstore = new Map(); // Change this to a Map

    function makeShort(URL) {
    const rndName = Math.random().toString(36).substring(2);
    // Place the short URL into the Map as the key with the long URL as the value
    URLstore.set(rndName, URL);
    return rndName;
    }

    function getLong(shortURL) {
    // Leave the function early to avoid an unnecessary else statement
    if (URLstore.has(shortURL) === false) {
        throw 'Not in URLstore!';
    }
    return URLstore.get(shortURL); // Get the long URL out of the Map
    }

## To read the full article, click [here][1].

[1]: <https://dev.to/healeycodes/refactoring-javascript-for-performance-and-readability-with-examples-1hec>
