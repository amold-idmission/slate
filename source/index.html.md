---
title: MyMo SDK

language_tabs: # must be one of https://git.io/vQNgJ
  - Java 
  - Objective_c
  - Swift


toc_footers:
  - © 2020 IDmission LLC
  - <a href='https://www.idmission.com/company/privacy-policy/'>Privacy Policy</a>
  - <a href='https://www.idmission.com/company/term-of-use/'>Terms of Use</a>  


includes:
  

search: true

code_clipboard: true
---

# Introduction

## Purpose
The purpose of this document is to serve as a reference manual and configuration guide for the MyMo Mobile SDK. This manual includes details for Android devices only.

This manual will illustrate how to embed the SDK into your host application and utilize all the basic features currently supported.

## Intended Audience
This document is intended for developers, project managers and QA testers. It is recommended that this document be read in full in order to understand the functionality as a whole and how each section relates to the other.

## Contact Us
If you have any questions regarding this guide, please contact our Customer Support Team at [implementation@idmission.com](mailto:implementation@idmission.com).  You can also submit a service request through the MyeVolv Portal if you have access.

# MyMo Overview and Key Features

The main features supported in this SDK are:

    <ul>
    <li>Send Money using MyMo keyboard</li>
    <li>Check transaction history</li>
    <li>Use MyMo keyboard on mobile phones</li>
    </ul>


# Minimum Requirements and Setup

## Requirements for IOS

    <ul>
    <li>iOS 11.0 or higher</li>
    <li>Active internet connection.</li>
    </ul>

## Requirements for Android
    <ul>
    <li>Android 4.0 or higher</li>
    <li>Active internet connection</li>
    <li>The following permissions and features should be present in your AndroidManifest.xml:</li>
    "uses-permission android:name="android.permission.INTERNET"<br/>
    "uses-permission android:name="android.permission.READ_CONTACTS"
    </ul>

# Dependencies

## Dependencies for iOS 
### Add Support for contact list
    <ul>
    <li>To get access to the contact list from your app, you need to add the following key & its description in your project’s info.plist file.</li>
    <li>Navigate to your project’s info.plist file</li>
    <li>Add key “Privacy - Contacts Usage Description”.</li>
    <li>Add its description “Access is needed to send an amount to the receiver's number.”</li>
    </ul>
    
## Dependencies for Android 
    <ul>
    <li>Need to add below dependency in build.gradle(App)</li>
    implementation 'androidx.recyclerview:recyclerview:1.0.0'<br/>
    implementation 'commons-lang:commons-lang:2.6'
    </ul>
    
# KeyboardSDK Enable/Disable State

## IOS functionality 
        <ul>
        <li>In keyboard extension, Keyboard’s enabled or disabled state can be find out using isKeyboardEnabled() method</li>
        <li>User can use above method in following way</li>
        </ul>
        
```Swift
    import UIKit
    import KeyboardSDK
     
    class KeyboardViewController: KeyboardParentViewController {
     
        override func viewDidLoad() {
            super.viewDidLoad()
     
            if isKeyboardEnabled() {
                print("Keyboard Is Enabled")
            } else {
                print("Keyboard Is Disabled")
            }
        }
    }
```
        
## Android functionality 
        <ul>
        <li>In keyboard extension, Keyboard’s enabled or disabled state can be find out using isMymoEnable() method</li>
        <li>User can use above method in following way</li>
        
    MyMoSettings myMoSettings = MyMoSettings.getInstance(Your Activity); </br>
    true / false =  myMoSettings.isMymoEnable();

        <li>True if Keyboard SDK is enabled; false if disabled.</li>
        </ul>

# Parameter Details
Note: Mandatory parameters are highlighted with *.

