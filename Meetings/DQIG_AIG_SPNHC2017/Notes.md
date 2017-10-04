# Notes from the Joint Data Quality/Annotations interest group meeting at SPNHC 2017 #

* Notes are not comprehensive, and were taken in part by Arthur Chapman and in part by Paul J. Morris.

Attendees (by approximate order of introductions and location in the room): 

* Arthur Chapman DQIG Convener,  Australia
* Paul	Morris	AIG Convener, United States
* James Macklin	Agriculture Canada, Canada
* Greg Riccardi iDigBio, United States
* Janeen Jones  Field Museum, United States
* Kevin Love, iDigBio, United States
* Simon Checksfield CSIRO, Australia
* Edward Lockhart CDC, United States
* John Wieczorek MCZ, United States
* Joanna McCaffrey iDigBio, United States
* Henry Engledow Botanic Garden Meise, Belgium
* Matthew Collins iDigBio, United States
* Melissa Islam	Denver Botanic Gardens, United States
* Walter Berendsohn BGBM, Germany

Introductions

Introducing Biodiversity Data Quality IG
Regular meetings at TDWG and between TDWGs: Brazil, Monash Univ, Canberra.
GBIF, ALA, iDigBio agreeing on standard test suite

* TG1: Framework: Allan Viega
Developing a framework for describing data quality in the biodiversity domain.  Allan's Dissertation (see mathematical formulation therein) PLOS1 paper:  https://doi.org/10.1371/journal.pone.0178731

* TG2: Lee Belbin
Developing a Test suite

* TG3: Miles Nicols
Developing User Story to Use Case to themed Use Case to profile.

## Summary of Canberra Meeting ## 
Report of the meeting on the TDWG BDQ github wiki: (Transcript of meeting)
Allan’s work: Data Quality Profile: Links and details on wiki
Positive vs Negative assertions.  What are the problems in my data?  What qualities do I need to use this data.
Tests and assertions : positive and negative phrasings.  
Framework – phrased as positive, need to support parallel.
Framework is complex: Allan is developing documentation as Framework Lite (developing in the BDQ github presence).

Site for collecting profiles – not heavily used, under revision

TG2: DQ Tests:
Based on a set of principles
Cover a core set of darwin core terms.
Software comes and goes, tests should persist.
Spreadsheet of standard tests 
guid
standard name for test
Technical specification
darwin core term(s) involved
example
Implementations (sql, python, java).

Test Data Set
Test x has expected result for this test.
Probably a mix of real and synthetic data.

Use Case library
Emily Rees – collecting user stories, examining literature cases, developing use case library.   GBIF: forms for collecting user stories (11 questions), Allan, specialist tool for extracting use case from user story.   Not getting user stories from the community (thus tasking of Emily Rees).

Lee Belbin: GLOBIS project

Use of TDWG github presence.  
Key issue: non software developer user community, spreadsheets don’t fit well.
Direction: Final products in github, work products can be outside but linked.  Experimenting with how to use github for TDWG, working out how.  

John: Similar issues will arise in developing vocabularies.
Something to discuss at TDWG in Ottawa

Proposed TG4: Paula: Vocabularies.  Charter being written.  
48 of the tests reference a controlled vocabulary (which often don’t exist yet).

Historical data – need standard names for historical entities.

Walter: Need support for multiple languages

ISO standard for developing vocabularies, includes multilingual support.

First task for the TG, a scoping document.

Other vocabulary efforts ongoing in TDWG.

James: Services group, would like to see standardization, relevant to see standard services for vocabularies.
Arthur: Need more people involved with Paula’s TG

James: Largest challenge probably the curation of the vocabularies, people to take ownership and management of each vocabulary.

Arthur: One stop shop for locating vocabularies within TDWG, maintinance may not be outside. 

Joanne: Guidance for multilingual values for each term? 

Arthur: Something that needs to be discussed in the scoping document.


## Discussion of how to represent data quality assertions ##

Paul: Proposal from John W., add a Darwin Core extension for data quality assertions, have a short vocabulary derived from the framework (this is a validation, this is its identifier, this is the result asserted on this core record, this is status commentary, etc).

Discussion: Viewed by many in the room as highly problematic.  Issues include mixing data and data quality asserions in one Darwin Core archive document.  Unclear how to interpret Ammendments therein.  Overall consensus this isn't an approach to pursue.

Paul: Prov-O? 

Brief discussion, worth further investigation.

### Using the W3c annotation data model ###

