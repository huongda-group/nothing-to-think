
# Nothing to think
===============================
Light Node.js ORM for RethinkDB.
We welcome pull requests, bug reports, ideas, and feedbacks.

### Quick start

Install:

```
npm install @huongda-group/nothing-to-think
```

Use:

```javascript
var NothingToThing = require('@huongda-group/nothing-to-think')();
var type   = NothingToThing.type;

// Create a model - the table is automatically created
var Post = NothingToThing.createModel("Post", {
  id: String,
  title: String,
  content: String,
  idAuthor: String
});

// You can also add constraints on the schema
var Author = NothingToThing.createModel("Author", {
  id: type.string(),      // a normal string
  name: type.string().min(2),  // a string of at least two characters
  email: type.string().email()  // a string that is a valid email
});

// Join the models
Post.belongsTo(Author, "author", "idAuthor", "id");
```

Save a new post with its author.

```js
// Create a new post
var post = new Post({
  title: "Hello World!",
  content: "This is an example."
});

// Create a new author
var author = new Author({
  name: "Michel",
  email: "orphee@gmail.com"
});

// Join the documents
post.author = author;


post.saveAll().then(function(result) {
  /*
  post = result = {
    id: "0e4a6f6f-cc0c-4aa5-951a-fcfc480dd05a",
    title: "Hello World!",
    content: "This is an example.",
    idAuthor: "3851d8b4-5358-43f2-ba23-f4d481358901",
    author: {
      id: "3851d8b4-5358-43f2-ba23-f4d481358901",
      name: "Michel",
      email: "orphee@gmail.com"
    }
  }
  */
});
```

Retrieve the post with its author.

```js
Post.get("0e4a6f6f-cc0c-4aa5-951a-fcfc480dd05a").getJoin().run().then(function(result) {
  /*
  result = {
    id: "0e4a6f6f-cc0c-4aa5-951a-fcfc480dd05a",
    title: "Hello World!",
    content: "This is an example.",
    idAuthor: "3851d8b4-5358-43f2-ba23-f4d481358901",
    author: {
      id: "3851d8b4-5358-43f2-ba23-f4d481358901",
      name: "Michel",
      email: "orphee@gmail.com"
    }
  }
  */
});
```



### Documentation

[https://www.justonepixel.com/NothingToThing](https://www.justonepixel.com/NothingToThing) (branch `gh-pages).

### Help

No SLA, but a few developers hang out there and may be able to help:

- [irc://irc.freenode.org/rethinkdb](irc://irc.freenode.org/rethinkdb)
- [https://gitter.im/neumino/NothingToThing](https://gitter.im/neumino/NothingToThing)

### Run the tests

```
npm test
```

### Contribute

You are welcome to do a pull request.


### Roadmap

The roadmap is defined with the issues/feedback on GitHub. Checkout:
[https://github.com/neumino/NothingToThing/issues](https://github.com/neumino/NothingToThing/issues)


### Author
- Michel Tu -- orphee@gmail.com -- [blog](http://blog.justonepixel.com) -- [twitter](https://twitter.com/neumino)

### Contributors

- [chrisfosterelli](https://github.com/chrisfosterelli)
- [colprog](https://github.com/colprog)
- [dulichan](https://github.com/dulichan)
- [flienteen](https://github.com/flienteen)
- [marshall007](https://github.com/marshall007)
- [mindjuice](https://github.com/mindjuice)
- [Morhaus](https://github.com/Morhaus)
- [primitive-type](https://github.com/primitive-type)
- [nikaspran](https://github.com/nikaspran)
- [rasapetter](https://github.com/rasapetter)
- [simonratner](https://github.com/simonratner)
- [wezs](https://github.com/wezs)


### License

MIT, see the [LICENSE](https://github.com/neumino/NothingToThing/blob/master/LICENSE) file