Parameter | Type | M–Mandatory </br> C–Conditional </br>O–Optional | Description
--------- | ------- |  ---------- | ----------
phoneNumber* | String | M | <ul><li>Senders’ Phone Number. </li><li>Internally used to enroll phone number in the IDM System on keyboard enable. </li><li> Used in transaction. </li><li> `E.g. 744636363`(Should not include country code) </li><li> Initialization iOS : </br> `initKeyboardSDK( .....,phoneNumber: "744636363 ",.....  )`</li><li> Initialization Android : </br>`myMoSettings.setPhoneNumber(phoneNumber);`</li></ul>
senderName* | String | M | <ul class="ul-in-table"><li>Senders’ Name.</li><li> Internally used to enroll the sender's name against his/her phone number in the IDM System.</li><li> Used in transaction.</li><li> `E.g. John Doe` </li><li> Initialization iOS : </br> `initKeyboardSDK( .....,senderName: "John Doe”,.....  )`</li><li> Initialization Android : </br>`myMoSettings.setSenderName(senderName);`</li></ul>
CustomerCode | String | O |<ul class="ul-in-table"><li> Sender Customer Code.</li><li>If present , internally associated with phone number and used for transaction else phone number is used in transaction.</li><li> `E.g. 47363` </li><li> Initialization iOS : </br> `initKeyboardSDK( .....,CustomerCode: "47363",.....  )`</li><li> Initialization Android : </br>`myMoSettings.setCustomerCode(customerCo de);`</li></ul>
CountryCode* | String | M | <ul class="ul-in-table"><li>Country Code.</li><li>Used internally for IDS to save against transactions in the database.</li><li> `E.g. PAKISTAN, HONDURAS etc` </li><li> Initialization iOS : </br> `initKeyboardSDK( .....,CountryCode: "PAKISTAN",.....  )`</li><li> Initialization Android : </br>`myMoSettings.setCountryCode(countryCode);`</li></ul>
CurrencyCode* | String | M | <ul class="ul-in-table"><li>Currency Code.</li><li>Used internally for IDS to save against transactions in the database.</li><li>Also used to display on Payment link web pages.</li><li> `E.g. PKR` </li><li> Initialization iOS : </br> `initKeyboardSDK( .....,CurrencyCode: "PKR",.....  )`</li><li> Initialization Android : </br>`myMoSettings.setCurrencyCode(currencyCode);`</li></ul>
CurrencySymbol | String | O | <ul class="ul-in-table"><li>Currency Symbol.</li><li>Used to display on UI for keyboard.</li><li> `E.g. PKR` </li><li> Initialization iOS : </br> `initKeyboardSDK( .....,CurrencySymbol: "PKR",..... )`</li><li> Initialization Android : </br>`myMoSettings.setCurrencySymbol(currencySymbol);`</li></ul>
loginID* | String | M | <ul class="ul-in-table"><li>Login Id internally used for Request Authentication at IDS.</li><li>It's a Constant Value. - `E.g: MyMoDemo`</li><li> Initialization iOS : </br> `initKeyboardSDK( .....,loginID: "MyMoDemo”,..... )`</li><li> Initialization Android : </br>`myMoSettings.setIntegLoginId(integLoginId);`</li></ul>
Password* | String | M | <ul class="ul-in-table"><li>Password is for above login id.</li><li>Is internally used for Request Authentication at IDS.</li><li>It's a Constant Value. - `E.g: Merchant#1`</li><li> Initialization iOS : </br> `initKeyboardSDK( .....,Password: "Merchant#1”,..... )`</li><li> Initialization Android : </br>`myMoSettings.setIntegPassword(integPassword);`</li></ul>
MerchantID* | String | M |<ul class="ul-in-table"><li>Merchant id is for above login credentials</li><li>Is internally used for Request Authentication at IDS. </li><li>It's a Constant Value. - `E.g: 14144`</li><li> Initialization iOS : </br> `initKeyboardSDK( .....,MerchantID: "14144",..... )`</li><li> Initialization Android : </br>`myMoSettings.setIntegMerchantId(integMerchantId);`</li></ul>
minimumAmount | String | O | <ul class="ul-in-table"><li>Minimum amount for transaction limit.</li><li>`E.g. 10`</li><li> Initialization iOS : </br> `initKeyboardSDK( .....,minimumAmount: "10",..... )`</li><li> Initialization Android : </br>`myMoSettings.setMinimumAmount(minAmount);`</li></ul>
maximumAmount | String | O |<ul class="ul-in-table"><li>Maximum amount for transaction limit. </li><li>`E.g. 2000` </li><li> Initialization iOS : </br> `initKeyboardSDK( .....,maximumAmount: "2000",.....  )`</li><li> Initialization Android : </br>`myMoSettings.setMaximumAmount(maxAmount);`</li></ul>
languageCode* | String | M | <ul class="ul-in-table"><li>Language code for keyboard.</li><li>Keyboard language will be based on it.</li><li>`E.g. en_US, es_ES etc`</li><li>Note : Currently keyboard supports below language :<br/>en_US :English<br/>es_ES : Spanish</li><li> Initialization iOS : </br> `initKeyboardSDK( .....,languageCode: "en_ES",.....  )`</li><li> Initialization Android : </br>`myMoSettings.setLanguage(language);`</li></ul>
apiURL* | String | M | <ul class="ul-in-table"><li>IDmission Server URL(Environment specific : Demo/UAT/Production)</li><li>`E.g. https://demo.idmission.com/IDS/service/ids/`</li><li> Initialization iOS : </br> `initKeyboardSDK( .....,apiURL: "https://demo.idmission.com/IDS/service/ids/",.....  )`</li><li> Initialization Android : </br>`myMoSettings.setPostURL(postURL);`</li></ul>
bankUserName | String | O | <ul class="ul-in-table"><li>Bank user name.</li><li>Used for bank transactions only.</li><li>`E.g. John`</li><li> Initialization iOS : </br> `initKeyboardSDK( .....,bankUserName: "John",.....  )`</li><li> Initialization Android : </br>`myMoSettings.setBankSenderName(bankUserName);`</li></ul>
bankBranchCode | String | O | <ul class="ul-in-table"><li>Bank branch code.</li><li>Used for bank transactions only.</li><li>`E.g. Bank Of Pakistan`</li><li> Initialization iOS : </br> `initKeyboardSDK( .....,bankBranchCode: "Bank Of Pakistan",.....  )`</li><li> Initialization Android : </br>`myMoSettings.setBranchCode(branchCode);`</li></ul>
bankAccountNumber | String | O | <ul class="ul-in-table"><li>Bank account number</li><li>Used for bank transactions only.</li><li>`E.g. 10333334791`</li><li> Initialization iOS : </br> `initKeyboardSDK( .....,bankAccountNumber: "2635476623",.....  )`</li><li> Initialization Android : </br>`myMoSettings.setBankAccountNo(bankAccountNumber);`</li></ul>
bankAccountType | String | O | <ul class="ul-in-table"><li>Bank Account Type.</li><li>Used for bank transactions only. </li><li>`E.g. Default/Savings/Current.`</li><li> Initialization iOS : </br> `initKeyboardSDK( .....,bankAccountType: "Default",.....  )`</li><li> Initialization Android : </br>`myMoSettings.setBankAccountType(bankAccountType);`</li></ul>
receiversPhoneRequired | String | C | <ul class="ul-in-table"><li>Parameter value must be :‘Y’ or ‘N’</li><li>If receiversPhoneRequired value is “Y” then Keyboard will ask to enter the receiver's phone number.</li><li>Upon entering receiver’s phone number, OTP will be sent on this number.(this OTP need to be enter on a web page to receive money)</li><li>If receiversPhoneRequired value is “N” then Keyboard will not ask to enter the receiver's phone number.</li><li><b><u>Important</u></b>: If you set receiversNoSecurity, you must also include configurations for PhoneLength.</li><li>`E.g Y`</li><li> Initialization iOS : </br> `initKeyboardSDK( .....,receiversPhoneRequired: "Y",.....  )`</li><li> Initialization Android : </br>`myMoSettings.setTxnSecurityReceiverPhoneNo(isReceivePhoneSecurityRequired);`</li></ul>
receiverPhoneNumberLength | String | O | <ul class="ul-in-table"><li>Length of receiver’s phone number.</li><li>If receiverPhoneNumberLength  : Y, then only need to specify its phone number length.</li><li>Only specified length phone numbers will be used for transactions.</li><li>`E.g 10`</li><li> Initialization iOS : </br> `initKeyboardSDK( .....,receiverPhoneNumberLength: "8",.....  )`</li><li> Initialization Android : </br>`myMoSettings.setPhoneNumberLength(receiverPhoneNumberLength);`</li></ul>
selfOTPRequired | String | C |<ul class="ul-in-table"><li>Parameter value must be :‘Y’ or ‘N’</li><li>If Y, then OTP security is enabled, so that during transaction otp will be sent on the sender's phone and the sender will be asked to enter this same otp to proceed with the transaction.</li><li>If N, then then OTP security is disabled and otp will not be sent on the sender phone.</li><li>`E.g Y`</li><li> Initialization iOS : </br> `initKeyboardSDK( .....,selfOTPRequired: "N",.....  )`</li><li> Initialization Android : </br>`myMoSettings.setTxnSecurityOTP(isTransactionOTPSecurityRequired);`</li></ul>
selfPINRequired | String | C |<ul class="ul-in-table"><li>Parameter value must be :‘Y’ or ‘N’</li><li>If Y, then PIN security is enabled and the user will have to specify a pin, so that during the transaction this same pin can be validated at the server.</li><li>If N, then then PIN security is disabled.</li><li>`E.g. Y`</li><li> Initialization iOS : </br> `initKeyboardSDK( .....,selfPINRequired: "Y",.....  )`</li><li> Initialization Android : </br>`myMoSettings.setTxnSecurityPIN(isTransactionPINSecurityRequired);`</li></ul>
selfPINValidationAt | String | C |<ul class="ul-in-table"><li>Parameter values must be : ‘BANK’ or ‘IDM’</li><li>If Pin Security Is used, then need to specify its validation to be done at :IDM or BANK</li><li>`E.g. Y`</li><li> Initialization iOS : </br> `initKeyboardSDK( .....,selfPINValidationAt: "BANK",.....  )`</li><li> Initialization Android : </br>`myMoSettings.setPinValidateAtIDM(validatePINAt);`</li></ul>
SelfPINString | String | C | <ul class="ul-in-table"><li>If pinSecurity : Y, then keyboard will ask to enter customerPIN.</li><li>Used during transaction for validation at server side</li><li>`E.g 1234`</li><li> Initialization iOS : </br> `initKeyboardSDK( .....,SelfPINString: "1234",.....  )`</li><li> Initialization Android : </br>`myMoSettings.setCustomerSecurityPIN(customeTransactionSecurityPIN);`</li></ul>
PINLength | String | C | <ul class="ul-in-table"><li>Length of pin entered by customer.</li><li>If PINLength is specified, then only need to specify its pin length.</li><li>`E.g 4`</li><li> Initialization iOS : </br> `initKeyboardSDK( .....,PINLength: "4",.....  )`</li><li> Initialization Android : </br>`myMoSettings.setPinLength(customerTransactionSecurityPINLength);`</li></ul>

