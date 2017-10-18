# Annotations Interest Group Meeting TDWG 2017 #

Present: Lutz Suhriber (BGBM), Paul J. Morris (MCZ), Okka Tschoepe (BGBM), Alex Thompson (iDigBio), Arthur Chapman (BDQIG Convener). 

Introductions.

Introduced Alex Thompson as new Co-Convener.

Question raised by Walter Berendsohn: Merge the annotations IG into DQ IG?

Discussion: Overlap, but distinct.  Arthur and Alex don't see them merging.  Consensus, keep as distinct interest groups. 

Some notes from SPNHC:

Reviewed using W3C annotation data model assertion wrapping a data quality assertions.  Seen as good fit, some details to be worked out.

Looked at using measurement or fact to record annotations.  Viewed as not a good idea.

Alex: Reverse: map measurement or fact and resource relationship into annotations - assert resource relations as 

Using annotations for managing provenance of additions into vocabulary has been suggested by John Wieczorek.

Alex: Who adds things to vocabularies.  Life Stage vocabulary.  Every addition to vocabulary gets an annotation indicating the source.

Arthur: Key advanatage of annotations is ability to conduct annotation conversations.

Lutz: Using annotations of annotations in AnnoSys, ultimately up to the curator to accept or act on.

Arthur: Avoiding repeated annotations of potentially problematic data that are actually not problematic, benefits both consumers of data and curators of data.

Alex: Scope of Annosys? 

Lutz: We see AnnoSys as propagator of messages.

Alex: To what extent is Annosys able to update source databases?

Lutz: No access to the source database - difficulties with schema mapping.

Discussion of FilteredPush schema mapping into Specify6.  Three complexities: exchange schema concept to field mappings that aren't one to one (one term mapping to more than one field or vice versa), mapping exchance schema onto relations in relational database (need to locate specimen record, locate taxon record, add an identification record, etc., including understanding of the buisness logic), and need to provide values for required fields where data is not present in the annotation (e.g. add a family in order to add a genus in order to add a species to use in an identification).  Overall needs deep knowledge of the database schema and the exchange schema.  Non-trivial, but possible to do on a single database schema to exchange schema mapping, much harder problem to generalize. 

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

