## Meta Find

The meta feed is being handled by the `meta.find` method. This is used for loading full catalogue in Discover (Stremio).

```javascript
var addon = new Stremio.Server({
	"meta.find": function(args, callback, user) {
		// expects array of meta elements (primary meta feed)
		// it passes "limit" and "skip" for pagination
	}
});
```

### Request

_otherwise known as `args` in the above code_

```javascript
{
  query: {
    type: 'movie',                     // can also be "tv", "series", "channel"
    'popularities.basic': { '$gt': 0 }
  },
  popular: true,
  complete: true,
  sort: {
    'populstities.basic': -1
  },
  limit: 70,                           // limit length of the response array to "70"
  skip: 0                              // offset, as pages change it will progress to "70", "140", ...
}
```

When an array of fewer then `70` elements is returned, the feed will be considered finished and pagination will no longer be requested.

See [Meta Request](meta.request.md) for Parameters.

See [Content Types](content.types.md) for the `type` parameter.

### Response

```javascript
[
  {
    id: 'basic_id:opa2135',         // unique ID for the media, will be returned as "basic_id" in the request object later
    name: 'basic title',            // title of media
    poster: 'http://goo.gl/rtxs10', // image link
    posterShape: 'regular',         // can also be 'landscape' or 'square'
    banner: 'http://goo.gl/xgCrG9', // image link
    genre: ['Entertainment'],
    isFree: 1,                      // some aren't
    popularity: 3831,               // the larger the better
    popularities: { basic: 3831 },  // same as 'popularity'
    type: 'movie'                   // can also be "tv", "series", "channel"
  },
  ...
]
```

See [Meta Element](meta.element.md) for Parameters.

See [Content Types](content.types.md) for the `type` parameter.
