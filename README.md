## Design rules

### remap @id and @type

We want to hide json-ld specific keys. `@id` is remapped to `id`, `@type` is remapped to `type`.

### ordering

We order the declaration by namespaces, as they are given in the linked data application profile document.


### handle key clashes

We choose to handle key clashes by suffixing the key with the prefix, e.g. `type` vs. `type_dct`.

## TODO

### accrualPeriodicity

Properly handle the IRI or Literal situation : 

> This property contains the publication frequency of the continuing resource, from the Dublin Core Collection Description Frequency Namespace, or as the literal values "unknown" or "other".

Right now we specify it as "@id"

### Check the @id vs. @vocab

Should we declare controlled list values in the context ?

