# docuri [![Build Status](https://travis-ci.org/jo/docuri.svg?branch=master)](https://travis-ci.org/jo/docuri)
Rich document ids for CouchDB:

```
type/id/subtype/index/version
```

For example: `movie/blade-runner/gallery-image/12/medium`

Docuris have many advantages:
* You can access the doc type (eg. in changes feed)
* They sort well in Futon
* They tell a lot about the document
* You can rely on a schema and construct ids of dependend documents (eg. a specific version of an image)
* You can easily delete related documents (eg. by requesting a range from `_all_docs`)
 
...and I'm sure I forgot to mention the best.

Give Docuris a try!

## Usage
Parse id string:
```js
var docuri = require('docuri');
docuri.parse('mytype/myid/mysubtype/myindex/myversion');
// {
//   type: 'mytype',
//   id: 'myid',
//   subtype: 'mysubtype',
//   index: 'myindex',
//   version: 'myversion'
// }
```

Build id string from object:
```js
docuri.stringify({
  type: 'mytype',
  id: 'myid',
  subtype: 'mysubtype',
  index: 'myindex',
  version: 'myversion'
});
// 'mytype/myid/mysubtype/myindex/myversion'
```

Change id string components:
```js
docuri.merge('mytype/myid/mysubtype/myindex/myversion', {
  type: 'my_new_type',
});
// 'my_new_type/myid/mysubtype/myindex/myversion'
```

Use custom definition:
```js
docuri(['id', 'meta']).parse('42/answer');
// {
//   id: '42',
//   meta: 'answer'
// }
```

Access current definition:
```js
docuri();
// ['type', 'id', 'subtype', 'index', 'version']
docuri(['id', 'meta']);
docuri();
// ['id', 'meta']
```

## Browser support
To use docid in your client-side application, browserify it like this:

```shell
browserify -s DocURI path/to/docuri/index.js > path/to/your/assets

```
Once added to your DOM, this will leave you with a global DocURI object for use
in your e.g.  Backbone Models/Collections.

## Development
To run the unit tests:
```shell
npm test
```

## License
Copyright (c) 2014 Johannes J. Schmidt, null2 GmbH   
Licensed under the MIT license.

