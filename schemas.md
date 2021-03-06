---
layout: default
---

# Sinopia JSON Schemas for Resource Templates / Profiles

## Version (future)

Desired updates:
- don't accept empty attributes (even if not required);  leave them out or provide a value

Resource Template:
- is there a real difference between description and resourceLabel?  If not, can we remove one?

Property Template:
- defaults:
    - is dataTypeURI associated with default values only? if so, adjust schema accordingly (put with defaults)
    - is dataTypeURI required when defaults are specified? if so, adjust schema accordingly
- use resourceTemplates at outer level instead of valueConstraint.valueTemplateRefs (or move  valueTemplateRefs out a level and get rid of resourceTemplates)
- move useValuesFrom out a level, instead of valueConstraints.useValuesFrom
- move defaults out a level, instead of valueConstraints.defaults
- move dataTypeURI out two levels, instead of valueConstraints.valueDataType.dataTypeURI or maybe include it within default, if it is only used for (type lookup with a ?) default.
- only accept boolean (not string) for true/false.  (e.g. true not "true")

## Version 0.2.1
Adds support for subtype equals `context`. 

## Version 0.2.0

Version 0.2.0 is the same as version 0.1.0 in all respects except that it further requires that a resource template ID contain no spaces in the ID string. This is due to the fact that the resource template ID becomes the last path part of the Sinopia server resource URI, and that URI cannot contain spaces in order to resolve correctly when fetching the resource.

Note:  0.2.0 is not the same as 0.0.2

### 0.2.0 schemas:

- <https://ld4p.github.io/sinopia/schemas/0.2.0/profile.json>
- <https://ld4p.github.io/sinopia/schemas/0.2.0/resource-templates-array.json>
- <https://ld4p.github.io/sinopia/schemas/0.2.0/resource-template.json>
- <https://ld4p.github.io/sinopia/schemas/0.2.0/property-templates-array.json>
- <https://ld4p.github.io/sinopia/schemas/0.2.0/property-template.json>
- <https://ld4p.github.io/sinopia/schemas/0.2.0/profiles-array.json>


## Version 0.1.0

Version 0.1.0 has more stringent requirements than version 0.0.9, based on how the editor uses the templates.
It also tries to avoid noise in the templates by forbidding empty attributes.

Changes from version 0.0.9:

- If properties are present, they must not be empty.

- Profile
    - update schema attribute version

- Resource Template:
    - require author attribute
    - require date attribute
    - update schema attribute version

