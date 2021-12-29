# What I Learned

- `npm i --save-dev` saves dependencies in development environment only that will not be included in production.

- `app.use(express.json())` - This is a built-in middleware function in Express. It parses incoming requests with JSON payloads and is based on body-parser. Returns middleware that only parses json and only looks at requests where the Content-Type header matches the type option.

- The return statement stops the execution of a function and returns a value from that function. (https://www.w3schools.com/jsref/jsref_return.asp)
```JS
async function getSubscriber (req, res, next) {
    let subscriber

    try {
        subscriber = await Subscriber.findById(req.params.id)
        if (subscriber == null) {
            return res.status(404).json({ message: 'Cannot find subscriber' })
        }
    } catch (error) {
        return res.status(500).json({ message: error.message })
    }

    res.subscriber = subscriber
    next()
}
```

- Middleware functions are functions that have access to the request object (req), the response object (res), and the next function in the application’s request-response cycle. The next function is a function in the Express router which, when invoked, executes the middleware succeeding the current middleware.
(https://expressjs.com/en/guide/writing-middleware.html)
```JS
// Getting one
router.get('/:id', getSubscriber, (req, res) => {
    res.json(res.subscriber)
})

// Middleware
async function getSubscriber (req, res, next) {
    let subscriber

    try {
        subscriber = await Subscriber.findById(req.params.id)
        if (subscriber == null) {
            return res.status(404).json({ message: 'Cannot find subscriber' })
        }
    } catch (error) {
        return res.status(500).json({ message: error.message })
    }

    res.subscriber = subscriber
    next()
}
```

- The `Element.remove()` method removes the element from the tree it belongs to. (https://developer.mozilla.org/en-US/docs/Web/API/Element/remove)
```JS
// Deleting one
router.delete('/:id', getSubscriber, async (req, res) => {
    try {
        await res.subscriber.remove() // res.subscriber is from getSubscriber
        res.json({ message: ' Deleted Subscriber' })
    } catch (error) {
        res.status(500).json({ message: error.message })
    }
})
```

- Value vs Reference (https://www.youtube.com/watch?v=-hBJz2PPIVE; https://www.geeksforgeeks.org/pass-by-value-and-pass-by-reference-in-javascript/)

> Pass by value is for primitive data types such as number, boolean, string, null, and undefined.

> Pass by reference is for non-primitive data types such as arrays, objects, strings, and classes. The value is stored in a location or reference/address.

- When do I use path params vs. query params in a RESTful API? (https://stackoverflow.com/questions/30967822/when-do-i-use-path-params-vs-query-params-in-a-restful-api)

> Best practice for RESTful API design is that path params are used to identify a specific resource or resources, while query parameters are used to sort/filter those resources.

> Here's an example. Suppose you are implementing RESTful API endpoints for an entity called Car. You would structure your endpoints like this:
```
GET /cars
GET /cars/:id
POST /cars
PUT /cars/:id
DELETE /cars/:id
```

> This way you are only using path parameters when you are specifying which resource to fetch, but this does not sort/filter the resources in any way.

> Now suppose you wanted to add the capability to filter the cars by color in your GET requests. Because color is not a resource (it is a property of a resource), you could add a query parameter that does this. You would add that query parameter to your GET /cars request like this:
```
GET /cars?color=blue
```
> This endpoint would be implemented so that only blue cars would be returned.

> As far as syntax is concerned, your URL names should be all lowercase. If you have an entity name that is generally two words in English, you would use a hyphen to separate the words, not camel case.

Ex. `/two-words`
