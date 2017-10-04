# Data Quality Assertions in the W3C annotation data model #

## An example data quality assertion ##

Some notes: 

* relevant motivations: assessing (definition includes "assess the quality of a dataset"), editing (for ammendments, requesting a change to the target resource), identifying (for ammendments which propose an IRI value for a dwc term), moderating (could be used for measures, definition includes "assign some value or quality to the target"). 

* This example is synthetic, urn:catalog:MCZ:Mala:120551 has a valid eventDate value of 1922-01-01/1924-12-31.

* This example uses a target of type dataset, where the dataset consists of a single record (identifiable by an identifier at GBIF and an occurrenceId), if stable identifiers exist for single records as datasets, then target of type dataset can be used rather than some form of query selector.  The value of the darwin core term that was assessed by the validation is included so that a lookup isn't needed to retrieve it.  An IRI for the dataset is included to enable lookup.

* The body could include additional metadata from the framework about the Validation (the Specification, CriterionInContext, etc.), or, as here, just a limited set of metadata and a guid that might be used to discover more metadata (though the current guids for tests in TG2 are uuids without a resolution mechanism.

* Terms without prefixes need further consideration.

Handcrafted, not entirely correct json-ld for discussion purposes:

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

