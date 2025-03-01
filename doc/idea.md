
# Agent IA Software Requirement Specification Reviewer

ChatGPT Operator avec ?? pour relire et ameliore Software Requirement Specification

# structure du document

Architecture Snapshot

<<It shall give an overview about the sub-system impacted by this documentation and should be have a reference to the architecture document, using the same denomination.>>

Functional Requirements

<<. List the functional requirements associated sort by this feature.
The requirements that are Risk Control Measures should be specifically identified.
Include error handling requirements: how the software shall respond to anticipated system errors or use errors.>>

Operational Requirements

Interaction

<< It describes alarm, warning and operator message sequences driven by the software system.
It describes user action/system response.
How the software shall respond to anticipated system errors or use errors.>>

Interfaces

<<It describes links between the software system and the other system>>



# Format d'un requirement

[ES-XXX-SRS-0002] Requirement title 2

The software shall respond to user commands within 0.005 seconds, measured from the moment the command is received by software to the moment the consequent action (e.g. motor control action) is activated. This excludes the hardware delays that are quantified in the hardware spec.  This responsiveness is required to fulfill the system requirement of <TBD>.

 [REF HFN-XXX-DIE-0002] [STATUS ACTIVE] [REV 02]

# Critere d'evaluation d'un requirement

| Characteristic | 	Explanation |
|----------------|---------------|
| Unitary (Cohesive) | 	The requirement addresses one and only one thing.| 
| Complete| 	The requirement is fully stated in one place with no missing information.| 
| Consistent| 	The requirement does not contradict any other requirement and is fully consistent with all authoritative external documentation.| 
| Non-Conjugated (Atomic)| 	The requirement is atomic, i.e., it does not contain conjunctions. E.g., "The postal code field must validate American and Canadian postal codes" should be written as two separate requirements: (1) "The postal code field must validate American postal codes" and (2) "The postal code field must validate Canadian postal codes". | 
| Traceable| 	The requirement meets all or part of a business need as stated by stakeholders and authoritatively documented.| 
| Current	| The requirement has not been made obsolete by the passage of time. | 
| Unambiguous| 	The requirement is concisely stated without recourse to technical jargon, acronyms (unless defined elsewhere in the Requirements document), or other esoteric verbiage. It expresses objective facts, not subjective opinions. It is subject to one and only one interpretation. Vague subjects, adjectives, prepositions, verbs and subjective phrases are avoided. Negative statements and compound statements are avoided. | 
| Specify Importance	| Many requirements represent a stakeholder-defined characteristic the absence of which will result in a major or even fatal deficiency. Others represent features that may be implemented if time and budget permits. The requirement must specify a level of importance.| 
| Verifiable	| The implementation of the requirement can be determined through basic possible methods: inspection, demonstration, test (instrumented) or analysis (to include validated modeling & simulation).| 

# Tips

AI Crew Manager ?



