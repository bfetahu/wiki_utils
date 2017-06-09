# Wikipedia Article Utils

In this library, we developed techniques for parsing the content of Wikipedia articles. The input is either the content of a revision which is either in its original XML format or the same format converted to JSON. 

We developed several parsing mechanisms, which we outline below. 

```code
Besnik Fetahu, Katja Markert, Avishek Anand: 
Automated News Suggestions for Populating Wikipedia Entity Pages. CIKM 2015: 323-332
```

## Wikipedia Section Extractor

Here we disect the Wikipedia article into its composing parts, here the sections. We intentionally left the extraction of the sections to be configurable, such that one can extract only the head sections, or all the sectoins at the different depths, e.g. sub-sections, sub-sub-sections, etc.

```code
WikiEntity entity = WikiUtils.parseEntity("REVISION", isJson);
entity.parseContent();

for(String section_label:entity.getSectionKeys()){
  WikiSection section = entity.getSection(section_label);
}
```

## Wikipedia Citation Extractor

Here we extract the citations from the Wikipedia articles. We keep only the URL and the type of the citation in case such exist. For example, citations in Wikipedia can be of type news, book, web, etc., correspondingly, dependent on their type these might have a URL (e.g. news or web). 

We additionally extract the statements citing such references. Here we rely on a heuristic which we defined in the paper below, and is called the inter-citation text. However, the code can be easily modified to allow for coarse or finer grained statements.

```code
WikiEntity entity = WikiUtils.parseEntity("REVISION", isJson);
entity.setExtractReferences(true);
entity.setExtractStatements(true);
entity.parseContent();

Map<Integer, String[]> citations = entity.getEntityCitations();
for(int cite_id:citations.keySet()){
  //do something with the citations
}
```
## JSON-Schema

Below we show the json-schema we have defined to represent the different outputs we extract from the Wikipedia articles. The schema is meant to serve as a general reference for the possible structure of the extracted data. However, through our tool one can extract only specific parts of the data, for instance, extraction of the sections only, extraction of the citations only, extraction of the statements only, or extracting all possible parts from a Wikipedia article.


<ul>
<li>Sections Only</li>
<li>Citations Only</li>
<li>Statements and Citations</li>
<li>All of the above</li>
</ul>

The schema is available for download <a href="https://github.com/bfetahu/wiki_utils/blob/master/citation.json">here</a>. 


```code
WikiEntity entity = WikiUtils.parseEntity("REVISION", isJson);
entity.setExtractReferences(true);
entity.setExtractStatements(true);
entity.parseContent();

//Sections only
String output = entity.printSectionsOnly();

//Citations only
String output_citations = entity.printSectionCitationsOnly();

//Statements and citations
String output_statements = entity.printSectionStatementsOnly();

//Full output
String output_full = entity.printFullEntity();
```

