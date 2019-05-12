# 🥣 deserialize-json-api
Immutable json:api deserializer

## Install

```
yarn add deserialize-json-api
```

## Usage

```js
import { deserialize } from 'deserialize-json-api';

const body = {
  data: {
    id: 1,
    type: 'movie',
    attributes: { name: 'test movie', year: 2014 },
    relationships: {
      actors: { data: [{ id: 1, type: 'actor' }] },
      awards: {
        data: [
          {
            id: 4,
            type: 'award',
            links: { self: '/awards/1' },
            meta: { verified: false }
          }
        ]
      },
    },
    links: { self: '/movies/1' },
    meta: { saved: false }
  },
  included: [
    {
      type: 'actor',
      id: 1,
      attributes: { name: 'John', age: 80 }
    },
    {
      type: 'award',
      id: 4,
      attributes: { type: 'Oscar', category: 'Best director'}
    }
  ],
  meta: { copyright: 'Copyright 2015 Example Corp.' },
  errors: [{ title: 'Error!' }]
};

const deserializedData = deserialize(body);

body === body // true

JSON.stringify(deserializedData) ===  JSON.stringify(
  {
    data: {
      id: 1,
      type: 'movie',
      links: { self: '/movies/1' },
      meta: { saved: false },
      name: 'test movie',
      year: 2014,
      actors: [
        {
          id: 1,
          type: 'actor',
          name: 'John',
          age: 80
        }
      ],
      awards: [
        {
          id: 4,
          type: 'Oscar',
          links: { self: '/awards/1' },
          meta: { verified: false },
          category: 'Best director'
        }
      ]
    },
    meta: { copyright: 'Copyright 2015 Example Corp.' },
    errors: [{ title: 'Error!' }]
  }
)
```

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b feature/fooBar`)
3. Commit your changes (`git commit -am 'Add some fooBar'`)
4. Push to the branch (`git push origin feature/fooBar`)
5. Create a new Pull Request
