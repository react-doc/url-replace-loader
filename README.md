
<div align="center">
  <a href="https://github.com/webpack/webpack">
    <img width="200" height="200"
      src="https://cdn.rawgit.com/webpack/media/e7485eb2/logo/icon.svg">
  </a>
  <h1>URL Replace Loader</h1>
  <p>Loads files as `base64` encoded URL, <a href="https://github.com/webpack-contrib/url-loader">url-loader</a> enhanced.</p>
</div>


<h2 align="center">Install</h2>

```bash
npm install --save-dev url-replace-loader
```

<h2 align="center"><a href="https://webpack.js.org/concepts/loaders">Usage</a></h2>

The `url-loader` works like the [`file-loader`](https://github.com/webpack-contrib/file-loader), but can return a DataURL if the file is smaller than a byte limit.


```js
import img from './image.png'
```

**webpack.config.js**
```js
module.exports = {
  module: {
    rules: [
      {
        test: /\.(svg|png|bmp|jpg|jpeg|gif)$/,
        loader: require.resolve('url-loader'),
        options: {
          limit: 8192,
          name: 'img/[name].[hash:8].[ext]',
          replace: [
            {
              test: /rdoc\.logo\.svg$/,
              path: 'path/to/logo.svg',
            }
          ]
        },
      },
    ]
  }
}
```


<h2 align="center">Options</h2>

|Name|Type|Default|Description|
|:--:|:--:|:-----:|:----------|
|**`limit`**|`{Number}`|`undefined`|Byte limit to inline files as Data URL|
|**`mimetype`**|`{String}`|`extname`|Specify MIME type for the file (Otherwise it's inferred from the file extension)|
|**`fallback`**|`{String}`|`file-loader`|Specify `loader` for the file when file is greater than the limit (in bytes)|

### `limit`

If the file is greater than the limit (in bytes) the [`file-loader`](https://github.com/webpack-contrib/file-loader) is used by default and all query parameters are passed to it.
You can use other loader using `fallback` option.

The limit can be specified via loader options and defaults to no limit.

**webpack.config.js**

```js
{
  loader: 'url-loader',
  options: {
    limit: 8192
  }
}
```

### `mimetype`

Set the MIME type for the file. If unspecified the file extensions will be used to lookup the MIME type.

**webpack.config.js**
```js
{
  loader: 'url-loader',
  options: {
    mimetype: 'image/png'
  }
}
```

### `fallback`

**webpack.config.js**
```js
{
  loader: 'url-loader',
  options: {
    fallback: 'responsive-loader'
  }
}
```

### `replace`

Replace with the specified picture.

**webpack.config.js**
```js
{
  loader: 'url-loader',
  options: {
    replace: [
      {
        test: /rdoc\.logo\.svg$/,
        path: 'path/to/logo.svg',
      }
    ]
  }
}
```