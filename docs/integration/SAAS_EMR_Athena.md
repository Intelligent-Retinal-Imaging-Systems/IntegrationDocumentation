---
title: Athena SAAS EMR Integration
---

# SAAS Integration specification: Athena

<div style="position:absolute;">

Intelligent Retinal Imaging Systems &#8482;

</div>

<div align="right" >

[Back to Cloud Providers main page](/docs/integration/IRISEMRCloudProviders.md)

</div>


Order Sets for a Specified Facility Intelligent Retinal

Imaging Systems

Order sets are utilized to accelerate the ordering process for clinicians. Order sets can be created for a specific user or to be utilized by all clinicians at the practice. Follow these steps to set-up order sets.

1. Navigate to "Manage My Order Sets" via Gear→ Order Sets

2. Click “Add New" to create a new order set, or search and filter to narrow down existing ones. Take special note of naming the order set.When ordering, this is what will be used to searchfor this set. This is also where an order set can be assigned to one user, a group of users, or the whole practice. Update Order Set

<!-- Order Set Name Fundus Photo Users AlIl Selected Specialty All Selected Ordering  -->
![](https://web-api.textin.com/ocr_image/external/01aa46851ddd49cc.jpg)


| Manage My Order SetsAsk on Order Entry (AOE) questions and answers will auto-populate in the encounter exactly as recorded in the Order Sets below | Manage My Order SetsAsk on Order Entry (AOE) questions and answers will auto-populate in the encounter exactly as recorded in the Order Sets below |
| -- | -- |
| Filter byUserSpecialty | Order set nameDiagnosis |
| Order set type Sets with compendiumchanges ①Fiter Beset | Order set type Sets with compendiumchanges ①Fiter Beset |
| My Order SetsAdd.new |  |


3. Search and Add Diagnos hat the order set should be associated with, if needed. An order set can be orders without a specified diagnosis.The gnosis will be required and added during the encounter.

4. In the purple "Add orders" line, select “Imaging."

5. To search orders specifically from IRIS, click the "select facility"link. Selecting "IRIS (INTELLIGENT RETINAL IMAGING SYSTEMS)" will ensure the orders that are chosen are within the IRIS compendium (offered at the selected facility).


| Diagnoses and Orders DetailNo Diagnosis |  |
| -- | -- |
| Add Orders Order SetMedication Imaging VaccineDMESurgery/Px Referral Patient Info OtheSearch within: Orders offered by (no facility selected) select facilityGlobal order listQuickpicks Patient Historicalno items found N/A | r Diagnoses and Orders DetailNo DiagnosisAdd OrdersOrder Set MedicationLabImagingVaccineDMESurgery/Px Referral Patient Info OtherSearch within:Orders offered byIRIS (INTELLIGENT RETINAL IMAGING SYSTEMS) changeGlobal order listQuickpicks Patient Historicalno items found N/A |


6. Add the imaging tests that should be included in t der seet ted tests will appear below the search field and are associated with the diagnosis listed in the high Enter additional tests by searching and clicking on the order. Notice the "Send to:" field on NTELLIGENT RETINAL IMAGING SYSTEMS), as selected in #5.

7. When complete, select "Add" below the order set.


| Diagnoses and Orders Detail |
| -- |
| No DiagnosisAdd Orders Order SetMedicationLabImagingVaccineDMESurgery/PxReferral Patient InfoOtherFUNDUS PHOTOGRAPHY WITH INTERPRETATION AND REPORT Alarm: defaul Send to: VVIRIS (INTELLIGENT RETINAL IMAGING SYSTEMS): 2 N PALAFOX STREET SUITE 200PENSACOLA, FL 32502, Ph (888) 535-2574 |
| PHOTO,EYT,FUNDUSSend To Cinical providerN/A (Point-of-care test)Imaging Order Details There is no dataavallable because no imaging faciity is selected. |
| Priority □STAT Future SubmissionAlarm no alarmNote to Imaging FacilitySubmitter |
| Internal NoteAppointment TimeSide |


