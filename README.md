# MA21_QA_Team_Abhinav
JIRA TICKET HHS-30658
COMMONWEALTH OF MASSACHUSETTS
EXECUTIVE OFFICE OF HEALTH AND HUMAN SERVICES
 JIRA 30658


MA21 System Change Specifications Document


  







	

	
Analyst:  Shailaja Jeevaratnam	 MassHealth MA21 Maintenance

Approval / Distribution / Interaction
Phase/Role 	Contact(s)
Scope / Use Cases	Mayvorly Ramirez
Functional Requirements	Mayvorly Ramirez
Observers	Name
MA21 Management 	Susan Kelly-Madden, Amanda Joubert
QA Supervisor	Alyssa Alexander
UAT - SME	
Partners / External Systems:	Description of Impact:	Contact /Imbedded Email
CFR	N	
CHPR	N	
CNS	N	
CommCare	N	
DOR	N	
eMBR	N	
HSNO	N	
IER	N	
Ins. Partnership	N	
ITD	N	
MAP	N	
MMARS	N	
MMIS	N	
Other	N	
Reporting	N	
RMV	N	
SLR	N	
SSA	N	
TPL/HIN	N	
Vital Stats	N	
Warehouse	N	

 
Revision History
Date	Version	Description	Author
1/30/2026	1.0	Removed combined ticket J33724 from scope and kept the functionality of J 30658 from original approved worksheet  	Shailaja Jeevaratnam


Impact Analysis
Requirements	Yes/No/NA/Comments
Are MoveIT interfaces required?
Must fill in MoveIT section 4.6 below	N
Is User Acceptance Testing (UAT) recommended?	N
Volume / No of records affected due to existing issue? Attach reports to indicate the records affected (if applicable)	N
Downstream Impact Analysis performed?  	Y
One time program needed to clean up affected existing cases?	N
Notices involved in this issue?  
Must Fill CNS section Below and Section 3.2	N
Need for reprocessing notices? 	N
Impact to MCP/MAP BEnefitService Webservice? 	N
Impact to MMIS middleware?	N
Table Changes (TABLE-GENERIC or BIG-TABLE-GENEIC)?	N
Any other systems affected?	N

 
CNS information provided in Jira
New Fields in Jira completed by Requestor
Notice Change Type	Needed? (Yes or No)
New notice	 N
Change notice text (static text only)	N
Change notice trigger	N
Change notice data element (ie, new fragment needed)	N
Add or remove insert to a notice	N
Esubmission required	N

CNS Impact Analysis
Notice Change Type	Notice in MA21 or CNS?	MA21/CNS Work Required
New Notice	Neither	MA21 payload development and CNS CR
Change notice text (static text only)	CNS	CNS CR only
	MA21-only	MA21 text change
	MA21 in transition to CNS	MA21 text change and CNS CR. Also coordinate with Judy/Jen for CNS template update
	Monsters (Highly complex)	Update MA21 text and coordinate with Judy/Jen for CNS template update
Change notice trigger	CNS	MA21 payload development/logic change and CNS CR
	MA21-only	MA21 logic change
	MA21 in transition to CNS	MA21 payload development/logic change and CNS CR. Also coordinate with Judy/Jen for CNS template update
	Monsters (Highly complex)	Update MA21 logic change and coordinate with Judy/Jen for CNS template update
Change notice data element (ie, new fragment needed, insert group)	CNS	MA21 payload development/logic change and CNS CR
	MA21-only	MA21 logic change
	MA21 in transition to CNS	MA21 payload development/logic change and CNS CR. Also coordinate with Judy/Jen for CNS template update
	Monsters (Highly complex)	Update MA21 logic change and coordinate with Judy/Jen for CNS template update
Esubmission	CNS	MA21 webservice development/payload development and CNS CR for conditional fragment
	MA21-only	MA21 webservice development/logic change
	MA21 in transition to CNS	MA21 webservice development/payload development and CNS CR for conditional fragment. Also coordinate with Judy/Jen for CNS template update

 
Table of Contents	

