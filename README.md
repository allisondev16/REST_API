#What I Learned
- `npm i --save-dev` saves dependencies in development environment only that will not be included in production.

- `app.use(express.json())` - This is a built-in middleware function in Express. It parses incoming requests with JSON payloads and is based on body-parser. Returns middleware that only parses json and only looks at requests where the Content-Type header matches the type option.

- return in function stops there

- next paramater in a function

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