Examined a handcrafted example (in text loosely approximating json-ld):


    {	
       @context: http://www.w3.org/ns/anno.jsonld
       id: urn:uuid:4592a7d32f27dc3db712285158458f07
       type: Annotation 
       motivation: 

Some of the list of W3C motivations may be appropriate.  If not, there is an easy extension mechanism for defining new ones.


       creator: {    
         type: Software
         id: urn:uuid:….
         name: Kurator-DateValidator 
       }
       created:
       generator:
       generated:

Discussion of metadata about the annotation, all seems straightforward.

Creator aligns with the Framework concept of Mechanism.       


      body: {
      }

Body is clearly where we would put the data quality assertions, would need to be able to serialize as json-ld (or another rdf serialization compatible with w3c annotations).  More later.

Target - how do we tell which data the assertions apply to.  For data represented as xml, quite straightforward, there is the xpath selector in the annotation data model (specify a data set which is in xml, then specify that the target of the annotation is a particular xpath).  Likewise if the data are a stable csv file, there is a csv selector to pick out a particular row from the file.  W3C annotation group considered data out of scope.  FilteredPush project proposed query selectors for annotating data (see doi:10.1371/journal.pone.0076093).  

W3C annotation data model includes a concept of a target of type Dataset.  If this data set is a single record (as in an identified rendering of an occurrence record on GBIF or iDigBio or ALA), then we could quite simply use the Dataset target.

Three ways to do this, one purely by reference, one by reference alone:

     target:
         type: Dataset,
         gbifRecordID: (pointer to versioned copy of record)
     }

Discussion: This requires resolution, reduces storage.  Storage may be a significant issue for large scale annotation of large data sets.  Can't tell in this case if the data has changed from the time the assertion in the annotation was made.  The annotation may or may not apply to the data when resolved.  Knowing values seen at the time of annotation viewed as important.

Or, by reference but including the darwin core terms in the record that are relevant to the measure/validation/ammendment in the body:

     target: {
         type: Dataset,
         gbifRecordID: (pointer to versioned copy of record),
         dwciri:occurrenceID: urn:uuid:205f3f79-512a-44a8-be35-76eef7b89c5d,
         dwc:day: 0
      }

Resolution possible, but no resolution needed to see the affected data, storage issue if affected terms include lots of data (as in higher taxonomy or higher geography). 

Or just consider the occurrenceId to be the reference to the data set, and leave locating the data set up to the consumer (as in the most general of the FP query selectors)

     target: {
         type: Dataset,
         dwciri:occurrenceID: urn:uuid:205f3f79-512a-44a8-be35-76eef7b89c5d
         dwc:day: 0
    }

No resolution possible unless occurrenceId is resolvable, storage issue if terms have much data.

Or embed the entire occurrence record (the state of the data at the time seen) in the data.

     target: {
         type: Dataset,
         dwciri:occurrenceID: urn:uuid:205f3f79-512a-44a8-be35-76eef7b89c5d
         {a full copy of the darwin core record at the time the annotation was created goes here}
     }

Including a full copy of the record obviously removes the need for resolution but is an obvious storage storage issue.  Discussion: This approach is probably untenable.  

For the body, the Kurator project's json serializations of data quality reports may provide a route to structure of data to go into the body.  Examples shown: 

#### DQ Report ####

    Assertion: Validation
    context 
        id: 48aa7d66-36d1-4662-a503-df170f11b03f
        name: DAY_IN_RANGE
        fieldsactedupon:   dwc:day
        fieldsconsulted: dwc:day
    dimension : Conformance
    specification: 
    mechanism  Kurator-Validation event-date-qc v1.0.3
    sources  (none)
    result {
       result NOT_COMPLIANT
       comments: Provided value for dwc:day of “0” is not in the range 1-31.
       Status: ASSERTED
    }

Mechanism in the body or the creator (at least body, may differ from creator)?

Initial values in the target or the body? (target, except for comment, no representation in report in framework)

Kurator-FFDQ(F2UF) proof of concept JSON serialization

    "ammendments" : [ {
      "recordId" : "MCZ:Herp:R-142502",
      "context" : {
         Id: test id
        "name" : "eventDateFromAtomicParts",
        "fieldsActedUpon" : [ "eventDate" ],
        "fieldsConsulted" : [ "verbatimEventDate", "startDayOfYear", "endDayOfYear", "year", "month", "day" ]
      },
      "specification" : "specification text",
      "mechanism" : "Kurator: DateValidator - Event date validator",
      "result" : {
        "initialValues" : {
          "month" : "",
          "verbatimEventDate" : "1968-1968",
          "year" : "",
          "endDayOfYear" : null,
          "startDayOfYear" : null,
          "eventTime" : null,
          "day" : "",
          "eventDate" : ""
        },	
        "curatedValues" : {
          "month" : "",
          "verbatimEventDate" : "1968-1968",
          "year" : "",
          "endDayOfYear" : null,
          "startDayOfYear" : null,
          "eventTime" : null,
          "day" : "",
          "eventDate" : "1968-01-01/1968-12-31"
        },
        "comments" : [ "Constructed event date from atomic parts." ],
        "status" : "FILLED_IN"
      },
      "sources" : null,
      "enhancement" : "Recommendation to fill in [eventDate] based on values from atomic fields [verbatimEventDate, startDayOfYear, endDayOfYear, year, month, day]"

