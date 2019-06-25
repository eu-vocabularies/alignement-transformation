# alignement-transformation
Transformation of alignment file using the "alignement ontology" into a standard alignment format for publication

## Introduction
This describe the mapping done to transform the alignment files coming from a system using the 
"Alignment Ontology" (from the INRIA) into a skos alignement file ready to be published.
This work is uncomplete and will be improved following the needs.

## Mapping

1. Namespaces

align: <http://knowledgeweb.semanticweb.org/heterogeneity/alignment#>
rdf:   <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
rdfs:  <http://www.w3.org/2000/01/rdf-schema#>
owl:   <http://www.w3.org/2002/07/owl#>
skos:  <http://www.w3.org/2004/02/skos/core#>
dc:    <http://purl.org/dc/elements/1.1/>
xsd:   <http://www.w3.org/2001/XMLSchema#">

2. Relationship between relationships 

Original version| Decription |Action	|Converted properties	| Converted resource	| Note
---|----|----|----|----|----|
 align:level	| Specific to EDOAL	 |removed	|-|	-|	
 align:map|	 Correspondance between entities of the ontologies|	removed |	-	| -	|
align:onto1	| URI of the 1st ontology	| keep as-is |	align:onto1 |	-	|
 align:onto2	| URI of the 2nd ontology	| keep as-is |	align:onto2	|-	|
 align:entity1 | The first aligned ontology entity	converted to| - |	skos:Concept	|
align:entity2	| The second aligned ontology entity	|converted to	|-	|skos:Concept	|
 align:relation	| Identify a relation between ontology entities
(> (subsumes), < (is subsumed), = (equivalent), % (incompatible), HasInstance, InstanceOf) |	converted to |	skos:exactMatch / skos:closeMatch |	-	|
 align:measure	|the confidence that the relation holds between the first and the second entity. |	removed	|-|	- |	Only the alignment with  a measure of 1.0 will be converted. | 
align:type |	the type of arity of alignement (total, partial, injective, surjective)	| removed (used for information) |	- |	- |
 align:status	|	removed	| -	| -	|
 align:mappingProperty	|	removed	| -	 |-	|
 
## Example

 1.Example (source file)
 
    <?xml version="1.0" encoding="UTF-8"?>
    <rdf:RDF
     xmlns:rdfs="http://www.w3.org/2000/01/rdf-schema#"
     xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#">

     <rdf:Description rdf:nodeID="node1d3oo5fj9x1">
     <level xmlns="http://knowledgeweb.semanticweb.org/heterogeneity/alignment#" rdf:datatype="http://www.w3.org/2001/XMLSchema#string">0</level>
     <map xmlns="http://knowledgeweb.semanticweb.org/heterogeneity/alignment#" rdf:nodeID="node1d3oo5fj9x1296"/>
     <map xmlns="http://knowledgeweb.semanticweb.org/heterogeneity/alignment#" rdf:nodeID="node1d3oo5fj9x1297"/>
     <map xmlns="http://knowledgeweb.semanticweb.org/heterogeneity/alignment#" rdf:nodeID="node1d3oo5fj9x1298"/>           
     <map xmlns="http://knowledgeweb.semanticweb.org/heterogeneity/alignment#" rdf:nodeID="node1d3oo5fj9x1299"/>
      
     <onto1 xmlns="http://knowledgeweb.semanticweb.org/heterogeneity/alignment#" rdf:resource="http://data.europa.eu/uxp/"/>
     <onto2 xmlns="http://knowledgeweb.semanticweb.org/heterogeneity/alignment#" rdf:resource="http://eurovoc.europa.eu/"/>
      
     <type xmlns="http://knowledgeweb.semanticweb.org/heterogeneity/alignment#" rdf:datatype="http://www.w3.org/2001/XMLSchema#string">??</type>
         <rdf:type rdf:resource="http://knowledgeweb.semanticweb.org/heterogeneity/alignment#Alignment"/>
     </rdf:Description>
  
     <rdf:Description rdf:nodeID="node1d3oo5fj9x1296">
     <entity1 xmlns="http://knowledgeweb.semanticweb.org/heterogeneity/alignment#" rdf:resource="http://data.europa.eu/uxp/3683"/>
     <entity2 xmlns="http://knowledgeweb.semanticweb.org/heterogeneity/alignment#" rdf:resource="http://eurovoc.europa.eu/3683"/>             
     <measure xmlns="http://knowledgeweb.semanticweb.org/heterogeneity/alignment#" rdf:datatype="http://www.w3.org/2001/XMLSchema#float">1.0</measure>           
     <relation xmlns="http://knowledgeweb.semanticweb.org/heterogeneity/alignment#" rdf:datatype="http://www.w3.org/2001/XMLSchema#string">=</relation>
     <rdf:type rdf:resource="http://knowledgeweb.semanticweb.org/heterogeneity/alignment#Cell"/>
     </rdf:Description>
  
     <rdf:Description rdf:nodeID="node1d3oo5fj9x1296">      
     <mappingProperty xmlns="http://knowledgeweb.semanticweb.org/heterogeneity/alignment#" rdf:resource="http://www.w3.org/2004/02/skos/core#exactMatch"/>     
     <status xmlns="http://knowledgeweb.semanticweb.org/heterogeneity/alignment#" rdf:datatype="http://www.w3.org/2001/XMLSchema#string">accepted</status>
    </rdf:Description>
    
    </rdf:RDF>

 
 2. Result file
 

     <?xml version="1.0" encoding="UTF-8"?>
     <rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#">
     <rdf:Description rdf:about="http://data.europa.eu/uxp/">  
         <rdf:type rdf:resource="http://knowledgeweb.semanticweb.org/heterogeneity/alignment#Ontology"/>
     </rdf:Description>
      
     <rdf:Description rdf:about="http://eurovoc.europa.eu/">   
         <rdf:type rdf:resource="http://knowledgeweb.semanticweb.org/heterogeneity/alignment#Ontology"/>
     </rdf:Description>
      
     <rdf:Description rdf:about="itm:n#_405787">   
         <rdf:type rdf:resource="http://knowledgeweb.semanticweb.org/heterogeneity/alignment#alignment"/>  
         <onto1 xmlns="http://knowledgeweb.semanticweb.org/heterogeneity/alignment#" rdf:resource="http://data.europa.eu/uxp/"/>   
         <onto2 xmlns="http://knowledgeweb.semanticweb.org/heterogeneity/alignment#" rdf:resource="http://eurovoc.europa.eu/"/>
     </rdf:Description>
      
     <rdf:Description rdf:about="http://data.europa.eu/uxp/3683">  
         <exactMatch xmlns="http://www.w3.org/2004/02/skos/core#" rdf:resource="http://eurovoc.europa.eu/3683"/>
     </rdf:Description> 
     </rdf:RDF>