## Android configurable parameters

<h3>MyMo Color Configuration</h3>


Parameter | Type | Description
--------- | ------- | -----------
textColor | String | Text color (e.g.`#c92d64`).
headerBtnTextColor | String | Text color for Send Money,Atm,History and Pay
headerBtnBackgroundColor | String | Background color for Send Money,Atm,History and Pay
editboxBorderColor | String | Editbox background color (eg. `#cfb6df`)
SuccessMsgTextColor | String | Success Message Text Color (eg. `#78777A`)
sendMoneyAmtColor | String | Send Money Amount Color (eg. `#78777A`)
AlertMsgTextColor | String | Alert Message Text Color (eg. `#DC0C23`)
loadMoreTextColor | String | Load More Text Color
calendarDateColor | String | Calendar Icon and Date Text Color
historyListHeaderColor | String | History List Header Color (eg. `#DC0C23`)
ConfirmTxnNoButtonColor | String | Confirm Transaction Popup: No Button Color (eg. `#78777A`)
ConfirmTxnYesButtonColor | String | Confirm Transaction Popup: Yes Button Color (eg. `#DC0C23`)
ConfirmCancelTransactionN oColor | String | Confirm Cancel Transaction Popup: No Button Color (eg. `#78777A`)
ConfirmCancelTransactionY esColor | String | Confirm Cancel Transaction Popup: Yes Button Color (eg. `#DC0C23`)
CancelTxnCloseButtonColor | String | Cancel Transaction Popup: Close Button Color (eg. `#DC0C23`)
CancelTxnConfirmButtonCo lor | String | Cancel Transaction Popup: Confirm Button Color (eg. `#78777A`)


