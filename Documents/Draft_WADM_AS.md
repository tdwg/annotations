# Draft Applicability Statement on the W3C Web Annotation Data Model #

This is a very draft start on a document eventually intended for a TDWG standards track, possibly as an Applicability Statement (AS).  It is currently very much in draft form, is in no way normative, and may change at any time.

The upper case key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

## Web Annotation Data Model ##

In February 2017 the World Wide Web Consortium (W3C) published the Web Annotation Data Model https://www.w3.org/TR/annotation-model as a recommendation.  

"The Web Annotation Data Model provides an extensible, interoperable framework for expressing annotations such that they can easily be shared between platforms, with sufficient richness of expresson to satify complex requirements while remaining dimple enough to also allow for the most common use cases, such as attaching a piece of text to a singe web resource."  (Sanderson et al., 2017).

The Web Annotation Data Model SHOULD be used to represent annotations of data objects in the biodiversity domain.

In botany, the term Annotation has long been used to describe the addition of information to herbarium sheets by botansts.  Botanical annotations are often new determinations of the scientific name to be applied to a specimen on a herbarium sheet, or an expression of concurrence by a specialist with an existing determinations, and in some cases, corrections or supplements to other information on the sheet.  Botanical annotations are sometimes handwritten on the herbarium sheet, or somtimes provided on separate pieces of paper that are affixed to the herbarium sheet.  Herbaria vary in their practices regarding aligning the identification history recorded in annotations on the herbarium sheet with the identification history for that sheet stored in the database of record for that herbarium.  

Botanical annotations are subset of the kinds of assertions that can be represented in biodiversity informatics on biodiversity data objects.  Care should be taken when discussing annotations with botanists as the term may carry a connotation for them of identifications that are physically associated with a herbarium sheet, and they may percieve a requirement that all annotations be physically associated with the herbarium sheet.

## Serialization and Transport ##

The Web Annotation data model has a preferred serialization of JSON-LD, with a media type of applcation/ld+json;profile="http://www.w3.org/ns/anno.jsonld"  Biodiversity uses MAY serialize annotations as JSON-LD.   In a separate recommendation, the W3C also provides a specification for a transport protocol for annotations (Sanderson, 2017).  This annotation protocol MAY be used in biodiversity information systems.

## Creator and Generator ##

The agent responsible for making the assertions in the body of the annotation SHOULD be recorded as the anno:creator of the annotation.  This annotator could be a human or software agent.  When a human is executing software where the logic in the software is responsible for making the assertions in the body of the annotation, the software SHOULD be asserted as the anno:creator. 

The point in time at which the assertions in the body of the were made SHOULD be asserted as the anno:created.

The agent responsible for creating the initial serialization of the annotation SHOULD be recorded as the anno:generator of the annotation.  The creator SHOULD be a software agent, unless the annotation was written by hand by a human.

The point in time at which the annotation was initially serialized made SHOULD be asserted as the anno:generated.

## Motivations ##

Annotations SHOULD assert a motivation.

The motivation "assessing" MAY be used as the motivation for data quality annotations that assert validation results on data. 

The motivation "identifying" SHOULD be used as the motivation for an annotation which proposes an IRI value  as an update of an annotated data record, for example, an annotation which proposes a value for dwciri:taxonId on the basis of the value of dwc:scientificName in the record should use the motivation "identifying".

The motivation "moderating" MAY be used as the motivation for data quality annotations that assert measues of data quality on data.

The motivation "editing" SHOULD be used as the motivation for an annotation which proposes a change to a data record.

## Targets ## 

Annotations on individual biodiversity data records SHOULD have a target of type anno:Dataset, where the Dataset is an identified single record.  

Annotations on individual biodiversity data records MUST include the guid for the individual record in the target.  

For example, an annotation of an Occurrence should have a target of type anno:Dataset and should include the dwciri:occurrenceID for the annotated occurrence record.

The target of the annotation SHOULD include a copy of any data in the original record to which the annotator proposes a change.  For example, an annotation proposing a new value for dwc:geodeticDatum in the annotation body should include in the target of the annotation the original value of dwc:geodeticDatum in the anotated record at the time of the creation of the annotation. 

The target of the annotation MAY include a full copy of the data in original record at the time of annotation.

When a versioned, resolvable, persistent identifier from which the data record at the time it was annotated is available, then the target of the annotation MAY assert only that identifier in the target of the annotation.

## An example data quality assertion ##

Very draft, started from this document, probably doesn't belong in the applicability statement.

Some notes: 

