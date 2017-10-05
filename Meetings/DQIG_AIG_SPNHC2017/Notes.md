# Notes from the Joint Data Quality/Annotations interest group meeting at SPNHC 2017 #

SPNHC pre-meeting full day workshop, held 2017-June-18 in Denver, CO, USA.

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

## TG1, the Framework ##

There have been repeated discussions of what to call the report element Allan originally called Enhancement.

“Enhancement” may not work with some audiences.  For example if you ask  a curator top enhance their data they will get angry  (amendment better).

James:  Don’t need to feed back all terminology to curator – amendment

Must use common terminology.

Walter “Enhancement actually adds data” therefore Enhancement may be a true Enhancement.

Enhancement – means better … - it might not make data better – may not be an improvement.

“Enrichment”

“Measures” not Measure in Glossary of terms.

Training exercise to interpret the need for Enhancement (tied to user needs) and Amendment – related to the Quality.

Raised – problem of institutions generalising their export (drop the seconds for example) but not changing the Precision or Uncertainty in meters.

NB Suggested that not use data custodian – data provider (Allan uses data holder)

Dimension:

NB In Glossary of Terms 

DQ Dimension “precision” should be “resolution”

## Discussion of TG2 Tests ## 

Paul: Extracted from GBIF – all records where latitude and longitude inverted. Ran Kurator workflow on them.  Results don't agree. Key problem: Different tests give different answers

How do we present the output of tests to the user.

W3C – can have a conversation of annotations.

How can we represent the annotations from the DQ reports in useful ways

Day=O Day Consistent with Month/Year:  DATA_PREREQUISIT_NOT_MET

Sequencing important – Day=O test before consistent with Month/Year.

Order of tests – a graph if not done in an order could get different results.

Rule set – if this test fails then there is no need to run these other tests as they won’t work anyway
(e.g. latitude out of range then centre of country/terrestrial etc. outliers tests are redundant

## Discussion of how to represent data quality assertions ##

Greg: confusion between IPT and DwC

Greg: If want in a DwCArchive need a more straight forward -IPT) – better than trying to shoehorn into another set of definitions.

Lots of discussion on best way to transmit Annotations

Paul: Proposal from John W., use Darwin Core Measurement or Fact for data quality assertions, have a short vocabulary derived from the framework (this is a validation, this is its identifier, this is the result asserted on this core record, this is status commentary, etc).

John Wieczorek

DarwinCore: MeasurementOrFact

Definition: A measurement of or a fact about a …”see Pauls slides)

#measurementID
#measurementType Data Quality Validation (Validation|measure|Amendment) careful about vocabulary DQmeasure?
#measurementValue COMPLIANT (COMPLIANTNOT COMPLIANT)
#measurementAccuracy
#measurementUnit
#measurementDeterminedBy -DQFramework:Mechanism” “event_date_qc v1.03  DwCEventQC
#measurementSeterminedDate
#measurementMethod DAY_IN_RANGE: 48aa7d66-36d1 ……
#measurementRemarks Provided value for dwc:day of “10” is in the range 1-31

Problem or order
Can’t send an annotation of an annotation

Reasons not to do above (overloading of measurementOfFact) Not flat and trying to force into Flat format /confusing to users)

Discussion: Viewed by many in the room as highly problematic.  Issues include mixing data and data quality asserions in one Darwin Core archive document.  Representing not-flat structure from framework as flat, no mechanism to annotate the annotations. Unclear how to interpret Ammendments therein.  Overall consensus this isn't an approach to pursue.

### Prov-o? ###

W3C Prov – representation of Prevenance  The things we have done – worth further and deeper investigation.

May be good mechanism for describing where data quality reports have come from.

See Bertram L. and see if a student can ….
Entity  <>  Activity  <>  Agent

May be a good way of describing all entitities  [CHASE UP]
	Work flow description

Brief discussion, W3C Prov-o is worth further investigation.

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


Annotation: Time/who/when – Target -Body

One Annotation can have as its target another Annotation – conversation of annotation assertions
An annotation on a data record can be treated as an issue (like bug tracking)
A subsequent annotation can mark the first annotation as resolved (or as a won’t fix)

W3C about documents on the Web – not about data

So would have to extend  the PathSelector mechanism to refer to Data rather than a document
Query – why not pack with GUIDs rather than use Selector?PathSelector too application specific.

Could do that.	

Walter – why not store the record and the annotation together.

How are these going to be delivered?