An Order Set can be utilized during an encounter in the Assessment & Plan section of the Exam. Ordering these order sets outside of an encounter is done by selecting the Patient Action Menu in a patient's chart and clicking on “Create Order Group."

1. For ordering during a patient's visit, navigate to the Assessment & Plan of the Exam. If ordering outside of the visit, navigate to the patient's chart and click on Create Order Group in the Patient Action Menu.

<!-- Quickview Create patient case Create orser group Create onder group Print chart sections Print forms Add document Chart export Third party applications Audit history  -->
![](https://web-api.textin.com/ocr_image/external/14876dd1613deade.jpg)

<!-- 11-09-2020 New Pa -0-0 Review-HPI-ROS 一 PE A/P Sign-off Assessment & Plan x DIAGNOSES & ORDERS Supervising Provider Albert Davis, MD  -->
![](https://web-api.textin.com/ocr_image/external/ef4d565f680ee46d.jpg)

2. Select the plus sign to add Diagnosis & Orders.

3. Using the search tool, search for the name of the Order Set that was created.

4. Alternatively,select the Order Sets filter to find the order set necessary to order.


| Order Group | Order Group | Order Group | Order Group |
| -- | -- | -- | -- |
| OrdersOrderingSupervisi |  | XIAGNOSES & ORDERS |  |
| OrdersOrderingSupervisi |  |  |  |
| OrdersOrderingSupervisi |  Search options |  Search options |  |
| OrdersOrderingSupervisi | Order Sets (2)Broken Hand (2)IRUS fundus phato(2) | Order Sets (2)Broken Hand (2)IRUS fundus phato(2) |  |
| PrescriMisuse 8 | Order Sets (2)Broken Hand (2)IRUS fundus phato(2) | Order Sets (2)Broken Hand (2)IRUS fundus phato(2) | Stimula |
| PrescriMisuse 8 | Diagnoses (10)active or passive immunization | Diagnoses (10)active or passive immunization | Stimula |
| FollowPatient w | Diagnoses (10)active or passive immunization | Diagnoses (10)active or passive immunization |  |
| FollowPatient w | Orders (9)CMP serum or plasma | Orders (9)CMP serum or plasma |  |
| LettersDelete Ord | Orders (9)CMP serum or plasma | Orders (9)CMP serum or plasma |  |
| LettersDelete Ord | Point of Care Tests(3)HbA1c (hemoglobin A1c), blooder Group | Point of Care Tests(3)HbA1c (hemoglobin A1c), blooder Group |  |


5. Ensure the selection is housed under the “Order Sets" section in the diagnosis and orders menu.

6. When the order set is selected, all orders and/or diagnosis will appear below the menu.

7. If the order set does not have a specified diagnosis, add the appropriate diagnosis by clicking the red plus sign.

8. Note, some diagnoses need more specificity and an ICD-10 code will have to be selected from a menu by clicking the red "ICD_10 CODE" text below the diagnosis.

9. When a diagnosis has been added, the orders are ready to be signed and sent to the appropriate facilities if need.

DIAGNOSIS

fundus photography with interpretation and report

Send on 08-12-2021 Iris (Intelligent Retinal Imaging Systems) Type 1 diabetes mellitus CHANGE

photo,eye,fundus ICD-10 CODE

fundus photography with interpretation and report

Send on 08-12-2021Iris (Intelligent Retinal Imaging Systems)

photo,eye,fundus

## Billing Consideration


![](https://web-api.textin.com/ocr_image/external/304d3f3b5002c5a4.jpg)


| Verify the proper procedure code is mapped to the procedure. (Clinicals Admin&gt; Order Type & ProcedureTemplate Mapping). This will ensure the code populates automatically on the billing tab when the procedureis ordered. When the image has been reviewed and approved by the provider, a claim is ready to becreated per your practice's billing workflows. |
| -- |




