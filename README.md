Just an old proof of concept.


Tubbs-RiakStorage
=================

Tubbs-RiakStorage is a riak adaptor for [Tubbs](https://github.com/dandean/tubbs).

Example:
--------

```js
var Tubbs = require("tubbs");
var Validate = require("tubbs/lib/validate");
var Memory = require("tubbs/lib/memory");
var RiakStorage = require('tubbs-riakstorage');

var dataStore = new RiakStorage({ host:'192.168.33.101', bucket: 'users' });

function User(data) {
  this.setData(data);
}

Tubbs(User, {
  // Persist our data with Riak
  dataStore: dataStore,
  primaryKey: 'username',
  fields: {
    username: undefined,
    password: undefined,
    first: "Rad",
    last: undefined,
    email: undefined
  },

  virtual: {
    name: function() {
      return ((this.first || '') + ' ' + (this.last || '')).trim();
    }
  }
});

module.exports = dataStore.DataType = User;
```

See [Tubbs](https://github.com/dandean/tubbs) for more information.
