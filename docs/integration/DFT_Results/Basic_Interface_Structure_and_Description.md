
## Basic Interface Structure and Description

This document outlines the values sent in an HL7 charge message (DFT-P03) from IRIS to a third-party system. This third-party system could be another application, an interface engine, or an EMR. For the purposes of this documentation, this third-party will be referred to an EMR.

IRIS uses HL7 v2.4 as a main protocol for message sharing. If there are any fields represented in this document that are not populated but required by a receiving EMR, IRIS will populate these value(s) as requested. If the receiving EMR requires a different version, IRIS can provide messages for the corresponding version. If the EMR expects messages to be delivered in a format other than HL7, this will need to be discussed with an IRIS Interface Engineer as this will not be covered in the scope of this document – please contact IRIS support for more information.

Following this section, the rest of the document will be divided by HL7 segment types as they would appear in a delivered HL7 message. IRIS has two different structural setups for the FT1 segment. This will be described in detail later in that section. The last section of this document contains an example HL7 message.

[Back to HL7 DFT Results Page](/docs/integration/DFT_Results/DFT_Results.md)