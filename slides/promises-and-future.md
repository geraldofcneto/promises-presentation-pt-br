
# Promises
### Concept, Motive and Implementations

---

## What is it?

- Something that will or won't be fulfilled 
- Asynchronous tasks <!-- .element: class="fragment" -->
- Proposed in 1976 in works of parallel processing <!-- .element: class="fragment" -->

Note: A promise is something that might not be ready yet, but will or won't be ready in the end. 
In Computer Science the concept of Promises, Futures and Delay as a way to deal with async tasks, and not a new one. 
In fact, it dates back from 76, when Daniel Friedman and David Wise coined the term in the International Conference in Parallel Processing. 
It is based on the idea of delaying the usage of the result of an async computation until the computation is ready.

---

## Simplify the synchronization in concurrent systems

- Less callbacks <!-- .element: class="fragment" -->
- Less identation levels <!-- .element: class="fragment" -->
- More control over exception handling <!-- .element: class="fragment" -->
- More semantics <!-- .element: class="fragment" -->

Note: Promises can help keeping a cleaner syntax while dealing with asynchronous tasks, ease the synchronization of those tasks and simplify the error/exception handling, giving a better semantic to control these fluxes

---

## Promise States:

- pending
- fulfilled
- rejected 

Note: Each promise represents the *possible* result of a task, and starts at the pending state. It can be fulfilled and return a success value or, being rejected, return error details.

---

## Without Promises

```
function readJSON(filename, callback){
  fs.readFile(filename, 'utf8', function (err, res){
    if (err) return callback(err);
    try {
      res = JSON.parse(res);
    } catch (ex) {
      return callback(ex);
    }
    callback(null, res);
  });
}
```

Note: Here we have a piece of async code without promises.
The callback looks a little out of place here, been called in different occasions with different parameters.
In the 1st call, it denotes an error in the readFile function.
2nd, an error in the parse function, and
3rd, a successful execution with null error and valid res.

---

## Without Promises

- No return
- No throw
- No stacktrace

Note: We notice that the return is used only to fast-fail the function, since callbacks don't handle returned values.
In the same way, there is no need to throw errors/exceptions because they wont be catched.
And so, no stacktrace would be available, as the callback exists in a separate thread.

---

## With Promises

```
function readJSON(filename){
  return readFile(filename, 'utf8').then(JSON.parse);
}
```

Note: And here, the same functionality if the readFile could return a promise.
As soon as readFile produces a value, it would feed the parse function and the program would continue.

---

##  JS implementations

- [then/promise](https://github.com/then/promise) Simple implementation of [Promises/A+](https://promisesaplus.com/) open standard
- [kriskowal/q](https://github.com/kriskowal/q/blob/v1/design/README.js) Whose implementation inspired angularjs $q service
- [petkaantonov/bluebird](https://github.com/petkaantonov/bluebird) Performance-focused implementation
