Certificate Validation: 

Business Requirement:  

In GeM portal, seller provides different certificates such as MRP documents, registered trademark 
certificate, DPIIT certificate and many other documents. Buyers also need to provide some documents 
such as CA (Competent Authority) document approval. Currently validation of the information provided 
in these documents is a manual process. 
GeM intends to automate/semi-automate validation of the information provided by sellers/buyers in 
different certificates with the information already provided by same sellers / buyers during on
boarding/bidding process. This is with intention to save time in verifying documents and avoid errors 
caused by manually verification. This will help with preliminary check on the documents uploaded, helping 
sellers/buyers avoid any mistaken upload of documents by the stakeholders. 
GeM requires a scalable solution for validating products and services related documents. Data extraction 
for analytics consumption from unstructured data/ scanned documents submitted. Content mining, Entity 
matching and Named Entity Extraction for capturing key parameters from the scanned documents which 
are not covered as part of overall QCI scope to identify patterns and generate actionable insights to 
design/improve future processes like vendor on-boarding, bidding etc. 

<img width="2028" height="1078" alt="image" src="https://github.com/user-attachments/assets/05593062-12f9-4fe5-a1e9-2f20af80b740" />

Proposed solution: 

Develop a data extraction model from scanned images/pdfs and a validation mechanism to verify 
information provided in certificates. Certificate’s validation process should be automated or semi
automated. This would reduce the time it takes to validate the documents and eliminate errors caused by 
manually importing the data into the report. As already mentioned in above section, which are the 
processes in which document verification performed in GeM. Once this solution applied, information 
obtained will be used for taking decisions 
Generic system to validate the content within the document based on the information provided by the 
sellers / buyer: 
• Certificate conversion from PDF to image 
• Image enhancement for increasing readability 
• Data extraction from the enhanced image 
• Data processing and NLP (Fuzzy Wuzzy) 
• Data validation as per the user details in Database. 

<img width="2028" height="1093" alt="image" src="https://github.com/user-attachments/assets/f9858d41-5cb6-441f-b58f-a0ed6db131e9" />


Solution Consumption: 

Following are the stakeholders and processes where this solution can have impact. There are two 
stakeholders in the process:  
• Buyers: Need to manually validate information provided by sellers in bidding process like MRP 
certificate, Trademark certificate etc.
• GEM - MSP: The team manually validates the documents provided to see if the information in the 
submitted documents by the buyer / seller matches the database information.

Data: 
• We require 7 documents (DPIIT,  Trademark, MRP, FSSAI, Meity, PSARA, BIS ) which are uploaded 
by Seller / buyer image or pdf format.  
• We require the concerned seller details of whom the documents have been uploaded. 
• We require the concerned Buyer details of whom the documents have been uploaded. 
How to get the required data: 
• Documents Data shared by GeM-MSP team for all the above-mentioned types of documents with 
all variations to create solution. At the time of ‘go-live’ on production system, GeM-MSP team to 
share document to be validated at process of GeM. 
• connect to the database and pull the required details to perform validation. 

<img width="1331" height="1164" alt="image" src="https://github.com/user-attachments/assets/52bc3ae1-93d9-4aa6-84ea-24d2c8fe6b5a" />
<img width="1082" height="1303" alt="image" src="https://github.com/user-attachments/assets/68f9f985-c846-4f14-840e-df8559b8ba82" />


Eg: Database Data: 
Data available in database, will be used for validating certificate information. 
<img width="1328" height="146" alt="image" src="https://github.com/user-attachments/assets/bbb68dd5-ed74-4855-8e37-d7051718d5ec" />

Model Methodology: 

