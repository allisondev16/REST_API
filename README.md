#What I Learned
- `npm i --save-dev` saves dependencies in development environment only that will not be included in production.

- `app.use(express.json())` - This is a built-in middleware function in Express. It parses incoming requests with JSON payloads and is based on body-parser. Returns middleware that only parses json and only looks at requests where the Content-Type header matches the type option.