---
title: Example Messages 
parent: DFT (DFT-P03)
---

## Example Messages

**Example A:** 
```
MSH|^~\&|IRIS|IRIS|Cerner|Cerner|20200130165606||DFT^P03|200130165606|T|2.4
EVN|P03|20200130165606
PID||123456|123456^^^^MRN||DOE^JANE||19620803|F||||||||||201026045|123-45-6789
PV1|1|O|CORE||||9988776655^Roe^John^^^^^^^^^^NPI|11223344^Doe^Janie^^^MD^MD^^^^^^NPI|||||||||9988776655^Roe^John^^^^^^^^^^NPI||201026045|||||||||||||||||||||||||20200130124309|20200130165606
FT1|1||815339|20200130045244|20200130165606|CG|92250^Fundus photography with interpretation and report^CPT||123456|1|||CORE||IRIS|CORE||||9988776655^Roe^John^^^^^^^^^^NPI|11223344^Doe^Janie^^^MD^MD^^^^^^NPI||604087471^Cerner||92250^Fundus photography with interpretation and report^CPT|26
```
**Example B:**
```
MSH|^~\&|IRIS|IRIS|Test Hospital|EPIC|20200108091806||DFT^P03|200108091806|P|2.3
EVN|P03|20200108091806
PID||777777777|777777777^^^^MRN||TEST^ABBY||19770101|F||||||||||1000139258624|
PV1|1|O|OCFMW||||tgittings@retinalscreenings.com^Gittings^Tiffani^^^^^^^^^^NPI|654321^DOE^JANE^^^MD^MD^^^^^^NPI|||||||||tgittings@retinalscreenings.com^Gittings^Tiffani^^^^^^^^^^NPI||1000139258624|||||||||||||||||||||||||20200107112601|20200108091806
FT1|1||803695|20200107113321|20200108091806|CG|92250^Fundus photography with interpretation and report^CPT||777777777|1|||OCFMW||IRIS|OCFMW|||E11.8^Type 2 diabetes mellitus with unspecified complications^ICD-10-CM~E11.349^Type 2 diabetes mellitus with severe nonproliferative diabetic retinopathy without macular edema^ICD-10-CM~E11.329^Type 2 diabetes mellitus with mild nonproliferative diabetic retinopathy without macular edema^ICD-10-CM|tgittings@retinalscreenings.com^Gittings^Tiffani^^^^^^^^^^NPI|654321^DOE^JANE^^^MD^MD^^^^^^NPI||143619354^EPIC||92250^Fundus photography with interpretation and report^CPT|26
```

**Example C:**
```
MSH|^~\&|IRIS|IRIS|Vendor|Vendor|20200124205607||DFT^P03|200124205607|T|2.3
EVN|P03|20200124205607 PID||12182019|12182019||Test^Greg||19900101|F||||||||||1234|111-22-3333 PV1|1|O|IrisTest||||adiaz@retinalscreenings.com^Diaz^Adam^^^^^^^^^^NPI|adiaz@retinalscreenings.com^Diaz^Adam^^^^^^^^^^NPI|||||||||adiaz@retinalscreenings.com^Diaz^Adam^^^^^^^^^^NPI||1234|||||||||||||||||||||||||20200124085439|20200124205607 FT1|1||805515|20200124085532|20200124205607|CG|92250^Fundus photography with interpretation and report^CPT||12182019|1|||IrisTest||IRIS|IrisTest|||E13.351^Other specified diabetes mellitus with proliferative diabetic retinopathy with macular edema^ICD-10-CM|adiaz@retinalscreenings.com^Diaz^Adam^^^^^^^^^^NPI|adiaz@retinalscreenings.com^Diaz^Adam^^^^^^^^^^NPI||Order846625^Vendor||92250^Fundus photography with interpretation and report^CPT|26 FT1|2||805515|20200110041014|20200124085532|CG|3072F^No evidence of retinopathy in the prior year||12182019|1|||IrisTest||IRIS|IrisTest|||E13.351^Other specified diabetes mellitus with proliferative diabetic retinopathy with macular edema^ICD-10-CM|adiaz@retinalscreenings.com^Diaz^Adam^^^^^^^^^^NPI|adiaz@retinalscreenings.com^Diaz^Adam^^^^^^^^^^NPI||Order846625^||3072F^No evidence of retinopathy in the prior year|TC 
```

<< [Most Common Diagnosis](/IntegrationDocumentation/docs/integration/DFT_Results/Most_Common_Diagnoses)