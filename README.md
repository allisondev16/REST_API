#What I Learned
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

- custom middleware

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

- Value vs Reference (https://www.youtube.com/watch?v=-hBJz2PPIVE)
-- Pass by value is for primitive data types such as number, boolean, string, null, and undefined.
-- Pass by reference is for non-primitive data types such as arrays, objects, strings, and classes. The value is stored in a location or a memory in a computer.