* This is hand crafted, not entirely valid json-ld, currently for discussion purposes only.

* This example is synthetic, urn:catalog:MCZ:Mala:120551 has a valid eventDate value of 1922-01-01/1924-12-31.

* This example uses a target of type dataset, where the dataset consists of a single record (identifiable by an identifier at GBIF and an occurrenceId), if stable identifiers exist for single records as datasets, then target of type dataset can be used rather than some form of query selector.  The value of the darwin core term that was assessed by the validation is included so that a lookup isn't needed to retrieve it.  An IRI for the dataset is included to enable lookup.

* The body could include additional metadata from the biodiversity fittnes for use framework about the Validation (the Specification, CriterionInContext, etc.), or, as here, just a limited set of metadata and a guid that might be used to discover more metadata (though the current guids for tests in TG2 are uuids without a resolution mechanism).

* Terms without prefixes need further consideration.

    {
         @context: { "anno" : "http://www.w3.org/ns/anno.jsonld" }
         @context: { "ffdq" : "http://example.org/ffdq/" }
         @context: { "dwc" : "http://rs.tdwg.org/dwc/terms/" }
         @context: { "dwciri" : "http://rs.tdwg.org/dwc/iri/" }

         @id: urn:uuid:4592a7d32f27dc3db712285158458f07
         @type: "anno:Annotation"
         "anno:motivation": "anno:assessing"
         "anno:creator": {    
             @id: urn:uuid:b844059f-87cf-4c31-b4d7-9a52003eef84
             "anno:type": Software
             "anno:name" : "Kurator: Date Validator - DwCEventDQ" 
         }
         "anno:created" : "2017-10-04"
         "anno:generator" : "hand written"
         "anno:generated" : "2017-10-04"
         "anno:body" : {
               "ffdq:Report" : { 
                   "ffdq:Validation" : { 
                      @id: urn:uuid:f413594a-df57-41ea-a187-b8c6c6379b45,
                      label: "EVENT_DATE_EXISTS",
                      "ffdq:Result" : { 
                         "ffdq:resultStatus" : "NOT_COMPLIANT",
                         "ffdq:resultState" : {
                             state: ASSERTED,  
                             comment : “Provided value for dwc:eventDate '1922-01.01' is not formated as an ISO date. "
                         }
                      }, 
                      "ffdq:informationElement" : [ "dwc:eventDate" ]
                   } 
              }
         }
         "anno:target" :
             @type: "anno:Dataset"
             { 
                  gbifRecordID: { 
                     @id : "https://www.gbif.org/occurrence/476960560" 
                  },
                  "dwciri:occurrenceID" : "urn:catalog:MCZ:Mala:120551",
                  "dwc:eventDate" : "1922-01.01"
             }
    }


## Best Practices for Some Biodiversity Uses ##

### Identifications ###

Annotations can be used to carry the assertions made by specialists in associating a scientific name with a biodiversity record.

Motivation SHOULD NOT use use "identifying", unless a dwciri term carrying a guid is asserted in the body.

Motivation for new identifications should use :determining.

### Transcriptions and Corrections ###

Annotations can be used to carry subsequent transcriptions from images of written records by data entry personnel the historical assertions made by specialists in associating a scientific name with a biodiversity record.  This form of annotation MUST be diestinguished from similar annotations which assert assertions made directly by specialists. 

Motivation for transcriptions SHOULD use :transcribing.

Body of transcriptions: dwc:identifiedBy as the transcribed name of the person who made the identification.  Annotation anno:creator the person who made the transcription.

### Biodiversity Data Quality Assertions ###

Motivation dependng on data quality assertions included in the body of the annotation (measure, validation, ammendment, issue).

### Semantic markup of Images ###

Target, selector, as described.

# Vocabulary for biodiversity motivations # 

transcribing, entry of data from paper records into electronic form.

determining, applying a scientific name to a biodiversity data object.

# Contributors #

Paul J. Morris, Museum of Comparative Zoology

# Citations #


Bradner, S. 1997. Network Working Group Request for Comments: 2119; Key words for use in RFCs to Indicate Requirement Levels.  IETF Best Current Practice.  https://ietf.org/rfc/rfc2119.txt

Sanderson, R., Ciccarese, P., Young B. eds. 2017.  Web Annotation Data Model, W3C Recommendation.  https://www.w3.org/TR/annotation-model/ 

Sanderson, R. ed., 2017. Web Annotation Protocol W3C Rccommendation https://www.w3.org/TR/annotation=protocol/ 


