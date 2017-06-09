# Wikipedia Article Utils

In this library, we developed techniques for parsing the content of Wikipedia articles. The input is either the content of a revision which is either in its original XML format or the same format converted to JSON. 

We developed several parsing mechanisms, which we outline below. 

## Wikipedia Section Extractor

Here we disect the Wikipedia article into its composing parts, here the sections. We intentionally left the extraction of the sections to be configurable, such that one can extract only the head sections, or all the sectoins at the different depths, e.g. sub-sections, sub-sub-sections, etc.

## Wikipedia Citation Extractor

Here we extract the citations from the Wikipedia articles. We keep only the URL and the type of the citation in case such exist. For example, citations in Wikipedia can be of type news, book, web, etc., correspondingly, dependent on their type these might have a URL (e.g. news or web). 

We additionally extract the statements citing such references. Here we rely on a heuristic which we defined in the paper below, and is called the inter-citation text. However, the code can be easily modified to allow for coarse or finer grained statements.
