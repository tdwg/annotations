# Annotations Interest Group Meeting TDWG 2017 #

Present: Lutz Suhriber, Paul Morris, Okka Tschoepe, Alex Thompson, Arthur Chapman. 

Introductions.

Alex Thomoson as new Co-Convener.

Question raised by Walter B. Merge the annotations IG into DQ IG.

Discussion: Overlap, but distinct.  Arthur and Alex don't see them merging.  

Some notes from SPNHC:

Reviewed using W3C annotation data model assertion wrapping a data quality assertions.  Seen as good fit, some details to be worked out.

Looked at using measurement or fact to record annotations.  Viewed as not a good idea.

Alex: Reverse: map measurement or fact and resource relationship into annotations - assert reslurce relations as 

Annotations into vocabulary suggested by John W.

Alex: Who adds things to vocabularies.  Life Stage vocabulary.  Every addition to vocabulary gets an annotation indicating the source.

Arthur Advanatage of annotations 

Lutz: Using annotations of annotations in AnnoSys, ultimately up to the curator to accept or act on.

Arthur: Avoiding repeated annotations of potentially problematic data that are actually not problematic, benefits both consumers of data and curators of data.

Alex: Scope of Annosys? 

Lutz: Annosys: As propagator of messages.

Alex: To what extent is Annosys able to update source databases?

Lutz: No access to the source database - difficulties with schema mapping.

Acton Item (create issue): Propose a Task Group charter for an Applicability Statement about the W3C annotation data model and use cases/best practices for data quality assertions using the W3C annotation data model.

## Example DQ assertion in W3C annotation ##

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