- Property Template:
    - conditional JSON schemas that only allow appropriate valueConstraints given the type:
      - lookup:
        - require valueConstraint
        - disallow valueTemplateRefs
        - (also disallow resourceTemplates)
      - resource:
        - require valueConstraint
        - disallow useValuesFrom
        - disallow defaults
      - literal:
        - disallow valueTemplateRefs as well as useValuesFrom
        - (also disallow resourceTemplates)

    - valueConstraint can have at most one of useValuesFrom, valueTemplateRefs
    - valueConstaint.useValuesFrom requires at least one entry (or it shouldn't be present)
    - valueConstaint.valueTemplateRefs requires at least one entry (or it shouldn't be present)
    - valueConstraint.valueDataType requires dataTypeURI (or it shouldn't be present)

### 0.1.0 schemas:

- <https://ld4p.github.io/sinopia/schemas/0.1.0/profile.json>
- <https://ld4p.github.io/sinopia/schemas/0.1.0/resource-templates-array.json>
- <https://ld4p.github.io/sinopia/schemas/0.1.0/resource-template.json>
- <https://ld4p.github.io/sinopia/schemas/0.1.0/property-templates-array.json>
- <https://ld4p.github.io/sinopia/schemas/0.1.0/property-template.json>
- <https://ld4p.github.io/sinopia/schemas/0.1.0/profiles-array.json>


## Version 0.0.9

Tweak made 2019-05-14:  (
- This was a small, well tested, backwards compatible tweak and we chose NOT to create a new version of the JSON schemas for more seamless backwards compatibility (and against string semantic versioning).
- Property Template:
    - valueConstraint.defaults
      - `defaultURI` is now an ordinary string; URI format is not required.  This allows for `defaultURI` to be an empty string.
      - `defaults` array's objects have no required fields.  This allows for either or both of `defaultURI` and `defaultLiteral` to be present or missing.

Version 0.0.9 JSON Schemas are streamlined for Sinopia work.      

Changes from version 0.0.2:

- Profile:
    - require author attribute
    - add required schema attributes
    - add adherence attribute
    - add source attribute

- Resource Template:
    - add required schema attributes
    - add adherence attribute
    - add author attribute
    - add date attribute
    - add source attribute

- Property Template:
    - type attribute can only be 'literal', 'resource', or 'lookup'
    - conditional JSON schemas that require appropriate valueConstraints given the type:
      - lookup:
        - require valueConstraints.useValuesFrom
      - resource:
        - require valueConstraints.valueTemplateRefs
    - mandatory and repeatable properties can be proper booleans OR strings (e.g. true or 'true')
    - valueConstraint.editable attribute removed as it will always be true
    - removed attributes that were never used or ignored in profile editor, BFE and RDF generated:
      - valueConstraint.remark
      - valueConstraint.repeatabe (duplicate of outer repeatable attribute)
      - valueConstraint.validatePattern
      - valueConstraint.valueLanguage
      - valueConstraint.valueDataType.dataTypeLabel
      - valueConstraint.valueDataType.dataTypeLabelHint
      - valueConstraint.valueDataType.remark

### 0.0.9 schemas:

- <https://ld4p.github.io/sinopia/schemas/0.0.9/profile.json>
- <https://ld4p.github.io/sinopia/schemas/0.0.9/resource-templates-array.json>
- <https://ld4p.github.io/sinopia/schemas/0.0.9/resource-template.json>
- <https://ld4p.github.io/sinopia/schemas/0.0.9/property-templates-array.json>
- <https://ld4p.github.io/sinopia/schemas/0.0.9/property-template.json>
- <https://ld4p.github.io/sinopia/schemas/0.0.9/profiles-array.json>


## Version 0.0.3

Version 0.0.3 is the same as version 0.0.2 in all respects except that it further requires that a resource template ID contain no spaces in the ID string. This is due to the fact that the resource template ID becomes the last path part of the Sinopia server resource URI, and that URI cannot contain spaces in order to resolve correctly when fetching the resource.

### 0.0.3 schemas:

- <https://ld4p.github.io/sinopia/schemas/0.0.3/profile.json>
- <https://ld4p.github.io/sinopia/schemas/0.0.3/resource-templates-array.json>
- <https://ld4p.github.io/sinopia/schemas/0.0.3/resource-template.json>
- <https://ld4p.github.io/sinopia/schemas/0.0.3/property-templates-array.json>
- <https://ld4p.github.io/sinopia/schemas/0.0.3/property-template.json>
- <https://ld4p.github.io/sinopia/schemas/0.0.3/profiles-array.json>

## Version 0.0.2

Version 0.0.2 JSON Schemas are the same as Version 0.0.1, but additionalProperties has been set to false for all properties of type "object".  This means the object (e.g. profile or resourceTemplate or propertyTemplate or valueConstraint ...) is not valid if it has additional properties that weren’t explicitly listed in the JSON schema.

It was an oversight that this wasn't included in Version 0.0.1 schemas.

Also:  resourceTemplate can have author attribute.

### 0.0.2 schemas:

- <https://ld4p.github.io/sinopia/schemas/0.0.2/profile.json>
- <https://ld4p.github.io/sinopia/schemas/0.0.2/resource-templates-array.json>
- <https://ld4p.github.io/sinopia/schemas/0.0.2/resource-template.json>
- <https://ld4p.github.io/sinopia/schemas/0.0.2/property-templates-array.json>
- <https://ld4p.github.io/sinopia/schemas/0.0.2/property-template.json>
- <https://ld4p.github.io/sinopia/schemas/0.0.2/profiles-array.json>


## Version 0.0.1

Version 0.0.1 JSON Schemas cleanly validate the LC profiles from <https://github.com/lcnetdev/verso> with a minimum of changes to those profiles. (See <https://github.com/LD4P/sinopia_sample_profiles/pull/14> for the changes required)

- https://ld4p.github.io/sinopia/schemas/0.0.1/profile.json>
- <https://ld4p.github.io/sinopia/schemas/0.0.1/resource-templates-array.json>
- <https://ld4p.github.io/sinopia/schemas/0.0.1/resource-template.json>
- <https://ld4p.github.io/sinopia/schemas/0.0.1/property-templates-array.json>
- <https://ld4p.github.io/sinopia/schemas/0.0.1/property-template.json>

special bonus schema
- <https://ld4p.github.io/sinopia/schemas/0.0.1/profiles-array.json>


## Example ajv validation commands

The following commands validate use the [`ajv CLI library`](https://www.npmjs.com/package/ajv-cli) for JSON schema validation. However, there are [many available JSON Schema validation libraries in numerous languages](https://json-schema.org/implementations.html#validators); just make sure you select one that validates JSON Schema version draft-07.

#### Validate JSON instance against schema(s)

Note: if the schemas themselves aren't valid, the following commands will so indicate.

##### Validate a single file

```
$ ajv validate -s schemas/profiles-array.json -r 'schemas/*.json' -d profiles/v1/all_profiles.json

profiles/v1/all_profiles.json invalid
  [ { keyword: 'format',
      dataPath:
       '[3].Profile.resourceTemplates[1].propertyTemplates[0].valueConstraint.valueDataType.dataTypeURI',
      schemaPath:
       '#/properties/valueConstraint/properties/valueDataType/properties/dataTypeURI/format',
      params: { format: 'uri' },
      message: 'should match format "uri"' } ]
```

```
$ ajv validate -s schemas/profile.json -r 'schemas/*.json' -d "BIBFRAME 2.0 Place.json"

BIBFRAME 2.0 Place.json valid
```

##### Validate all files in a folder

```
$ ajv validate -s schemas/profile -r 'schemas/*.json' -d "profiles/*.json"

profiles/all_profiles.json invalid
[ { keyword: 'type',
    dataPath: '',
    schemaPath: '#/type',
    params: { type: 'object' },
    message: 'should be object' } ]
profiles/BIBFRAME 2.0 Admin Metadata.json valid
profiles/BIBFRAME 2.0 Agents Contribution.json valid
profiles/BIBFRAME 2.0 Agents Primary Contribution.json valid
profiles/BIBFRAME 2.0 Agents.json valid
profiles/BIBFRAME 2.0 Cartographic.json valid
profiles/BIBFRAME 2.0 DDC.json valid
profiles/BIBFRAME 2.0 Edition Information.json valid
profiles/BIBFRAME 2.0 Extra menus.json valid
profiles/BIBFRAME 2.0 Form.json valid
profiles/BIBFRAME 2.0 IBC.json valid
profiles/BIBFRAME 2.0 Identifiers.json valid
profiles/BIBFRAME 2.0 Item.json valid
profiles/BIBFRAME 2.0 Language.json valid
profiles/BIBFRAME 2.0 LCC.json valid
profiles/BIBFRAME 2.0 Load.json valid
profiles/BIBFRAME 2.0 Monograph.json valid
profiles/BIBFRAME 2.0 Moving Image-35mm Feature Film.json valid
profiles/BIBFRAME 2.0 Moving Image-BluRay DVD.json valid
profiles/BIBFRAME 2.0 Notated Music.json valid
profiles/BIBFRAME 2.0 Note.json valid
profiles/BIBFRAME 2.0 Place.json valid
profiles/BIBFRAME 2.0 Prints and Photographs.json valid
profiles/BIBFRAME 2.0 Publication, Distribution, Manufacturer Activity.json valid
profiles/BIBFRAME 2.0 Rare Materials.json valid
profiles/BIBFRAME 2.0 Related Works and Expressions.json valid
profiles/BIBFRAME 2.0 RWO.json valid
profiles/BIBFRAME 2.0 Serial.json valid
profiles/BIBFRAME 2.0 Series Information.json valid
profiles/BIBFRAME 2.0 Sound Recording-Analog.json valid
profiles/BIBFRAME 2.0 Sound Recording-Audio CD-R.json valid
profiles/BIBFRAME 2.0 Sound Recording-Audio CD.json valid
profiles/BIBFRAME 2.0 Title Information.json valid
profiles/BIBFRAME 2.0 Topic.json valid
profiles/PMO Medium of Performance.json valid
```

#### Validate schema itself

```
$ ajv compile -s schemas/property-template

schema schemas/property-template is valid
```

```
$ ajv compile -s schemas/profile

schema schemas/profile is invalid
error: can't resolve reference resource-templates-array from id profile#
```