<h3>MyMo Error/Success Message Configuration</h3>

Parameter | Type | Description
--------- | ------- | -----------
textOfErrorCode016 | String | `myMoSettings.setTextOFErrorCode016(tex tOfErrorCode016);`
textOfErrorCode224 | String | `myMoSettings.setTextOFErrorCode224(tex tOfErrorCode224);`
textOfErrorCode236 | String | `myMoSettings.setTextOFErrorCode236(tex tOfErrorCode236);`
textOfErrorCode358 | String | `myMoSettings.setTextOFErrorCode358(tex tOfErrorCode358);`
textOfErrorCode370 | String | `myMoSettings.setTextOFErrorCode370(tex tOfErrorCode370);`
textOfErrorCode428 | String | `myMoSettings.setTextOFErrorCode428(tex tOfErrorCode428);`
textOfErrorCode604 | String | `myMoSettings.setTextOFErrorCode604(tex tOfErrorCode604);`
textOfErrorCode888 | String | `myMoSettings.setTextOFErrorCode888(tex tOfErrorCode888);`
textOfErrorCode999 | String | `myMoSettings.setTextOFErrorCode999(tex tOfErrorCode999);`
textOfErrorCode1003 | String | `myMoSettings.setTextOFErrorCode1003(te xtOfErrorCode1003);`
textOfErrorCode2054 | String | `myMoSettings.setTextOFErrorCode2054(te xtOfErrorCode2054);`
textOfErrorCode2071 | String | `myMoSettings.setTextOFErrorCode2071(te xtOfErrorCode2071);`
textOfErrorCode2077 | String | `myMoSettings.setTextOFErrorCode2077(te xtOfErrorCode2077);`
textOfErrorCode2080 | String | `myMoSettings.setTextOFErrorCode2080(te xtOfErrorCode2080);`
textOfErrorCode2084 | String | `myMoSettings.setTextOFErrorCode2084(te xtOfErrorCode2084);`
textOfErrorCode2086 | String | `myMoSettings.setTextOFErrorCode2086(te xtOfErrorCode2086);`
textOfErrorCode2087 | String | `myMoSettings.setTextOFErrorCode2087(te xtOfErrorCode2087);`
textOfErrorCode2589 | String | `myMoSettings.setTextOFErrorCode2589(te xtOfErrorCode2589);`
textOfErrorCode5000 | String | `myMoSettings.setTextOFErrorCode5000(te xtOfErrorCode5000);`
textOfErrorCode5010 | String | `myMoSettings.setTextOFErrorCode5010(te xtOfErrorCode5010);`
textOfErrorCode3059 | String | `myMoSettings.setTextOFErrorCode3059(te xtOfErrorCode3059);`
textOfValidation001 | String | `myMoSettings.setTextOfValidation001(text OfValidation001);`
textOfValidation002 | String | `myMoSettings.setTextOfValidation002(text OfValidation002);`
textOfValidation003 | String | `myMoSettings.setTextOfValidation003(text OfValidation003);`
textOfValidation004 | String | `myMoSettings.setTextOfValidation004(text OfValidation004);`
textOfValidation005 | String | `myMoSettings.setTextOfValidation005(text OfValidation005);`
textOfValidation006 | String | `myMoSettings.setTextOfValidation006(text OfValidation006);`
textOfValidation007 | String | `myMoSettings.setTextOfValidation007(text OfValidation007);`
textOfValidation008 | String | `myMoSettings.setTextOfValidation008(text OfValidation008);`
textOfValidation009 | String | `myMoSettings.setTextOfValidation009(text OfValidation009);`
textOfValidation011 | String |  `myMoSettings.setTextOfValidation011(text OfValidation011);`


