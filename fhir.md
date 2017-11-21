# FHIR

As a healthcare organization, a lot of our work deals with storing and analyzing complex healthcare data. For this, we depend on the [FHIR](https://www.hl7.org/fhir/) standard. FHIR (Fast Health Interoperability Resources) is an HL7 specification for Healthcare Interoperability.

What does that mean to you right now? Probably not too much (unless it does, in which case bonus points for you). That being said, it's a long, relatively complicated set of documentation to read and learn, so for the sake of our technical test we are going to focus on one small part; the [patient](https://www.hl7.org/fhir/patient.html) object.

## Nuts and Bolts

To import the necesary library components for fhir, use the following import in your build.gradle file:

```groovy
    compileOnly 'ca.uhn.hapi.fhir:hapi-fhir-structures-dstu3:3.1.0-SNAPSHOT'
```
The dependency comes from Maven Central, which should automatically in the new project your create. If you are having issues, the entry in the Maven repository browser is [here](https://mvnrepository.com/artifact/ca.uhn.hapi.fhir/hapi-fhir-structures-dstu3/3.0.0). This will contain the necessary objects for this demo application.

## Patient

So, people are complicated, so natually the model that represents them is going to have a lot going on. Let's take a quick look at the JSON representation of the model ->

```
{
  "resourceType" : "Patient",
  // from Resource: id, meta, implicitRules, and language
  // from DomainResource: text, contained, extension, and modifierExtension
  "identifier" : [{ Identifier }], // An identifier for this patient
  "active" : <boolean>, // Whether this patient's record is in active use
  "name" : [{ HumanName }], // A name associated with the patient
  "telecom" : [{ ContactPoint }], // A contact detail for the individual
  "gender" : "<code>", // male | female | other | unknown
  "birthDate" : "<date>", // The date of birth for the individual
  // deceased[x]: Indicates if the individual is deceased or not. One of these 2:
  "deceasedBoolean" : <boolean>,
  "deceasedDateTime" : "<dateTime>",
  "address" : [{ Address }], // Addresses for the individual
  "maritalStatus" : { CodeableConcept }, // Marital (civil) status of a patient
  // multipleBirth[x]: Whether patient is part of a multiple birth. One of these 2:
  "multipleBirthBoolean" : <boolean>,
  "multipleBirthInteger" : <integer>,
  "photo" : [{ Attachment }], // Image of the patient
  "contact" : [{ // A contact party (e.g. guardian, partner, friend) for the patient
    "relationship" : [{ CodeableConcept }], // The kind of relationship
    "name" : { HumanName }, // A name associated with the contact person
    "telecom" : [{ ContactPoint }], // A contact detail for the person
    "address" : { Address }, // Address for the contact person
    "gender" : "<code>", // male | female | other | unknown
    "organization" : { Reference(Organization) }, // C? Organization that is associated with the contact
    "period" : { Period } // The period during which this contact person or organization is valid to be contacted relating to this patient
  }],
  "animal" : { // This patient is known to be an animal (non-human)
    "species" : { CodeableConcept }, // R!  E.g. Dog, Cow
    "breed" : { CodeableConcept }, // E.g. Poodle, Angus
    "genderStatus" : { CodeableConcept } // E.g. Neutered, Intact
  },
  "communication" : [{ // A list of Languages which may be used to communicate with the patient about his or her health
    "language" : { CodeableConcept }, // R!  The language which can be used to communicate with the patient about his or her health
    "preferred" : <boolean> // Language preference indicator
  }],
  "generalPractitioner" : [{ Reference(Organization|Practitioner) }], // Patient's nominated primary care provider
  "managingOrganization" : { Reference(Organization) }, // Organization that is the custodian of the patient record
  "link" : [{ // Link to another patient resource that concerns the same actual person
    "other" : { Reference(Patient|RelatedPerson) }, // R!  The other patient or related person resource that the link refers to
    "type" : "<code>" // R!  replaced-by | replaces | refer | seealso - type of link
  }]
}
```

**Oh boy**, that's a lot going on there. For the sake of this test, let's focus on three fields: 

```
  "name" : [{ HumanName }], // A name associated with the patient
  "gender" : "<code>", // male | female | other | unknown
  "birthDate" : "<date>", // The date of birth for the individual
```

Not so complicated now, right? We know the patient has three fields we care about:

* "name" -> The name of the patient we are working with. This is stored as an instance of the datatype [HumanName](https://www.hl7.org/fhir/datatypes.html#HumanName)
* "gender" -> The gender of the patient. This is stored as an [AdministrativeGender](https://www.hl7.org/fhir/valueset-administrative-gender.html)
* "birthday" -> The date of birth for the patient. Stored as a date object.

Our example app will center around the modification of these three fields.