The code is designed to semi-automate the validation of information provided in various certificates by 
sellers and buyers on the GeM portal. The methodology involves the following steps: 
1. Text Data Processing: 
• The code begins by extracting and processing text data from a provided document (doc). This 
document might be extracted from certificates submitted by users. 
• The text is cleaned by converting it to lowercase, removing newline characters, and stripping 
any unnecessary whitespace. This step ensures the text is in a uniform format for further 
processing. 
2. Fuzzy Matching Using NLP Techniques: 
• The core function (test1) takes a search string (which could be critical keywords or phrases from 
the on-boarding/bidding process) and splits it into individual words. 
• The document is also split into words, and each word in the search string is compared against 
different parts of the document using fuzzy matching techniques. 
• The fuzzy matching is done using the fuzzy Wuzzy library's token_set_ratio function, which 
calculates similarity scores between the words in the search string and sections of the 
document. 
• The function is versatile and can handle search strings of varying lengths (from 1 to 7 words), 
ensuring that different document types and content lengths are appropriately handled. 
3. Data Storage and Analysis: 
• The similarity scores calculated during the fuzzy matching process are stored in a Pandas Data 
Frame, with columns corresponding to each word's matching score. 
• This structured data allows for easy analysis, where matching scores can be reviewed to 
determine the accuracy of the document content against the provided information during the 
on-boarding/bidding process. 
4. Validation Mechanism: 
• The resulting scores provide a basis for validating the information contained within the 
documents. By comparing the scores against a predefined threshold, the system can determine 
whether the document content aligns with the expected information. 
• This semi-automated approach helps in the preliminary check of the documents, reducing the 
likelihood of errors and speeding up the validation process.

<img width="1419" height="911" alt="image" src="https://github.com/user-attachments/assets/0151bba3-61b2-4aa2-97b1-309ba82be2d2" />
<img width="2009" height="1075" alt="image" src="https://github.com/user-attachments/assets/4223fdcd-d660-4326-a4fa-f52bd1e07fa8" />

Steps In Model:  
1. Extract and Preprocess Text Data: 
• Input Document: Start by loading the document (doc) that contains text extracted from 
certificates or other relevant sources provided by sellers or buyers. 
• Text Cleaning: Clean the document text by converting it to lowercase, removing newline 
characters, and stripping any unnecessary whitespace. This standardizes the text for consistent 
processing. 
2. Search String Preparation: 
• Search String Input: Define the search string, which represents the critical information that 
needs to be validated against the document. This could be key phrases, entity names, or other 
relevant data from the on-boarding/bidding process. 
• Word Splitting: Split the search string into individual words, preparing them for detailed 
comparison against the document content. 
3. Fuzzy Matching of Text: 
• Document Splitting: Split the document into a list of words, preparing it for matching. 
• Token Set Ratio Calculation: For each word in the search string, calculate the similarity score 
between the word and various sections of the document using the fuzzy Wuzzy library's 
token_set_ratio function.

• Handle Different Search String Lengths: Adapt the matching process to handle search strings of 
varying lengths (from 1 to 7 words), ensuring flexibility in dealing with different types of 
documents. 
4. Store and Analyse Matching Scores: 
• Data Frame Creation: Store the calculated similarity scores in a Pandas Data Frame. Each word's 
score is saved in a separate column, providing a structured view of how well the document 
matches the search string. 
• Score Review: Analyse the scores to determine the accuracy of the document's content against 
the expected information provided during the on-boarding/bidding process. 
5. Validation Mechanism: 
• Threshold Comparison: Compare the similarity scores against predefined thresholds to assess 
whether the document content aligns with the expected data. 
• Decision Making: Use the comparison results to make decisions on the validity of the document. 
Documents that do not meet the threshold criteria may require further manual review or be flagged for errors.

Note: 
As per our understanding and after discussion with GeM taskforce, below are the processes and 
documents identified in which this verification solution can be applied in GeM.  
• Seller On Boarding: DPIIT, DOE order compliance (At the time of profile update) and Seller profile 
update documents. 
• CMS: Trademark certificate, MRP, Unbranded unregistered etc. certificates  
• Bidding related: Buyer side Competent Authority document 

Business Value:

1. Reduces the time it takes to validate a record by ten times. 
2. Verifies that the buyer/seller has uploaded the correct certificate.  
3. Tries to capture the certificates where validity has been expired or about to expire  
4. GeM stakeholders can identify Buyers/Sellers in case they are uploading fake certificates / Irrelevant 
certificates.

Integration & API: Developed and integrated RESTful APIs using FlaskAPI :

Input – Solution required three inputs to validate certificates in “Certificate Validation”. 
These are the following checks required


1.TOC 
2.Upload Image 
3. Checks 
Outcome: Solution showcases the validated checks result in json format containing consolidated 
scores, checks and respective check status. 

<img width="1407" height="981" alt="image" src="https://github.com/user-attachments/assets/6482aa61-cfc6-42a7-8550-91e1ffc226d3" />