<p>Note : Description for these ErrorCodes and Validations mentioned at point 3.6</p>



<h3>MyMo Label Configuration</h3>

Parameter | Type | Description
--------- | ------- | -----------
sendMoneyLabel | String | Label for Send Money Button
sendToAtmLabel | String | Label for Send to ATMButton
historyLabel | String | Label for History Button
payLabel | String | Label for Pay Button
successMsgTextLabel | String | Label for Success Message Text


<h3>MyMo Icon Configuration</h3>

Parameter | Type | Description
--------- | ------- | -----------
mymoIconbitmap | Bitmap | MyMo Icon
downArrowIconbitmap | Bitmap | Down arrow Icon
processingIconbitmap | Bitmap | Processing Icon
txnSuccessIconbitmap | Bitmap | Transaction Success Icon
contactIconbitmap | Bitmap | Contact Icon
alertIconbitmap | Bitmap | Alert Icon

## iOS configurable parameters

<h3>MyMo Label/Color/UI Configurations</h3>

Parameter | Type |  |Description
--------- | ------- | ----------- | -----------
UIConfigDictionary | Dictionary | O | Dictionary should have following keys with your user default as value:<li>ImagePath_OF_SelectionArrow</li><li>ImagePath_OF_Contact</li><li>ImagePath_OF_Processing</li><li>ImagePath_OF_TransactionSuccess</li><li>ImagePath_OF_ErrorAlert</li><li>Text_OF_SendMoney_Button</li><li>Text_OF_SendToATM_Button</li><li>Text_OF_History_Button</li><li>Text_OF_Send_Button</li><li>Text_OF_Transaction_SuccessMessage</li><li>HexColor_OF_Keyboard_Header</li><li>HexColor_OF_Header_Button</li><li>HexColor_OF_Header_Button_Text</li><li>HexColor_OF_AmountText</li><li>HexColor_OF_AmountBackgroundColor</li><li>HexColor_OF_Transaction_SuccessMessage</li><li>HexColor_OF_Transaction_SuccessAmount</li><li>HexColor_OF_AlerMessage</li><li>HexColor_OF_HistoryList_Header</li><li>HexColor_OF_ConfirmTransaction_CofirmButton</li><li>HexColor_OF_ConfirmTransaction_CancelButton</li><li>HexColor_OF_CancelTransaction_CancelTransactionButton</li><li>HexColor_OF_CancelTransaction_CloseButton</li><li>HexColor_OF_CancelTransactionConfirmation_YESButton</li><li>HexColor_OF_CancelTransactionConfirmation_NOButton</li><li>HexColor_OF_Calendar_SelectDateButton</li><li>HexColor_OF_Calendar_CancelButton</li><li>HexColor_OF_Calendar_Button_Text</li><li>HexColor_OF_LoadMore_Button_Text</li><li>Text_For_ErrorCode_016</li><li>Text_For_ErrorCode_224</li><li>Text_For_ErrorCode_236</li><li>Text_For_ErrorCode_358</li><li>Text_For_ErrorCode_370</li><li>Text_For_ErrorCode_428</li><li>Text_For_ErrorCode_501</li><li>Text_For_ErrorCode_604</li><li>Text_For_ErrorCode_888</li><li>Text_For_ErrorCode_1003</li><li>Text_For_ErrorCode_2054</li><li>Text_For_ErrorCode_2071</li><li>Text_For_ErrorCode_2077</li><li>Text_For_ErrorCode_2080</li><li>Text_For_ErrorCode_2082</li><li>Text_For_ErrorCode_2084</li><li>Text_For_ErrorCode_2086</li><li>Text_For_ErrorCode_2087</li><li>Text_For_ErrorCode_2589</li><li>Text_For_ErrorCode_3059</li><li>Text_For_ErrorCode_5000</li><li>Text_For_ErrorCode_5010</li><li>Text_For_Validation_001</li><li>Text_For_Validation_002</li><li>Text_For_Validation_003</li><li>Text_For_Validation_004</li><li>Text_For_Validation_005</li><li>Text_For_Validation_006</li><li>Text_For_Validation_007</li><li>Text_For_Validation_008</li><li>Text_For_Validation_009</li><li>Text_For_Validation_010</li><li>Text_For_Validation_011</li><li>Text_For_Validation_012</li>


