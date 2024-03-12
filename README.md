## Design rules

### remap @id and @type

We want to hide json-ld specific keys. `@id` is remapped to `id`, `@type` is remapped to `type`.

### @base declaration

Notices should declare their base URI to the record URI, e.g.

```
"@context": {
    "@import": "https://raw.githubusercontent.com/sparna-git/issn-jsonld-context/main/issn-jsonld-context.json",
    "@base": "http://issn.org/resource/ISSN/0028-0836"
  },
```

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
    "formofmaterial":"http://marc21rdf.info/terms/formofmaterial#",
    "countries": "http://id.loc.gov/vocabulary/countries/",
```

### use of identifier indexing

```
    "identifiedBy" : {
      "@id" : "bf:identifiedBy",
      "@type" : "@id",
      "@container": "@id"
    },
```

This forces us to repeat the ISSN-L inside the identifierBy of the ISSN-L, but this is not bad thing:

```
  "isPartOf" : {
    "id" : "http://issn.org/resource/resource/ISSN-L/0247-0624",
    "identifiedBy" : {
      "#ISSN-L" : {
        "type" : "bf:IssnL",
        "status" : "idStatus:Valid",
        "value" : "0247-0624"
      }
    }
  },
```

### reverse properties

We want to have a hierarchical structure from the resource down to its Record and down to its CreationEvent. Thus we need 2 inverse hierarchical links:

```
"generated_by" : {
  "@reverse" : "prov:generated",
  "@type" : "@id"
},
```

and 

```
"mainEntity_of" : {
  "@reverse" : "schema:mainEntity",
  "@type" : "@id"
},
```

## TODO / Open questions

### accrualPeriodicity

Properly handle the IRI or Literal situation : 

> This property contains the publication frequency of the continuing resource, from the Dublin Core Collection Description Frequency Namespace, or as the literal values "unknown" or "other".

Right now we specify it as "@id"

### Check the @id vs. @vocab

Should we declare controlled list values in the context ?

### Should we declare additional namespaces for controlled vocabularies ?

e.g. `http://marc21rdf.info/terms/formofmaterial#a`, `http://id.loc.gov/vocabulary/countries/fr` ?

Not sure we really need this, this will hide a lot of URI. Maybe the URIs should be kept in clear ?

### check values of dct:spatial on Organization

Is it using URIs ?

### How should we handle hierarchical nesting ?

In the case entity is referenced from multiple places


## Application Profile document update

### Update the use of bibschema in the application profile

bibschema namespace is outdated. Properties have been integrated directly in schema.org

- bibschema:translationOfWork exists as schema:translationOfWork
- bibschema:workTranslation exists as schema:workTranslation
- bibschema:Atlas, bibschema:Map, bibschema:AudioObject, bibschema:VideoObject, bibschema:Newspaper all exist in schema.org
- bibschema:publishedBy exists as schema:publishedBy

I have set the corresponding mapping to schema URI instead of bibschema URIs

### update versionOf in AP

dct:versionOf does not exist. It should be dct:isVersionOf.

### reference to dcterms namespace

At least one reference subsist to dcterms: namespace, should be replaced by dct:

### xsd:number is wrong

xsd:number is wrong and should be replaced by xsd:decimal

### reference to issn: namespace

issn: namespace should be replaced by issnprop: namespace

### memberOf is not in the application profile

nature exemple uses memberOf on classification information, but this is not in the AP table, not in the diagrams. The mapping table contains it, but with visible errors in the URIs. Should it be added to the AP ?

### Check dcam namespace: missing a final /

### Check bfmarc namespace: missing a final /

### Check namespace consistence m2100X vs m2100x : should use capital X

## Problem notice Nature

- Missing #ISSN identifier in the data !!
- hasCancelledISSN : Wrong value URI
- GeoCoordinates are missing, should this be skipped if no geo information is available ?
- Problem in URI of "M008CR22" : "http://marc21rdf.info/terms/continuingori##"
- There is an entity `resource/ISSN/0028-0836#PublicationPlace-London_:` (note the `_:` at the end) that is never referenced from any publication event. Is this an error ? I remove it
- Wrong URI in `"wasAssociatedWith" : "http://www.w3.org/ns/ISSNCentre#BO"`
- I can't find an identifier attribute in the Nature record ?