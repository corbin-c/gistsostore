# DataGists

[DataGists](https://github.com/corbin-c/datagists/) is a project by
[Clément Corbin](https://github.com/corbin-c/). Feel free to contribute.

DataGists is a JS module for data storage & retrieval on
[Github's Gists](https://gist.github.com/). It makes use of
[Github's API v3](https://developer.github.com/v3/).

To run DataGists, import it first:

```javascript
import { DataGists } from "https://corbin-c.github.io/datagists/DataGists.js";
```

Then you can create a DataGists object, which must be fed with an Auth Token
(Mandatory, can be obtained at https://github.com/settings/tokens - todo: OAuth
should be used instead).

```javascript
let myGists = new DataGists(auth_token);
```

As this module fetches Github's API, you might want to wait for it being done
before doing something else, with `await` operator. Once created, DataGists
object has to be initialized, this will check the auth token:

```javascript
await myGists.init();
```

If you don't know which Gists are available, you can simply call:

```javascript
myGists.listGists();
```

Once your target Gist is identified, you can start working with it:

```javascript
let currentGist = await myGists.useGist(gist);
```

The above `gist` variable is meant to be an object providing either an ID or a 
description : `gist = {id:id_string,description:gist_description};`

Now, getting a file raw content can be achieved easily:

```javascript
currentGist.getContent(file_name);
```

Similarly, putting content to a file is done as follow:

```javascript
currentGist.putContent(file_name,content,[append]);
```

The optional `[append]` parameter is a boolean flag. If set to true, content
will be added to the file instead of overwriting it. **Note: new content added
to the file is appended at the beggining of the file.**
