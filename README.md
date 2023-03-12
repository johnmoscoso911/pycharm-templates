
#### Odoo 15 Live Templates
- [Python](python/README.md)

- [XML](xml/README.md)

#### How to editing/updating/deleting in one2many and many2many
- `(0, 0, { values })` **link to a new record** that needs to be created with the given values dictionary

- `(1, ID, { values })` **update** the linked record with id = ID (write values on it)

- `(2, ID)` **remove and delete** the linked record with id = ID (calls unlink on ID, that will delete the object completely, and the link to it as well)

- `(3, ID)` cut the link to the linked record with id = ID (**delete the relationship between the two objects but does not delete the target object itself**)

- `(4, ID)` **link to existing record** with id = ID (adds a relationship)

- `(5)` **unlink all** (like using `(3, ID)` for all linked records)

- `(6, 0, [IDs])` **replace the list** of linked IDs (like using `(5)` then `(4, ID)` for each ID in the list of IDs)

#### How to use in
- [CentOS](CentOS/README.md)

- [MacOS](iMac/README.md)


#### More info
[JetBrains Help](https://www.jetbrains.com/help/pycharm/project-and-ide-settings.html)