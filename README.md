# powerappsportal-liquid-cheat-sheet
Cheat sheet for Power Apps Portal liquid

## Liquid Objects

### Entity reference object

Object that represents lookup (entity reference)

| Attribute | Description |
|-----------|-------------|
| id | The guid of the referenced entity as a string|
| logical_name | The dataverse logical name of the entity |
| name | The primary name attribute of the referenced entity |

### Option Set Value (or Dataverse Choise)

Object that represents option set/ picklist/ choise column.

| Attribute | Description |
|-----------|-------------|
| label | The localized label of the option set|
| value | The integer value of the option set |

### Note

Object that represents note (annotation) record. Extend entity object.

| Attribute | Description |
|-----------|-------------|
| documentbody | File body of the note as base64 encoded string. Not loaded with rest of the attribute and only available ondemand ie by direct call. May slow down rendering of the page |
| url | Url path to the built-in annotation handler for the portal. If user has permission and note has attached file, request to this url will download the note file attachment |

### entities

Allows to load dataverse entity by ID. If the entity exists entity object will be returned. If not found will return null

| Attribute | Description |
|-----------|-------------|
| id | The guid if the entity |
| logical_name | The dataverse logical name of the entity |
| notes | Returns array of notes (as notes objects) associated with the entity, ordered from oldest to newest by createon field |
| <attribute or relationship name> | You can access any attribute or relationship of the Dataverse entity by it's logical name. |

### page

Refers to the current page. Combines the attributes from sitemap and entity type records. Extends entity object.

| Attribute | Description |
|-----------|-------------|
| breadcrumbs | Returns an **array** of site map nodes from root page to parent of the current page|
| url | The URL of the page |
| title | The title of the page |
| parent | Returns the parent site map node of the current page |
| adx_entityform | Lookup to an entity form associated with the current page |
| adx_entitylist | Lookup to an entity list associated wtih the current page |

### user

Refers to the current portal user. Provides access to the underlying contact record and some additional attributes. If user is not signed in will return null. Extends entity object.

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

{{snippets['My Awesome Snippet']}}

### sitemarkers

Allows to load site marker by name. If not found will return null. Extends entity object.

| Attribute | Description |
|-----------|-------------|
| url | The url of the site marker target page |


## Liquid Tags

### fetchxml

Allows users to query data from Dataverse and render the results in a page using fetchxml query syntax. Learn more about fetchxml [here](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/use-fetchxml-construct-query).

```
{% fetchxml contactFeed %}
<fetch version"1.0" mapping="logical">
  <entity name="contact">
    <attribute name="fullname">
    <attribute name="emailaddress1">
    <attribute name="parentcustomerid">
  </entity>
</fetch>
{% endfetchxml %}

{% for result in contactFeed.results.entities %}
// do something with results
{% endfor %}
```

Result attribute contains couple of useful attributes

| Attribute | Description |
|-----------|-------------|
| entities | Result of fetchxml query |
| entityname | Logical name of the entity |
| extensiondata | Gets the structure that contains extra data. |
| MinActiveRowVersion | Gets the lowest active row version value. |
| MoreRecords | Gets whether there are more records available. |
| PagingCookie | Gets the current paging information |
| TotalRecordCount | Gets the total number of records in the collection.
ReturnTotalRecordCount was true when the query was executed. |
| TotalRecordCountLimitExceeded | Gets whether the results of the query exceeds the total record count |

### entityform

### powerbi
