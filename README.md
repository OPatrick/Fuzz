Fuzz
====

This application is intended for generating testing data files.
Today is supported generation of XML files from XSDs (1.0)

Planned:

•generate SQL inserts and/or database schemas from XSDs

•generate simple equivalent XSD from several complex XSDs (solving include, import, override, redefine, substitution groups, abstract, attributes groups, element groups, extensions, restrictions)

•generate simple XSD from database schema

•generate XML data files from Database Schemas

 

This generator does NOT check for XSD conformity

XSD 1.0 partially supported

Not supported xsd tags:

•any | anyAttribute | any attributes with non-schema Namespace

•schema facets: ◦explicitTimezone,

◦totalDigits, fractionDigits,

◦RegExp pattern,

◦whiteSpace

•complexType: block & final attributes

No incidence xsd tags:

•appinfo | mixed content

Namespace resolution policy for generated XML file:

•Schema targetNamespace will be the default namespace for generated XML

•Non default namespaces in included or imported XSDs are added to generated XML

•Default namespace of included XSDs are replaced by main schema targetNamespace, but should be the same

•Default namespace of imported XSDs are replaced by namespace given in import instruction and the last ones are added to generated XML

•Namespaces given in "redefine" and "override" instructions replace default namespaces of target XSD classes, and are added to generated XML

•Check is done for namespace unicity

•Uri are listed alphabetically and then prefixes are generated incrementally for them: ns1, ns2...

Qualification resolution policy for generated XML file:

•When a schema has no target namespace (enclosing schema or imported schema), the elements used from it are unqualified

•When a node is set unqualified but its parent have an implicit qualification (xmlns="some uri"), then that node is given the following empty attribute: xmlns=""

•Schema attributesFormDefault & elementFormDefault values may be overridden by user settings in the &quot;Override&quot; pane

•When a schema (main or imported) does not have a targetNamespace, generated xml for those elements/attributes will not have any prefix (unqualified)

•When a schema has a target namespace, but no default namespace: ◦global elements will be prefixed

◦local elements & attributes might be prefixed or not, based on schema wide info, eventually overridden by user settings, eventually overridden by local form info

•When import instruction does not supply namespace, imported elements are unqualifed

•When elementFormDefault (or its user override) is set to "unqualified": ◦Only root elements defined within a schema will be qualified

◦All types that are defined inline (locally) will NOT be qualified


@author: Patrick Brouillé <patrick@brouille.net> 