# Image Sizes
## iOS Image Sizes 
<h3>Icon sizes for icons used in MyMo Keyboard</h3>

Icon Name | Size (in Pixels)
--------- | -------
Bank Logo Icon | @1x = (45x45), <br/>@2x = (90x90), <br/> @3x = (135x135)
Down arrow Icon | @1x = (20x10), <br/>@2x = (40x20), <br/>@3x = (60x30)
Processing Icon | @1x = (80x80), <br/>@2x = (160x160), <br/>@3x = (240x240
Transaction Success Icon | @1x = (50x50), <br/>@2x = (100x100), <br/>@3x = (150x150)
Contact Icon | @1x = (36x36), <br/>@2x = (72x72), <br/>@3x = (108x108)
Alert Icon | @1x = (50x50), <br/>@2x = (100x100), <br/>@3x = (150x150)

## Android Image Sizes 
<h3>Icon sizes for icons used in MyMo Keyboard</h3>

Icon Name | Size (in Pixels)
--------- | -------
MyMo Icon | 150 x 150
Down arrow Icon | 48 x 28
Processing Icon | 100 x 100
Transaction Success Icon | 150 x 150
Contact Icon | 60 x 60
Alert Icon | 72 x 72


# Error Status Message Handling 


<span style="white-space:nowrap">Error Code</span> | Meaning
---------- | -------
000 | Success
016 | Invalid input XML
224 | Invalid login credentials.
236 | Invalid login credentials for merchant
358 | Customer Not Found.
370 | Invalid phone number.
428 | Customer data is not available or Customer not found.
501 | Merchant not found
604 | Invalid login id or password.
888 | Customer Not Enrolled in Program
1003 | No records found.
2054 | OTP verification is failed. Please enter the correct OTP.
2071 | Insufficient balance!
2077 | Transaction point count of sender greater than 30000
2080 | Transaction Pin Verification is Failed.
2082 | Invalid ATM Withdrawal amount
2084 | Amount exceeds limit
2086 | Transaction count exceeds limit
2087 | Transaction count exceeds limit
2341 | Insufficient balance
2589 | Código de respuesta
3059 | User is already mapped with another hardware.Please contact your administrator
5000 | System Error
5010 | Failed to generate payment link

<i>Table 1: Error codes and respective message from Server side</i>

<br/>
    
<span style="white-space:nowrap">App Side Validation Code</span> | Validation Messages
---------- | -------
Validation 001 | Please enter amount
Validation 002 | Please enter OTP
Validation 003 | Please enter PIN
Validation 004 | Please enter (Customer_Security_PIN_Length) digit PIN
Validation 005 | Please enter Phone Number
Validation 006 | Amount should be less than max value
Validation 007 | Amount should be greater than min value
Validation 008 | Amount should be in multiple of 100
Validation 009 | Phone number should be valid digit number
Validation 010 | Phone number not available
Validation 011 | Generate OTP Failed...
Validation 012 | Unable to process the request

<i>Table 2: Validation codes and respective message from App side</i>


# Troubleshooting

## iOS 
### initKeyboardSDK function
    <ul>
    <li>On initializing the SDK using initKeyboardSDK() method, send all parameter ask by method (e.g as shown in above section number 5)</li>
    </ul>    
### initKeyboardSDK function
    <ul>
    <li>To setup Keyboard SDK make sure you have to follow steps mentioned in above section number 4.1</li>
    <li>To send data to the keyboard SDK from Host App, an App group should be created to share data between Host App & Keyboard Extension. Please refer to the standard Apple Document for how to enable the App Group for Bundle identifier.</li>
    <li>To send Image to Keyboard SDK, you can store images in directory using NSFileManger class at shared path & send that path to Keyboard SDK.</li>
    </ul>    

## Android 
### MyMoSettings function
    <ul>
    <li>On initializing the SDK using enableMyMo() method, send all parameter ask by method (e.g as shown in above section 3.2 Initializing the SDK )</li>
    </ul>    
### KeyboardSDK
    <ul>
    <li>To setup Keyboard SDK make sure you have to follow steps mentioned in above section 3. Minimum Requirements and Setup</li>
    <li>To send data to the keyboard SDK from Host App, an App group should be created to share data between Host App Keyboard Extensions.</li>
    <li>To send Image to Keyboard SDK, you can set Bitmap of image to specific icon of keyboard using methods described in above section 3.2 Initializing the SDK (eg. myMoSettings.setMyMoBitmapDrawable(mymoIconbitmap);) </li>
    </ul>    
