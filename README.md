## Design rules

### remap @id and @type

We want to hide json-ld specific keys. `@id` is remapped to `id`, `@type` is remapped to `type`.

### sections

Sections in the context files are separated by 2 newlines for readability.

### ordering

We order the declaration by namespaces, as they are given in the linked data application profile document.

### handle key clashes

We choose to handle key clashes by suffixing the key with the prefix, e.g. `type` vs. `type_dct`.

This is the case for :
  - issn (issn_bibo vs. issn_schema)
  - type

### Controlled vocabularies namespaces

We do not follow the naming convention used in the application profile. For consistency we set the keys to :

```
    "IdentifierStatus":"http://issn.org/vocabularies/IdentifierStatus#",
    "RecordStatus":"http://issn.org/vocabularies/RecordStatus#",
    "Medium":"http://issn.org/vocabularies/Medium#",
```

## TODO

### accrualPeriodicity

Properly handle the IRI or Literal situation : 

> This property contains the publication frequency of the continuing resource, from the Dublin Core Collection Description Frequency Namespace, or as the literal values "unknown" or "other".

Right now we specify it as "@id"

### Check the @id vs. @vocab

Should we declare controlled list values in the context ?

