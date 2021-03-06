# <img src="https://cloud.githubusercontent.com/assets/7833470/10899314/63829980-8188-11e5-8cdd-4ded5bcb6e36.png" height="60"> CRUD Server Routes: Create & Read

| Objectives |
| :--- |
| Implement Express routes to CREATE and READ data |
| Write request specs to test our CREATE and READ routes |

## Steps to Create

1. <details>
    <summary>Create a server route to handle the `POST` request.</summary>
    ```js
    app.post('/api/todos', function (req, res) {

    });
    ```
</details>

2. <details>
    <summary>Create a new todo with form data</summary>
    ```js
    app.post('/api/todos', function (req, res) {
      var newTodo = req.body;
    });
    ```
</details>

3. <details>
    <summary>Set a sequential id to the todo</summary>
    ```js
    app.post('/api/todos', function (req, res) {
      var newTodo = req.body;

      if (todos.length > 0) {
        newTodo._id = todos[todos.length - 1]._id + 1;
      } else {
        newTodo._id = 1;
      }
    });
    ```
</details>

4. <details>
    <summary>Add new todo to the `todos` array</summary>
    ```js
    app.post('/api/todos', function (req, res) {
      var newTodo = req.body;

      if (todos.length > 0) {
        newTodo._id = todos[todos.length - 1]._id + 1;
      } else {
        newTodo._id = 1;
      }

      todos.push(newTodo);
    });
    ```
</details>

5. <details>
    <summary>Send new todo as JSON response</summary>
    ```js

    app.post('/api/todos', function (req, res) {
    // create new todo with form data (`req.body`)
      var newTodo = req.body;

    // set sequential id (last id in `todos` array + 1)
      if (todos.length > 0) {
        newTodo._id = todos[todos.length - 1]._id + 1;
      } else {
        newTodo._id = 1;
      }

    // add newTodo to `todos` array
      todos.push(newTodo);

    // send newTodo as JSON response
      res.json(newTodo);
    });
    ```
</details>

## Steps to Read

1. <details>
    <summary>Create a server route to handle the `GET` request.</summary>
    ```js
    app.get('/api/todos/:id', function (req, res) {

    });
    ```
</details>

2. <details>
    <summary>Get the todo id from the URL params and save it to a variable.</summary>
    ```js
    app.get('/api/todos/:id', function (req, res) {
      var todoId = parseInt(req.params.id);
    });
    ```
</details>

3. <details>
    <summary>Use the id to find the todo we want to read.</summary>
    ```js
    app.get('/api/todos/:id', function (req, res) {
      var todoId = parseInt(req.params.id);

      var foundTodo = todos.filter(function (todo) {
        return todo._id == todoId;
      })[0];
    });
    ```
</details>

4. <details>
    <summary>Respond with the selected todo.</summary>
    ```js
    // get one todo
    app.get('/api/todos/:id', function (req, res) {

       // get todo id from url params (`req.params`)
       var todoId = parseInt(req.params.id);

       // find todo to by its id
       var foundTodo = todos.filter(function (todo) {
       return todo._id == todoId;
       })[0];

     // send foundTodo as JSON response
     res.json(foundTodo);
    });
    ```
</details>

## Testing Create & Read

#### Example Request Spec: Create

```js

var request = require('request'),
    expect = require('chai').expect,
    baseUrl = 'http://localhost:3000';

it('should post a single blob', function(done) {
  request.post(
    {
      url: baseUrl + '/blobs',
      form: {
        name: 'WDI 24',
        location: 'SF'
      }
    },
    function(error, response, body) {
        expect(response.statusCode).to.equal(200);
        done();
    }
  );
});
```

#### Example Request Spec: Read

```js
var request = require('request'),
    expect = require('chai').expect,
    baseUrl = 'http://localhost:3000';

// testing for all blobs
it('should return statusCode 200', function(done) {
  request(baseUrl + '/blobs', function(error, response, body) {
    expect(response.statusCode).to.equal(200);
    done();
  });
});

// testing for a single blob
it('should return statusCode 200', function(done) {
    request(baseUrl + '/blobs/:id', function(error, response, body) {
      expect(response.statusCode).to.equal(200);
      done();
    });
});
```

#### Testing Resources

* <a href="http://mherman.org/blog/2015/09/10/testing-node-js-with-mocha-and-chai/#.Vjyor66rSRs" target="_blank">Testing Node.js with Mocha and Chai</a> - Note the syntax of the tests in this article is a little different than what we're using. This is because they're using `chai-http` instead of `request` and `chai.should` instead of `chai.expect`. There are many different ways of putting together testing frameworks to build a testing stack, but no matter the stack, the logic behind the tests translates.
* <a href="http://mochajs.org" target="_blank">Mocha</a> - framework for running tests
* <a href="http://chaijs.com/api" target="_blank">Chai</a> **(expect)** - for *expect* assertions
* <a href="https://github.com/request/request" target="_blank">Request</a> - for handling HTTP requests and responses

## Challenges

1. Begin working on your <a href="https://github.com/sf-wdi-24/express-todo-app" target="_blank">express-todo-app</a>.
2. When you're ready, use the steps above to implement routes for creating and reading todos.
3. Make sure your routes work by using Postman.
4. Write request specs to test your create and read routes.

## Resources

* <a href="http://expressjs.com/api.html#req" target="_blank">Express Request Docs</a>
* <a href="http://expressjs.com/api.html#app.get" target="_blank">Express app.get()</a>
* <a href="http://expressjs.com/api.html#app.post.method" target="_blank">Express app.post()</a>
