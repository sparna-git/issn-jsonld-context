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

We follow the naming convention used in the application profile. :

```
    "idStatus":"http://issn.org/vocabularies/IdentifierStatus#",
    "recordStatus":"http://issn.org/vocabularies/RecordStatus#",
    "medium":"http://issn.org/vocabularies/Medium#",
```

We add :

```
    "issnCenter":"http://issn.org/organization/ISSNCenter#",
```

### use of indexing

```
    "identifiedBy" : {
      "@id" : "bf:identifiedBy",
      "@type" : "@id",
      "@container": "@id"
    },
```

## TODO

### accrualPeriodicity

Properly handle the IRI or Literal situation : 

> This property contains the publication frequency of the continuing resource, from the Dublin Core Collection Description Frequency Namespace, or as the literal values "unknown" or "other".

Right now we specify it as "@id"

### Check the @id vs. @vocab

Should we declare controlled list values in the context ?

### Should we declare additional namespaces for controlled vocabularies ?

e.g. `http://marc21rdf.info/terms/formofmaterial#a`, `http://id.loc.gov/vocabulary/countries/fr` ?