1.	Purpose of this Document	7
2.	Scope	7
2.1	Use Case Scenarios	8
3.	Functional Requirements	8
3.1	Decision Tree Changes	9
3.2	Notices	9
3.2.1	Paragraphs or Complete Notice – (Draft / Approved)	9
3.2.2	Notice Master Document Updates	9
3.2.3	Stacking	9
3.2.4	Order of Paragraphs	9
3.2.5	Downgrade Reasons	9
3.2.6	Closing and Denial Reasons	9
3.3	Reports	10
3.4	System Screen Updates (Queries, Maintenance & Events)	10
4.	Transition	10
4.1	Table Updates (include seed table updates)	10
4.2	Event Code Changes	10
4.3	Security Updates	10
4.3.1	User Security – (Natural Security – Define for New JCL Jobs)	11
4.3.2	Function Security – (MA21 Security – Functions, Groups, or Users)	11
4.3.3	Dataset Security	11
4.4	Production Control	12
4.4.1	Operational Instructions	12
4.4.2	JCL, Procedures, Parameters (TEST and PROD JCL & Parm Members)	12
4.4.3	Batch Process Considerations and Scheduling	12
4.5	Additional Required UP Artifacts	12
4.6	MoveIT Interfaces	13
4.7	Post Production Validation	13
4.7.1	Checklist to perform Post Production Validation	13
5.	Appendix A – Original JIRA Headline and Description	14
6.	Appendix B – Additional Documentation	17


 
1.	Purpose of this Document
This document is to be used by the MA21 Project Lead to accumulate and review information from contributors as part of the U.P. documentation process. This document includes Scope, Use Cases, Functional Requirements, Transition, and supporting information.


2.	Scope 
State Business Need or Issue:
Block Users from Adding a PCA Supplement (entered through the PCA event, MA21) when an Active LOC Code is present (all waiver codes with a clinical status of Y with no end date). Conversely, prevent all users from entering the waiver code in the LOC event when a PCA is active. 

Required edits to the pop-up message are provided by MH operation. 
PCA not allowed with active LOC *
LOC not allowed with active PCA

A one-time ADHOC report will be provided to identify members who are active on both the PCA and LOC codes (EOEA, DDS, ABI, MFP, MRC, LTC, Autism). 

Ensure that the LOC event is active with only one LOC type at a time. 


How it works now or the cause:
  Currently, the system allows workers to enter both a PCA supplement and an approved waiver. Members cannot be eligible for both at the same time. This causes the system to apply PCA disregard before evaluating income for the waiver program. 

Currently, MA-21 is allowing two active waiver codes, which is incorrect. MA-21 will be modified to prevent more than one LOC code from being entered at the same time. 

How it will work:
All Users are prevented from entering a PCA supplement for a member with an active LOC. The system should notify the worker that a PCA supplement cannot be entered for a waiver applicant and vice versa. Before a member's waiver status can be entered, the PCA must be ended first.  MA21 will only allow one active waiver code at a time and if a user attempts to add another waiver code when there is already one active, they will receive an error message.  


	MA-21 shall not allow both PCA and waiver to be valid codes at the same time. 
	Ensure that the LOC event is active with only one LOC type at a time. 
Comments:


 
2.1	Use Case Scenarios  
U33724-01 Goal – MA-21 shall not allow both PCA and LOC to be active at the same time. 
Person Actors:       MA-21 User
System Actors:  Ma-21

Pre-Conditions:   PCA and LOC waiver codes are active 
ABI-N   ABI Non-Residential Habilitation
ABI-RH  ABI Residential Habilitation
AUTISM  Autism Waiver For ST children 8 or younger
DDS-AR  DDS-Intensive Supports Waiver
DDS-AS  DDS-Adult Supports Waiver
DDS-CL  DDS-Community Living Waiver
EOEA    Frail Elder Waiver - EOEA
LTC     Long Term Care
MFP-CL  MFP Community Living
MFP-RS  MFP Residential Supports
MRC     Traumatic Brain Injury – MRC
PACE    PACE ONLOK

Ensure that the LOC code for any type is active when its clinical status is Y. 

Main Flow: Block Users from Adding a PCA Supplement (entered through the PCA event, MA21) when LOC is active and Vice Versa

Alternate Flow #: N/A
Exception Flow #:N/A

Post Success Condition: MA-21 will not allow both PCA and LOC codes at the same time. 


U30658-0=2 Goal –  Ensure that the LOC event is active with only one LOC type at a time. 

Person Actors:       MA-21 User
System Actors:  Ma-21

