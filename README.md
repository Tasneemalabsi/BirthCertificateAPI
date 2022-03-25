# Birth Certificate Service

## Get List Of Departments
----
API endpoint to return a list of Departments in the system.

* **URL**

 /rest/api/v1/Departments

* **Method:**

  `POST`
  
*  **URL Body**

**All of the elements are required**

```
     {
    "IsoCode":"001",
    "ServiceType":"Birth_Certificate",
    "DepartmentType":"02"
    }
```

* **Success Response:**

  * **Code:** 200 <br />
    **Content:** 
                        
                    [
                        {
                      
                        "Code": "1",
                        "HasEmployee": false,
                        "HasManager": false,
                        "DepartmentType": "CSPD_Office",
                        "IP_Address_From": "1.1.1.1",
                        "MainOfficeInd": true,
                        "PrintingInd": true,
                        "AddressDetails": "Amman",
                        "AdditionalServiceFees": 0,
                        "IP_Address_To": "1.1.1.2",
                        "ArabicIssuanceAuthority": "عمان",
                        "EnglishIssuanceAuthority": "Amman",
                        "PrintingExport": "1",
                        "DepartmentTypeExport": "1",
                        "OnlineInd": true,
                        "CivilOfficeInd": false,
                        "InternalOffice": false,
                        "PrintingButton": "ViewAndPrinting",
                        "PassportFileInd": false,
                        "CheckIPAddress": false,
                        "embassyInd": false,
                        "DescriptionArabic": "عمان",
                        "DescriptionEnglish": "Amman",
                        "Description": "عمان",
                        "ActiveInd": "Active",
                        "changedDate": "2018-08-27T15:31:17.915Z",
                        "createdDate": "2018-06-10T11:47:18.806Z"
                      },
                      {
                        "Code": "2",
                        "HasEmployee": false,
                        "HasManager": false,
                        "DepartmentType": "CSPD_Office",
                        "MainOfficeInd": false,
                        "PrintingInd": true,
                        "AddressDetails": "الزرقاء",
                        "AdditionalServiceFees": 0,
                        "ArabicIssuanceAuthority": "الزرقاء",
                        "EnglishIssuanceAuthority": "Zarqa",
                        "PrintingExport": "1",
                        "DepartmentTypeExport": "1",
                        "OnlineInd": true,
                        "CivilOfficeInd": false,
                        "InternalOffice": false,
                        "PrintingButton": "ViewAndPrinting",
                        "PassportFileInd": false,
                        "CheckIPAddress": false,
                        "embassyInd": false,
                        "DescriptionArabic": "الزرقاء",
                        "DescriptionEnglish": "Zarqa",
                        "Description": "الزرقاء",
                        "ActiveInd": "Active",
                        "changedDate": "2018-08-16T11:09:54.941Z",
                        "createdDate": "2018-08-09T11:02:36.456Z"
                            }
                ]

* **Error Response:**

  * **Code:** 400 BAD REQUEST <br />
    **Content:** `{"error": "Bad Request"}`
    
* **Notes:**

The DepartmentType holds the value of 01 to return the empassies or 02 to return the CSPD-offices .

## Get Prerequisite
----
API endpoint to return the prerequisite for a certain service type.

* **URL**

/rest/api/v1/GetPrerequisite

* **Method:**

  `POST`
  
*  **URL Body**
 
 **All of the elements are required**
 
```
{
 "ServiceType": "Birth_Certificate",
  "UserLanguage": "ar_JO"
 }
```

* **Success Response:**

  * **Code:** 200 <br />
    **Content:** 
    ```
    {
       "Prerequisit": "شهادة ميلاد"
    }
    ```
                        
                    
* **Error Response:**

  * **Code:** 400 BAD REQUEST <br />
    **Content:** `{"error" : "The Service Is Not Found"}`

## Fees Calculation
----
API endpoint to calculate the fees for the requested service .

* **URL**

/rest/api/v1/FeesCalculation

* **Method:**

  `POST`
  
*  **URL Body**
 
 **All of the elements are required** //the DeliveryType is required only if the country is local 
 
```
{
 "DeliveryCountryCode":"001",
 "ServiceType":"Birth_Certificate",
 "DeliveryType":"Aramex",
 "arabicCopies":2,
 "EnglishCopies":1
}

```

* **Success Response:**

  * **Code:** 200 <br />
    **Content:** 
    ``` 
        [
          {
            "FeeType": "Certificate_Issuance_Arabic",
            "FeeAmount": 1,
            "CopiesNumber": 1
          },
          {
            "FeeType": "Certificate_Issuance_English",
            "FeeAmount": 1,
            "CopiesNumber": 1
          },
          {
            "FeeType": "Delivery_Fees",
            "FeeAmount": 6,
            "CopiesNumber": 0
          }
        ]
    ```
                        
                    
* **Error Response:**

  * **Code:** 400 BAD REQUEST <br />
    **Content:** `{"error": "The Parameters should be filled"}`
    
## Check English Name
----
API endpoint to check the editability of an English name for the input national number .

* **URL**

/rest/api/v1/CheckEnglishName

* **Method:**

  `POST`
  
*  **URL Body**
 
 **All of the elements are required**
```
{
"ServiceType": "Birth_Certificate",
"NAT_NO": "9932020000"
}

```

* **Success Response:**

  * **Code:** 200 <br />
    **Content:** 
    ``` 
        {
          "EFirstName": "Ayah",
          "ESecondName": "Mohammad",
          "EThirdName": "Ayed",
          "EFamilyName": "Alqurashi",
          "EditableEngNameInd": false
        }
    ```
                        
                    
* **Error Response:**

  * **Code:** 400 BAD REQUEST <br />
    **Content:** `{"error": "No Data Found for this NationalId"}`
   
* **Notes:**

The EditableEngNameInd is a boolean that is false when the english name for the input national number can be editted and false when it's not possible to edit it
