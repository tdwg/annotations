# Annotations Interest Group Meeting, TDWG 2016 #

## Participants ## 

* Alex Thompson
* Niels Klazenga
* Aaron Wilton
* Paul J. Morris
* Lee Belbin
* James Macklin
* Denné Reed
* Patricia Mergen
* Wouter Addink
* Greg Whitbread. 

## Notes ## 

AnnoSys successfull deployment and integration with GBIF.  Collected several hundred annotations.

ALA-Collecting Annotations, though not fed to GBIF.

Epandda – need for annotations which assert links between data objects

Need for social engagement with people who make annotations and people who curate data based on them – ALA sends email to data curator.

Annotations are being designed into DINA

Examined a skeletat W3C web annotation data model annotation:

    {	
       @context: http://www.w3.org/ns/anno.jsonld
       id: urn:uuid:4592a7d32f27dc3db712285158458f07
       type: Annotation 
       motivation: 
       creator: {    (Made the assertions)
           type: Software
           id:
           name: Kurator-DateValidator
       }
       created:
       generator:    ? scope of definition.
       generated:
       body: {
          curatedValues: 
       }
       target:
         type: Dataset
         selector: { 
       }
     }


Suggestion- oa:body, add a type, DWCDocument.  Add a type JSONBody.

Path forward: Action item: put an issue into the AIG github presence to draft a charter for TG.  Action item: send email to TDWG content about this issue soliciting interest.

Alternative view: Don’t need annotations for some use cases, just ability to represent assertions on DwC data.

Discussion of F2UF reports in annotations – simple case just put in body, but needs further deeper considerations, likely subtltes encountered in discussion.

Discuss with DQ IG TG for representation of fitness for use assertions.