Pre-Conditions:  LOC waiver codes 
ABI-N   ABI Non-Residential Habilitation
ABI-RH  ABI Residential Habilitation
AUTISM  Autism Waiver For ST children 8 or younger
DDS-AR  DDS-Intensive Supports Waiver
DDS-AS  DDS-Adult Supports Waiver
DDS-CL  DDS-Community Living Waiver
EOEA    Frail Elder Waiver - EOEA
LTC     Long Term Care
MFP-CL  MFP Community Living
MFP-RS  MFP Residential Supports
MRC     Traumatic Brain Injury – MRC
PACE    PACE ONLOK


Main Flow: Ensure that the LOC code for any type is active when its clinical status is Y. 

Alternate Flow #: N/A
Exception Flow #:N/A

Post Success Condition: Ensure that the LOC event is active with only one LOC type at a time. 




3.	Functional Requirements 
Describe, from a user's perspective, the functions that the system is required to perform.
Functional Requirement  Number	Detailed Functional Requirement.  

F33724-01	Block Users from Adding a PCA Supplement (entered through the PCA event, MA21) when an Active LOC Code is present. Conversely, prevent the Mec worker from entering a waiver code in the LOC event when a PCA is active. 
Have screen edit as listed below.
PCA not allowed with active LOC *
LOC not allowed with active PCA

F30658-02	Ensure that the LOC event is active with only one LOC type at a time. 



3.1	Decision Tree Changes
Chart #	Description of Change (Exit Point, Benefit affected)	Imbedded Chart
N/A		
		
		

3.2	Notices
New or
Change	Notice Type	CNS Enabled (Y/N)	Description of Change 	Received Final English Text (Y/N)	Received Final Spanish Text (Y/N)
N/A					
					
					


3.2.1	Paragraphs or Complete Notice – (Draft / Approved)
N/A
3.2.2	Notice Master Document Updates
N/A
3.2.3	Stacking
N/A
3.2.4	Order of Paragraphs
N/A
3.2.5	Downgrade Reasons
N/A
3.2.6	Closing and Denial Reasons
           N/A

3.3	Reports
New or
Change	ViewDirect  One Time	Report Name	Report Description 	Imbedded Mock-Up
N/A				
				
				



3.4	System Screen Updates (Queries, Maintenance & Events) 


4.	Transition
4.1	Table Updates (include seed table updates)
Table Name	Table Type	Table Code	Description 
N/A			
			
			
			

4.2	Event Code Changes 
Type Key:  EVENT CODE
New or
Change	Event Code	Description

N/A		
		
		




4.3	Security Updates

4.3.1	User Security – (Natural Security – Define for New JCL Jobs)
New or
Change	User or Group ID	Description (80 Characters Maximum)                                                                           
(This includes any new Jobs that need to be Defined if JCL executes Natural)
N/A	DMA-JOB	
		
		

4.3.2	Function Security – (MA21 Security – Functions, Groups, or Users)
New or
Change	Function ID/User ID	Description (80 Characters Maximum)	Linked Users or Groups	Access Type: Display, Modify, Add, Purge or N/A
N/A				
				
N/A				

4.3.3	Dataset Security
Dataset Name or 
High Level Qualifier	Description	User RACF ID or Group ID	Access: Read, Write, Alter, Delete
N/A			
			
			


 
4.4	Production Control
4.4.1	Operational Instructions  
Describe Any Production Control Instructions
N/A




4.4.2	JCL, Procedures, Parameters (TEST and PROD JCL & Parm Members) 
Type Key:  JCL, Proc, Parm 
New or
Change	JCL
Procedure
Parameter 
Name	
Type	Description including JCLDOC information.

N/A			
			

4.4.3	Batch Process Considerations and Scheduling 
Process Considerations and Scheduling
N/A



4.5	Additional Required UP Artifacts
Artifact File Name	Description of Artifact
N/A	
	
	

 
4.6	MoveIT Interfaces 
(Analyst and Developer coordination may be needed)
Note: Once this section is completed, please copy and send to Mike Conena. 
Agency Name	Sending file name	Receiving file name	Frequency (daily, weekly, monthly, etc)	Timing (time of day)	Dependencies (jobs that need to run before and/or after)
N/A					
					
					

