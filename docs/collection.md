### Collection

A Collection is a decorated array that includes the following standard array methods:

`every()`, `filter()`, `forEach()`, `indexOf()`, `lastIndexOf()`, `map()`, `pop()`, `push()`, `reverse()`, `shift()`, `slice()`, `some()`, `sort()`, `splice()`, `unshift()`

These methods are assumed to be present on the `Array.prototype` and therefore need to be polyfilled if support older browsers is required – in which case I suggest [Augment.js](http://augmentjs.com/).

#### `add(model)`

Adds a model to a collection and won’t allow you to add the same model to a collection more than once. An “add” event is emitted by the collection when a model is successfully added to it.

    Food.collection
    // => []
    
    var egg = new Food({ id: 1, name: "egg" })
    var ham = new Food({ id: 2, name: "ham" })
    var cheese = new Food({ id: 3, name: "cheese" })
    
    Food.collection.add(egg)
    Food.collection
    // => [egg]
    
    Food.collection.add(ham).add(cheese)
    Food.collection
    // => [egg, ham, cheese]
    
    Food.collection.add(egg)
    Food.collection
    // => [egg, ham, cheese]

#### `at(index)`

Returns the model at the specified index.

    Food.collection.at(1)
    // => ham

#### `detect(func[, context])`

Returns the first model that matches the supplied function.

    Food.collection.detect(function(model) {
      return model.get("name") == "ham"
    })
    // => ham

#### `first()`

Returns the first model in the collection.

    Food.collection.first()
    // => egg

    Food.collection.filter(function(model) {
      return model.get("name").indexOf("h") > -1
    }).first()
    // => ham

#### `last()`

Returns the last model in the collection.

    Food.collection.last()
    // => cheese

#### `length`

Returns the size of the collection, just like an array.

    Food.collection.length
    // => 3

    Food.collection.filter(function(model) {
      return ~model.get("name").indexOf("e")
    }).length

#### `pluck(attribute)`

Returns an array of values for the specified attribute.

    Food.collection.pluck("name")
    // => ["egg", "ham", "cheese"]

    Food.collection.filter(function(model) {
      return model.get("name").indexOf("e") > -1
    }).pluck("name")
    // => ["egg", "cheese"]

#### `remove(model)`

Removes a model from a collection. A “remove” event is emitted by the collection when a model is removed from it.

    Food.collection
    // => [egg, ham, cheese]

    Food.collection.remove(egg)
    Food.collection
    // => [ham, cheese]

#### `sortBy(attribute || func)`

Returns the collection sorted by either an attribute or a custom function.

    Food.collection.sortBy("name")
    // => [cheese, egg, ham]

    Food.collection.sortBy(function(model) {
      return model.get("name").length
    })
    // => [egg, ham, cheese]

#### `toArray()`

Returns an array

#### `toJSON()`

Returns an array of its models' attributes by calling [`toJSON()`](#tojson) on each one.
