# powerappsportal-liquid-cheat-sheet
Cheat sheet for Power Apps Portal liquid

## Liquid Objects

### page

Rerers to the current page. Combines the attributes from sitemap and entity type records. Extends entity object.

| Attribute | Description |
|-----------|-------------|
| breadcrumbs | Returns an **array** of site map nodes from root page to parent of the current page|
| url | The URL of the page |
| title | The title of the page |
| parent | Returns the parent site map node of the current page |
| adx_entityform | Lookup to an entity form associated with the current page |
| adx_entitylist | Lookup to an entity list associated wtih the current page |

### user

Rerers to the current portal user. Provides access to the underlying contact record and some additional attributes. If user is not signed in will return null. Extends entity object.

| Attribute | Description |
|-----------|-------------|
| roles | Returns an **array** of roles associated with current user |
| parentcustomerid | Lookup to the parent contact or parent account of the current record |

### request

Provides information about the current HTTP request

| Attribute | Description |
|-----------|-------------|
| params | Named parameter values for the current request. It is a combintaion of a URL query, string parameters, form post parameters and cookies. For example: to access id parameter that was passed as part of query you need to call **request.params['id']** |
| path | Path to the current request URL. For example /profile/ |
| path_and_query |  The path and query to the current request URL. For example /profile/?id=test&number=5 |
| query | The query part of the current request URL. For example ?id=test&number=5 |
| url | Full url of the cyrrent request. For example https://<portal_url>/profile/?id=test&number=5 |

### snippets

Allows to load content snippets by name. If snippet not found will return null.

{{snippets[Header]}}

{{snippets['My Awesome Snippet']}}

### sitemarkers

Allows to load site marker by name. If not found will return null. Extends entity object.

| Attribute | Description |
|-----------|-------------|
| url | The url of the site marker target page |

### entities

Allows to load dataverse entity by ID. If the entity exists entity object will be returned. If not found will return null

| Attribute | Description |
|-----------|-------------|
| url | The url of the site marker target page |

## Liquid Tags

### entityform

### powerbi