4.7	Post Production Validation 
4.7.1	Checklist to perform Post Production Validation
It is the assigned Analysts’ responsibility to verify that production implementation was completed successfully.  Analyst should plan ahead to identify what kinds of transactions to view that will validate functionality. You are responsible to work with DBA, QA, MMIS and Production Control and verify that each of the following has been completed successfully.
Post Production Verification Points	Completed (Y, N, N/A) 
Add comment if  N or N/A
One time program / conversion execution	N
Security changes	N
Table changes	N
JCL changes	N
Notice changes  	N
Program migrations	Y
Pre-Identified Transactions are completed and accurate	N
Calculations are completed and accurate	N/A
Any other items not mentioned but covered in this worksheet	N/A
 
 
5.	Appendix A – Original JIRA Headline and Description
Note:  This section is a snapshot of the original JIRA and does not necessarily represent the final Scope, Business Requirements, Functional Specifications, or Technical Specifications. 
JIRA Number	Requested By	JIRA Title
30658	MH ops 	LOC Event is allowing two waiver codes to be active which is incorrect

Assigned to and comments	JIRA Description
Shailaja Jeevaratnam	This is an unknown issue found by the Incident ticket that; a waiver member can be active at the same time in LOC event this existing screen edit could be broken due to recent updates. Need more analysis. LOE is medium. 

6.	Appendix B – Additional Documentation








COMMONWEALTH OF MASSACHUSETTS
EXECUTIVE OFFICE OF HEALTH AND HUMAN SERVICES

JIRA 30658 – Unit Test Results 



  







This document must be reviewed by MA21 Release management (Sue Kelly-Madden and Danna Sturdivant).

Short Description:	
LOC Event is allowing two waiver codes to be active which is incorrect	Analyst:	Shailaja Jeevaratnam
Total Number of test cases:	1	Developer:	Andrew Libambo
Maintenance Release 26.03 	01/09/2026	Date Created:	1/30/2026















Table of Contents

1.	Critical testing factors to be addressed guidelines:	3
2.	Describe Unit Testing Approach:	3
3.	Background (Describe the purpose of the code, refer to scope):	3
4.	Impact of the change (Predict a worst-case scenario to guide tester to critical areas):	4
5.	Additional Information:	4
6.	Test Cases:	4
6.1	Test Case Summary	4
6.1.1	Test Case 1: {scenario name}	5
6.1.2	Test Case 2: {scenario name}	5
6.1.3	Test Case 3: {scenario name}	5
6.1.4	Test Case 4: {scenario name}	6

 
1.	Critical testing factors to be addressed guidelines:  

a.	Must describe the Purpose of the code in Background section below, Describe the Unit test approach and add any important information that will aid System Testing.  

b.	Include regression testing needs to describe how the code change may affect existing functionality.

c.	Attempt to cause code to fail and document successful results with screenshots. 

d.	Must have a Unit Test Case documented to cover each Functional Requirement.

e.	Ensure that the following Pillars of Eligibility are fully tested as applicable for any eligibility changes.
•	Age
•	Income
•	Household composition
•	Immigration / Citizenship status

f.	Mandatory meeting must occur between Analyst and assigned QA Tester to share details of the change and confirm full understanding of scope.

g.	Data in DSGN/TEST may not be complete for testing. Analyst should run the new code in ADHOC against real PROD data, if possible, to show that the code change is working and not causing any failure.

h.	Document if the code change has potential to cause major side effects that will affect members.


2.	Describe Unit Testing Approach:

3.	Background (Describe the purpose of the code, refer to scope): 
 
              Ensure that the LOC code for any type is active when its clinical status is Y. 
4.	Impact of the change (Predict a worst-case scenario to guide tester to critical areas):


          
5.	Additional Information:
For this section, add in any additional information that would be helpful to QA to complete the test plan.

QA need to check all LOC types 

ABI-N   ABI Non-Residential Habilitation
ABI-RH  ABI Residential Habilitation
AUTISM  Autism Waiver For ST children 8 or younger
DDS-AR  DDS-Intensive Supports Waiver
DDS-AS  DDS-Adult Supports Waiver
DDS-CL  DDS-Community Living Waiver
EOEA    Frail Elder Waiver - EOEA
LTC     Long Term Care
MFP-CL  MFP Community Living
MFP-RS  MFP Residential Supports
MRC     Traumatic Brain Injury – MRC
PACE    PACE ONLOK


6.	Test Cases:


6.1	Test Case Summary
For this section, list all test case scenarios.


 
Add any necessary screenshots here.

6.1.1	  Test Case 1: {scenario name}
Functional Requirement(s) being tested:


Ensure that the LOC event is active with only one LOC type at a time. 

Prerequisites: (Are there any conditions or settings that are needed to execute test)

ENTER Any LOC type and try to add a another type in LOC event 


In Design: (add steps to prepare test data and include applicable screenshots)
Step 1: 

 



 

Add any necessary screenshots here.




