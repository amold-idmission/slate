---
title: MyMo SDK

language_tabs: # must be one of https://git.io/vQNgJ
  - java 
  - swift


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
    

# SDK integration in iOS Project 

## Project Setup
<strong>Step 1 :</strong> Open Xcode.

    <ul>
    <li>To create a new project, continue to <b>Step 2.</b></li>
    <li>If you have an existing iOS project, proceed to <b>Step 3.</b></li>
    </ul>
    <br/>
    <br/>
    
<strong>Step 2 :</strong> Create a new iOS project by navigating to the path `File > New > Project`, as shown on <i>Figure 1.</i>

    <div style="text-align:center; width:50%" >
    <img src="../images/iOS/Figure1.png" style="max-width:520px"/><br/>
    <i>Figure 1: SingleView project/app.</i>
    </div>
    <br/>
    
    <b><u>Note</u></b>: Below <i>Figure 2</i> shows an example with the project name “MyMoDemo”.
    
    <div style="text-align:center; width:50%" >
    <img src="../images/iOS/Figure2.png" style="max-width:520px"/><br/>
    <i>Figure 2: Set project/app name.</i>
    </div>
    <br/>
    <br/>

<strong>Step 3 :</strong> Create a new <b>Target</b> using one of the following two methods:

    <ul>
    <li>Navigate to `Editor > Add Target > Custom Keyboard Extension` as shown on <i>Figure 3</i> or</b></li>
    <li>Click the + button located below the <b>Target</b> section as shown on <i>Figure 4</i></b></li>
    </ul>

    <div style="text-align:center; width:50%" >
    <img src="../images/iOS/Figure3.png" style="max-width:520px"/><br/>
    <i>Figure 3: Add target as a Custom Keyboard Extension.</i>
    </div>
    <br/>
    <br/>
    
    <div style="text-align:center; width:50%" >
    <img src="../images/iOS/Figure4.png" style="max-width:520px"/><br/>
    <i>Figure 4: Add target.</i>
    </div>
    <br/>
    <br/>

<strong>Step 4 :</strong> Use the <b>Product Name</b> box to set the custom keyboard name.

    <b><u>Note</u></b>: Below <i>Figure 5</i> shows the keyboard name “MyMoKeyboard”.

    <div style="text-align:center; width:50%" >
    <img src="../images/iOS/Figure5.png" style="max-width:520px"/><br/>
    <i>Figure 5: Set name for keyboard extension.</i>
    </div>
    <br/>
    <br/>

<strong>Step 5 :</strong> Open the custom keyboard extension's <b>info.plist</b> file.

    <ul>
    <li>Navigate to `NSExtension > NSExtensionAttributes > RequestsOpenAccess`.</b></li>
    <li>Change the value of `RequestsOpenAccess` to `YES`, as shown in <i>Figure 6.</i></li>
    </ul>
    <br/>

    <div style="text-align:center; width:50%" >
    <img src="../images/iOS/Figure6.png" style="max-width:520px"/><br/>
    <i>Figure 6: Keyboard extension’s info.plist</i>
    </div>
    <br/>
    <br/>

<strong>Step 6 :</strong> Adding <b>KeyboardSDK.Framework</b> File.

    <ul>
    <li>Drag and drop the `KeyboardSDK.framework` file at root level of your project.</b></li>
    <li>Select the <b>Copy items if needed</b> checkbox and select the target as your project name, as shown in <i>Figure 7.</i></li>
    </ul>
    <br/>

    <div style="text-align:center; width:50%" >
    <img src="../images/iOS/Figure7.png" style="max-width:520px"/><br/>
    <i>Figure 7: Add keyboardSDK in host app</i>
    </div>
    <br/>
    <br/>

<strong>Step 7 :</strong> Set Framework as <b>Embed & Sign</b> in the General tab.

    <ul>
    <li>After adding framework in your project navigate to `Project Target > General > Frameworks, Libraries, and Embedded Content`</li>
    <li>Verify that `KeyboardSDK.framework` was added.</li>
    <li>Set `KeyboardSDK.framework` as `Embed & Sign`, as shown in <i>Figure 8.</i></li>
    </ul>
    <br/>

    <div style="text-align:center; width:50%" >
    <img src="../images/iOS/Figure8.png" style="max-width:520px"/><br/>
    <i>Figure 8: Embed and sign keyboardSDK.</i>
    </div>
    <br/>
    <br/>

<strong>Step 8 :</strong> Setting app groups.

    <ul>
    <li>Create provisioning profiles for your app and keyboard extension.</li>
    <li>Add `App Groups` capability for both targets (your app and keyboard extension).</li>
    <li>Enable same `App Group name (e.g groups.idmission.mymodemo)` for both targets (your app and keyboard extension).</li>
    <li><b>Host App</b> : Select `Host App Target > Signing & Capabilities > Capabilities > App Groups`, as shown below <i>Figure 9.</i></li>
    </ul>

    <div style="text-align:center; width:50%" >
    <img src="../images/iOS/Figure9.png" style="max-width:520px"/><br/>
    <i>Figure 9: Enable app group in host app.</i>
    </div>
    <br/>

    <ul>
    <li><b>Extension App</b> : Select `Keyboard Extension Target > Signing & Capabilities > Capabilities > App Groups`, as shown below <i>Figure 10.</i></li>
    </ul>
    </ul>

    <div style="text-align:center; width:50%" >
    <img src="../images/iOS/Figure10.png" style="max-width:520px"/><br/>
    <i>Figure 10: Enable app group in keyboard extension.</i>
    </div>
    <br/>

    <ul>
    <li><b>Important</b> : Setting app groups is very important for send/share/pass data between your app and the keyboard extension. To create a provisioning profile and enable App Group capabilities, please refer to the [Adding Capabilities to Your App](https://developer.apple.com/documentation/xcode/adding_capabilities_to_your_app). (Apple Support web page).</li>
    </ul>
    </ul>
    </br>
    </br>
    
<strong>Step 9 :</strong> Info.plist configurations

To get access to the contact list from your app, add the key and its description to your project’s info.plist file as explained in the following steps:

    <ul>
    <li>Navigate to your project’s info.plist file.</li>
    <li>Add key `Privacy - Contacts Usage Description`</li>
    <li>In the `Info.plist` file, locate `Privacy – Contacts Usage Description` and set the value to `Access is needed to send an amount to the receiver's number`, as shown on <i>Figure 11.</i></li>
    </ul>

    <div style="text-align:center; width:50%" >
    <img src="../images/iOS/Figure11.png" style="max-width:520px"/><br/>
    <i>Figure 11: Enable contact app permission in host app info.plist.</i>
    </div>
    <br/>


## Initialization of SDK

You can choose to initialize the SDK with or without ConfigurableUI. This section details how to set each of these options.

### Initializing the SDK Without ConfigurableUI
    <ul>
    <li>Navigate to `Keyboard Extension’s > KeyboardViewController.swift`</li>
    <li>Remove all code in `KeyboardViewController.swift`</li>
    <li>Copy the below mentioned code and paste as it is in the `keyboardViewController.swift.`</li>
    <li>You may set to use or not use shared values from the Host App. Choose one of the following:</li>
        <ul>
        <li>If you do not want to use shared values from Host App, directly set parameter values right after the parameter name without using `UserDefaults.`</li>
        <li>To use shared values from Host App, use: `UserDefaults(suiteName: “group.idmission.MyMoDemo”).`</li>
        </ul>
    <li>Set the following `UserDefaults` values in your Host App, and use the same `UserDefaults` string to enable access to these values in the Keyboard Extension:</li>
    </ul>

```swift
    
    import UIKit
    import KeyboardSDK
     
    class KeyboardViewController: KeyboardParentViewController {
     
        var userDefaults = UserDefaults(suiteName: "group.idmission.MyMoDemo")
     
        override func viewDidLoad() {
            super.viewDidLoad()
     
            initKeyboardSDK(enableMyMo: userDefaults?.string(forKey: "Enable_MyMO") ?? "",
                            showSendMoney: userDefaults?.string(forKey: "isShowSendMoney") ?? "",
                            showSendToATM: userDefaults?.string(forKey: "isShowSendToATM") ?? "",
                            showHistory: userDefaults?.string(forKey: "isShowHistory") ?? "",
                            applicationCode: userDefaults?.string(forKey: "Application_Code") ?? "",
                            senderName: userDefaults?.string(forKey: "Sender_Name") ?? "",
                            loginID: userDefaults?.string(forKey: "Login_Id") ?? "",
                            Password: userDefaults?.string(forKey: "Login_Password") ?? "",
                            MerchantID: userDefaults?.string(forKey: "Merchant_Id") ?? "",
                            PhoneNumber: userDefaults?.string(forKey: "Phone_Number") ?? "",
                            CustomerCode: userDefaults?.string(forKey: "Customer_Code") ?? "",
                            CountryCode: userDefaults?.string(forKey: "Country_Code") ?? "",
                            CurrencyCode: userDefaults?.string(forKey: "Currency_Code") ?? "",
                            CurrencySymbol: userDefaults?.string(forKey: "Currency_Symbol") ?? "",
                            minimumAmount: userDefaults?.string(forKey: "Minimum_Amount") ?? "",
                            maximumAmount: userDefaults?.string(forKey: "Maximum_Amount") ?? "",
                            languageCode: userDefaults?.string(forKey: "Language_Code") ?? "",
                            apiURL: userDefaults?.string(forKey: "Url") ?? "",
                            bankUserName: userDefaults?.string(forKey: "Bank_User_Name") ?? "",
                            bankBranchCode: userDefaults?.string(forKey: "Bank_Branch_Code") ?? "",
                            bankAccountNumber: userDefaults?.string(forKey: "Bank_Account_No") ?? "",
                            bankAccountType: userDefaults?.string(forKey: "Bank_Account_Type") ?? "",
                            receiversPhoneRequired: userDefaults?.string(forKey: "PhoneNo_Security_Required") ?? "",
                            receiverPhoneNumberLength: userDefaults?.string(forKey: "Phone_Number_Length") ?? "",
                            selfOTPRequired: userDefaults?.string(forKey: "OTP_Security_Required") ?? "",
                            selfPINRequired: userDefaults?.string(forKey: "PIN_Security_Required") ?? "",
                            selfPINValidationAt: userDefaults?.string(forKey: "PIN_Validate_At") ?? "",
                            SelfPINString: userDefaults?.string(forKey: "Customer_Security_PIN") ?? "",
                            PINLength: userDefaults?.string(forKey: "PIN_Length") ?? "",
                            receiversEmailRequired: userDefaults?.string(forKey: "Email_Security_Required") ?? "",
                            receiversFaceRequired: userDefaults?.string(forKey: "Face_Security_Required") ?? "")
        }
    }

```
    <ul>
    <li><b>Important</b> : In above code <ul>
    <li>Make changes in the `App Group String` as created in <b>Step 8.</b></li>
    <li>Make changes in the `UserDefault` value according to your convenience.</li>
    </ul>
    </li>
    <li>Build and run the project.</li>
    </ul>


### Initializing the SDK With ConfigurableUI
    <ul>
    <li>Navigate to `Keyboard Extension’s > KeyboardViewController.swift`</li>
    <li>Remove all code in `KeyboardViewController.swift`</li>
    <li>Copy the below mentioned code and paste as it is in the `keyboardViewController.swift.`</li>
    <li>You may set to use or not use shared values from the Host App. Choose one of the following:</li>
        <ul>
        <li>If you do not want to use shared values from Host App, directly set parameter values right after the parameter name without using `UserDefaults.`</li>
        <li>To use shared values from Host App, use: `UserDefaults(suiteName: “group.idmission.MyMoDemo”).`</li>
        </ul>
    <li>Set the following `UserDefaults` values in your Host App, and use the same `UserDefaults` string to enable access to these values in the Keyboard Extension:</li>
    <li>Here we need to add “UIConfigDictionary” as an extra parameter to the Keyboard initialised method for making configurable text, colour, ImagePath & error messages</li>
    <li>In your host app Image path should be stored in the document directory using FileManager class with ApplicationGroupIdentifier, So that It can be accessible in extension.</li>
    </ul>

```swift
    
    import UIKit
    import KeyboardSDK
     
    class KeyboardViewController: KeyboardParentViewController {
     
        var userDefaults = UserDefaults(suiteName: "group.idmission.MyMoDemo")
     
        override func viewDidLoad() {
            super.viewDidLoad()
     
            /* Image Configuration Dictionary Value*/
            let ImagePath_For_BankLogo = userDefaults?.string(forKey: "ImagePath_For_BankLogo") ?? ""
            let ImagePath_For_SelectionArrow = userDefaults?.string(forKey: "ImagePath_For_SelectionArrow") ?? ""
            let ImagePath_For_Contact = userDefaults?.string(forKey: "ImagePath_For_Contact") ?? ""
            let ImagePath_For_Processing = userDefaults?.string(forKey: "ImagePath_For_Processing") ?? ""
            let ImagePath_For_TransactionSuccess = userDefaults?.string(forKey: "ImagePath_For_TransactionSuccess") ?? ""
            let ImagePath_For_ErrorAlert = userDefaults?.string(forKey: "ImagePath_For_ErrorAlert") ?? ""
     
            /* Text Configuration Dictionary Value*/
            let Text_For_SendMoney_Button = userDefaults?.string(forKey: "Text_For_Send_Money") ?? ""
            let Text_For_SendToATM_Button = userDefaults?.string(forKey: "Text_For_Send_To_ATM") ?? ""
            let Text_For_History_Button = userDefaults?.string(forKey: "Text_For_History") ?? ""
            let Text_For_Send_Button = userDefaults?.string(forKey: "Text_For_Send") ?? ""
            let Text_For_Transaction_SuccessMessage = userDefaults?.string(forKey: "Text_For_Transaction_SuccessMessage") ?? ""
     
            /* Color Configuration Dictionary Value*/
            let HexColor_For_Keyboard_Header = userDefaults?.string(forKey: "HexColor_For_Keyboard_Header") ?? ""
            let HexColor_For_Header_Button = userDefaults?.string(forKey: "HexColor_For_Header_Button") ?? ""
            let HexColor_For_Header_Button_Text = userDefaults?.string(forKey: "HexColor_For_Header_Button_Text") ?? ""
            let HexColor_For_AmountText = userDefaults?.string(forKey: "HexColor_For_AmountText") ?? ""
            let HexColor_For_AmountBackgroundColor = userDefaults?.string(forKey: "HexColor_For_AmountBackgroundColor") ?? ""
            let HexColor_For_Transaction_SuccessMessage = userDefaults?.string(forKey: "HexColor_For_Transaction_SuccessMessage") ?? ""
            let HexColor_For_Transaction_SuccessAmount = userDefaults?.string(forKey: "HexColor_For_Transaction_SuccessAmount") ?? ""
            let HexColor_For_AlerMessage = userDefaults?.string(forKey: "HexColor_For_AlerMessage") ?? ""
            let HexColor_For_HistoryList_Header = userDefaults?.string(forKey: "HexColor_For_HistoryList_Header") ?? ""
            let HexColor_For_ConfirmTransaction_CofirmButton = userDefaults?.string(forKey: "HexColor_For_ConfirmTransaction_CofirmButton") ?? ""
            let HexColor_For_ConfirmTransaction_CancelButton = userDefaults?.string(forKey: "HexColor_For_ConfirmTransaction_CancelButton") ?? ""
            let HexColor_For_CancelTransaction_CancelTransactionButton = userDefaults?.string(forKey: "HexColor_For_CancelTransaction_CancelTransactionButton") ?? ""
            let HexColor_For_CancelTransaction_CloseButton = userDefaults?.string(forKey: "HexColor_For_CancelTransaction_CloseButton") ?? ""
            let HexColor_For_CancelTransactionConfirmation_YESButton = userDefaults?.string(forKey: "HexColor_For_CancelTransactionConfirmation_YESButton") ?? ""
            let HexColor_For_CancelTransactionConfirmation_NOButton = userDefaults?.string(forKey: "HexColor_For_CancelTransactionConfirmation_NOButton") ?? ""
            let HexColor_For_Calendar_SelectDateButton = userDefaults?.string(forKey: "HexColor_For_Calendar_SelectDateButton") ?? ""
            let HexColor_For_Calendar_CancelButton = userDefaults?.string(forKey: "HexColor_For_Calendar_CancelButton") ?? ""
            let HexColor_For_Calendar_Button_Text = userDefaults?.string(forKey: "HexColor_For_Calendar_Button_Text") ?? ""
            let HexColor_For_LoadMore_Button_Text = userDefaults?.string(forKey: "HexColor_For_LoadMore_Button_Text") ?? ""
     
            /* ErrorCode Messages Configuration Dictionary Value*/
            let Text_For_ErrorCode_016 = userDefaults?.string(forKey: "Text_For_ErrorCode_016") ?? ""
            let Text_For_ErrorCode_224 = userDefaults?.string(forKey: "Text_For_ErrorCode_224") ?? ""
            let Text_For_ErrorCode_236 = userDefaults?.string(forKey: "Text_For_ErrorCode_236") ?? ""
            let Text_For_ErrorCode_358 = userDefaults?.string(forKey: "Text_For_ErrorCode_358") ?? ""
            let Text_For_ErrorCode_370 = userDefaults?.string(forKey: "Text_For_ErrorCode_370") ?? ""
            let Text_For_ErrorCode_428 = userDefaults?.string(forKey: "Text_For_ErrorCode_428") ?? ""
            let Text_For_ErrorCode_501 = userDefaults?.string(forKey: "Text_For_ErrorCode_501") ?? ""
            let Text_For_ErrorCode_604 = userDefaults?.string(forKey: "Text_For_ErrorCode_604") ?? ""
            let Text_For_ErrorCode_888 = userDefaults?.string(forKey: "Text_For_ErrorCode_888") ?? ""
            let Text_For_ErrorCode_1003 = userDefaults?.string(forKey: "Text_For_ErrorCode_1003") ?? ""
            let Text_For_ErrorCode_2054 = userDefaults?.string(forKey: "Text_For_ErrorCode_2054") ?? ""
            let Text_For_ErrorCode_2071 = userDefaults?.string(forKey: "Text_For_ErrorCode_2071") ?? ""
            let Text_For_ErrorCode_2077 = userDefaults?.string(forKey: "Text_For_ErrorCode_2077") ?? ""
            let Text_For_ErrorCode_2080 = userDefaults?.string(forKey: "Text_For_ErrorCode_2080") ?? ""
            let Text_For_ErrorCode_2082 = userDefaults?.string(forKey: "Text_For_ErrorCode_2082") ?? ""
            let Text_For_ErrorCode_2084 = userDefaults?.string(forKey: "Text_For_ErrorCode_2084") ?? ""
            let Text_For_ErrorCode_2086 = userDefaults?.string(forKey: "Text_For_ErrorCode_2086") ?? ""
            let Text_For_ErrorCode_2087 = userDefaults?.string(forKey: "Text_For_ErrorCode_2087") ?? ""
            let Text_For_ErrorCode_2589 = userDefaults?.string(forKey: "Text_For_ErrorCode_2589") ?? ""
            let Text_For_ErrorCode_3059 = userDefaults?.string(forKey: "Text_For_ErrorCode_3059") ?? ""
            let Text_For_ErrorCode_5000 = userDefaults?.string(forKey: "Text_For_ErrorCode_5000") ?? ""
            let Text_For_ErrorCode_5010 = userDefaults?.string(forKey: "Text_For_ErrorCode_5010") ?? ""
            let Text_For_Validation_001 = userDefaults?.string(forKey: "Text_For_Validation_001") ?? ""
            let Text_For_Validation_002 = userDefaults?.string(forKey: "Text_For_Validation_002") ?? ""
            let Text_For_Validation_003 = userDefaults?.string(forKey: "Text_For_Validation_003") ?? ""
            let Text_For_Validation_004 = userDefaults?.string(forKey: "Text_For_Validation_004") ?? ""
            let Text_For_Validation_005 = userDefaults?.string(forKey: "Text_For_Validation_005") ?? ""
            let Text_For_Validation_006 = userDefaults?.string(forKey: "Text_For_Validation_006") ?? ""
            let Text_For_Validation_007 = userDefaults?.string(forKey: "Text_For_Validation_007") ?? ""
            let Text_For_Validation_008 = userDefaults?.string(forKey: "Text_For_Validation_008") ?? ""
            let Text_For_Validation_009 = userDefaults?.string(forKey: "Text_For_Validation_009") ?? ""
            let Text_For_Validation_010 = userDefaults?.string(forKey: "Text_For_Validation_010") ?? ""
            let Text_For_Validation_011 = userDefaults?.string(forKey: "Text_For_Validation_011") ?? ""
            let Text_For_Validation_012 = userDefaults?.string(forKey: "Text_For_Validation_012") ?? ""
     
            /* Prepare Dictionary to Pass Configurable Values in Keyboard SDK*/
            let UI_Dictionary = ["ImagePath_OF_BankLogo" : ImagePath_For_BankLogo,
                                 "ImagePath_OF_SelectionArrow" : ImagePath_For_SelectionArrow,
                                 "ImagePath_OF_Contact" : ImagePath_For_Contact,
                                 "ImagePath_OF_Processing" : ImagePath_For_Processing,
                                 "ImagePath_OF_TransactionSuccess" : ImagePath_For_TransactionSuccess,
                                 "ImagePath_OF_ErrorAlert" : ImagePath_For_ErrorAlert,
     
                                 "Text_OF_SendMoney_Button" : Text_For_SendMoney_Button,
                                 "Text_OF_SendToATM_Button" : Text_For_SendToATM_Button,
                                 "Text_OF_History_Button" : Text_For_History_Button,
                                 "Text_OF_Send_Button" : Text_For_Send_Button,
                                 "Text_OF_Transaction_SuccessMessage" : Text_For_Transaction_SuccessMessage,
     
                                 "HexColor_OF_Keyboard_Header": HexColor_For_Keyboard_Header,
                                 "HexColor_OF_Header_Button": HexColor_For_Header_Button,
                                 "HexColor_OF_Header_Button_Text": HexColor_For_Header_Button_Text,
                                 "HexColor_OF_AmountText": HexColor_For_AmountText,
                                 "HexColor_OF_AmountBackgroundColor": HexColor_For_AmountBackgroundColor,
                                 "HexColor_OF_Transaction_SuccessMessage": HexColor_For_Transaction_SuccessMessage,
                                 "HexColor_OF_Transaction_SuccessAmount": HexColor_For_Transaction_SuccessAmount,
                                 "HexColor_OF_AlerMessage": HexColor_For_AlerMessage,
                                 "HexColor_OF_HistoryList_Header": HexColor_For_HistoryList_Header,
                                 "HexColor_OF_ConfirmTransaction_CofirmButton": HexColor_For_ConfirmTransaction_CofirmButton,
                                 "HexColor_OF_ConfirmTransaction_CancelButton": HexColor_For_ConfirmTransaction_CancelButton,
                                 "HexColor_OF_CancelTransaction_CancelTransactionButton": HexColor_For_CancelTransaction_CancelTransactionButton,
                                 "HexColor_OF_CancelTransaction_CloseButton": HexColor_For_CancelTransaction_CloseButton,
                                 "HexColor_OF_CancelTransactionConfirmation_YESButton": HexColor_For_CancelTransactionConfirmation_YESButton,
                                 "HexColor_OF_CancelTransactionConfirmation_NOButton": HexColor_For_CancelTransactionConfirmation_NOButton,
                                 "HexColor_OF_Calendar_SelectDateButton": HexColor_For_Calendar_SelectDateButton,
                                 "HexColor_OF_Calendar_CancelButton": HexColor_For_Calendar_CancelButton,
                                 "HexColor_OF_Calendar_Button_Text": HexColor_For_Calendar_Button_Text,
                                 "HexColor_OF_LoadMore_Button_Text": HexColor_For_LoadMore_Button_Text,
     
                                 "Text_OF_ErrorCode_016":Text_For_ErrorCode_016,
                                 "Text_OF_ErrorCode_224":Text_For_ErrorCode_224,
                                 "Text_OF_ErrorCode_236":Text_For_ErrorCode_236,
                                 "Text_OF_ErrorCode_358":Text_For_ErrorCode_358,
                                 "Text_OF_ErrorCode_370":Text_For_ErrorCode_370,
                                 "Text_OF_ErrorCode_428":Text_For_ErrorCode_428,
                                 "Text_OF_ErrorCode_501":Text_For_ErrorCode_501,
                                 "Text_OF_ErrorCode_604":Text_For_ErrorCode_604,
                                 "Text_OF_ErrorCode_888":Text_For_ErrorCode_888,
                                 "Text_OF_ErrorCode_1003":Text_For_ErrorCode_1003,
                                 "Text_OF_ErrorCode_2054":Text_For_ErrorCode_2054,
                                 "Text_OF_ErrorCode_2071":Text_For_ErrorCode_2071,
                                 "Text_OF_ErrorCode_2077":Text_For_ErrorCode_2077,
                                 "Text_OF_ErrorCode_2080":Text_For_ErrorCode_2080,
                                 "Text_OF_ErrorCode_2082":Text_For_ErrorCode_2082,
                                 "Text_OF_ErrorCode_2084":Text_For_ErrorCode_2084,
                                 "Text_OF_ErrorCode_2086":Text_For_ErrorCode_2086,
                                 "Text_OF_ErrorCode_2087":Text_For_ErrorCode_2087,
                                 "Text_OF_ErrorCode_2589":Text_For_ErrorCode_2589,
                                 "Text_OF_ErrorCode_3059":Text_For_ErrorCode_3059,
                                 "Text_OF_ErrorCode_5000":Text_For_ErrorCode_5000,
                                 "Text_OF_ErrorCode_5010":Text_For_ErrorCode_5010,
                                 "Text_OF_Validation_001":Text_For_Validation_001,
                                 "Text_OF_Validation_002":Text_For_Validation_002,
                                 "Text_OF_Validation_003":Text_For_Validation_003,
                                 "Text_OF_Validation_004":Text_For_Validation_004,
                                 "Text_OF_Validation_005":Text_For_Validation_005,
                                 "Text_OF_Validation_006":Text_For_Validation_006,
                                 "Text_OF_Validation_007":Text_For_Validation_007,
                                 "Text_OF_Validation_008":Text_For_Validation_008,
                                 "Text_OF_Validation_009":Text_For_Validation_009,
                                 "Text_OF_Validation_010":Text_For_Validation_010,
                                 "Text_OF_Validation_011":Text_For_Validation_011,
                                 "Text_OF_Validation_012":Text_For_Validation_012] as NSMutableDictionary
     
            initKeyboardSDK_WithUIConfiguration(enableMyMo: userDefaults?.string(forKey: "Enable_MyMO") ?? "",
                                                showSendMoney: userDefaults?.string(forKey: "isShowSendMoney") ?? "",
                                                showSendToATM: userDefaults?.string(forKey: "isShowSendToATM") ?? "",
                                                showHistory: userDefaults?.string(forKey: "isShowHistory") ?? "",
                                                applicationCode: userDefaults?.string(forKey: "Application_Code") ?? "",
                                                senderName: userDefaults?.string(forKey: "Sender_Name") ?? "",
                                                loginID: userDefaults?.string(forKey: "Login_Id") ?? "",
                                                Password: userDefaults?.string(forKey: "Login_Password") ?? "",
                                                MerchantID: userDefaults?.string(forKey: "Merchant_Id") ?? "",
                                                PhoneNumber: userDefaults?.string(forKey: "Phone_Number") ?? "",
                                                CustomerCode: userDefaults?.string(forKey: "Customer_Code") ?? "",
                                                CountryCode: userDefaults?.string(forKey: "Country_Code") ?? "",
                                                CurrencyCode: userDefaults?.string(forKey: "Currency_Code") ?? "",
                                                CurrencySymbol: userDefaults?.string(forKey: "Currency_Symbol") ?? "",
                                                minimumAmount: userDefaults?.string(forKey: "Minimum_Amount") ?? "",
                                                maximumAmount: userDefaults?.string(forKey: "Maximum_Amount") ?? "",
                                                languageCode: userDefaults?.string(forKey: "Language_Code") ?? "",
                                                apiURL: userDefaults?.string(forKey: "Url") ?? "",
                                                bankUserName: userDefaults?.string(forKey: "Bank_User_Name") ?? "",
                                                bankBranchCode: userDefaults?.string(forKey: "Bank_Branch_Code") ?? "",
                                                bankAccountNumber: userDefaults?.string(forKey: "Bank_Account_No") ?? "",
                                                bankAccountType: userDefaults?.string(forKey: "Bank_Account_Type") ?? "",
                                                receiversPhoneRequired: userDefaults?.string(forKey: "PhoneNo_Security_Required") ?? "",
                                                receiverPhoneNumberLength: userDefaults?.string(forKey: "Phone_Number_Length") ?? "",
                                                selfOTPRequired: userDefaults?.string(forKey: "OTP_Security_Required") ?? "",
                                                selfPINRequired: userDefaults?.string(forKey: "PIN_Security_Required") ?? "",
                                                selfPINValidationAt: userDefaults?.string(forKey: "PIN_Validate_At") ?? "",
                                                SelfPINString: userDefaults?.string(forKey: "Customer_Security_PIN") ?? "",
                                                PINLength: userDefaults?.string(forKey: "PIN_Length") ?? "",
                                                receiversEmailRequired: userDefaults?.string(forKey: "Email_Security_Required") ?? "",
                                                receiversFaceRequired: userDefaults?.string(forKey: "Face_Security_Required") ?? "",
                                                UIConfigDictionary: UI_Dictionary)
        }
    }

```
    <ul>
    <li><b>Important</b> : In above code <ul>
    <li>Make changes in the `App Group String` as created in <b>Step 8.</b></li>
    <li>Make changes in the `UserDefault` value according to your convenience.</li>
    </ul>
    </li>
    <li>Build and run the project.</li>
    </ul>
    
### Initialization of SDK with Sample Values.

    <ul>
    <li>If you want to send values from HOST App to keyboard Extension : In this case Set values in Host app (e.g As shown in Image below) stored it using UserDefaults under App group suit name & access this values in Keyboard Extension as mentioned in above Section.</b></li>
    <li>Sample Parameter values</li>
    </ul>

    <div style="text-align:center; width:50%" >
    <div class="row";>
      <div class="column">
        <img src="../images/iOS/Figure12.png" style="max-width:520px"></br>
        <i>Figure 12: With Login ID & Password</i>
      </div>
      <div class="column">
        <img src="../images/iOS/Figure13.png" style="max-width:520px"></br>
        <i>Figure 13: With Bank Details</i>
      </div>
      </div>
    </div>

    <ul>
    <li>If you don’t want to send values from the HOST App to Keyboard Extension : In this case in Keyboard Extension you can directly send values right after the parameter name as shown in below code.</li>
    </ul>

```swift

import UIKit
import KeyboardSDK
 
class KeyboardViewController: KeyboardParentViewController {
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        initKeyboardSDK(enableMyMo: "Y",
                        showSendMoney: "Y",
                        showSendToATM: "Y",
                        showHistory: "Y",
                        applicationCode: "CUX",
                        senderName: "TestUser1",
                        loginID: "atl_mymo",
                        Password: "Merchant#",
                        MerchantID: "14196",
                        PhoneNumber: "74636363",
                        CustomerCode: "47390",
                        CountryCode: "United States",
                        CurrencyCode: "USD",
                        CurrencySymbol: "$",
                        minimumAmount: "1",
                        maximumAmount: "2000",
                        languageCode: "en_ES",
                        apiURL: "https://demo.idmission.com/IDS/service/ids/",
                        bankUserName: "John",
                        bankBranchCode: "Bank Of ATL",
                        bankAccountNumber: "2635476623",
                        bankAccountType: "Default",
                        receiversPhoneRequired: "Y",
                        receiverPhoneNumberLength: "8",
                        selfOTPRequired: "N",
                        selfPINRequired: "N",
                        selfPINValidationAt: "BANK",
                        SelfPINString: "",
                        PINLength: "4",
                        receiversEmailRequired: "N",
                        receiversFaceRequired: "N")
    }
}

```
# SDK integration in Android Project 

## Integration of AAR

The following steps are given to integrate MyMo SDK in an Android project:
<br/>

<strong>Step 1 :</strong> Navigate to Android Studio > Files > New Module > select Import .Jar/.AAR Package> Next, as shown on Figure 1 and Figure 2 :

    <div style="text-align:center; width:50%" >
    <img src="../images/Android/Figure1.png" style="max-width:520px"/><br/>
    <i>Figure 1: Selecting a New Module</i>
    </div>
    <br/>
    <br/>
    <div style="text-align:center; width:50%" >
    <img src="../images/Android/Figure2.png" style="max-width:520px"/><br/>
    <i>Figure 2: Selecting a Module Type</i>
    </div>
    <br/>
    <br/>

<strong>Step 2 :</strong> Locate mymo.aar file from the local storage, as shown on Figure 3.

    <div style="text-align:center; width:50%" >
    <img src="../images/Android/Figure3.png" style="max-width:520px"/><br/>
    <i>Figure 3: Locating mymo.aar from device storage</i>
    </div>
    <br/>
    <br/>

<strong>Step 3 :</strong> Enter the name for module/SDK library(eg `mymoLibrary`), as shown on Figure 4  and Click finish:

    <div style="text-align:center; width:50%" >
    <img src="../images/Android/Figure4.png" style="max-width:520px"/><br/>
    <i>Figure 4: Finishing import with a library name</i>
    </div>
    <br/>
    <br/>

<strong>Step 4 :</strong> Confirm that the MyMo library/module has been added, as shown on Figure 5:

    <div style="text-align:center; width:50%" >
    <img src="../images/Android/Figure5.png" style="max-width:520px"/><br/>
    <i>Figure 5: Project structure after adding new sdk library</i>
    </div>


## Initialization of SDK
### Enable MyMo Call
```java
final MyMoSettings myMoSettings = MyMoSettings.getInstance(cordova.getActivity().getApplicationContext());

myMoSettings.enableMyMo();
myMoSettings.setPhoneNumber(phoneNumber);
myMoSettings.setCustomerCode(customerCode);
myMoSettings.setCountryCode(countryCode);
myMoSettings.setCurrencyCode(currencyCode);
myMoSettings.setCurrencySymbol(currencySymbol);
myMoSettings.setIntegLoginId(integLoginId);
myMoSettings.setIntegPassword(integPassword);
myMoSettings.setIntegMerchantId(integMerchantId);
myMoSettings.setMinimumAmount(minAmount);
myMoSettings.setMaximumAmount(maxAmount);
myMoSettings.setLanguage(language);
myMoSettings.setPostURL(postURL);

// Transaction OTP security
myMoSettings.setTxnSecurityOTP(isTransactionOTPSecurityRequired);

// Transaction PIN security
myMoSettings.setTxnSecurityPIN(isTransactionPINSecurityRequired);
myMoSettings.setPinValidateAtIDM(validatePINAt);
myMoSettings.setCustomerSecurityPIN(customerSecurityPin);
myMoSettings.setPinLength(customerPinLength);

// Receiver phone configuration
myMoSettings.setTxnSecurityReceiverPhoneNo(isReceivePhoneSecurityRequired);
myMoSettings.setPhoneNumberLength(receiverPhoneNumberLength);

// Bank Username 
myMoSettings.setBankSenderName(bankUserName);
myMoSettings.setBranchCode(branchCode);
myMoSettings.setBankAccountNo(bankAccountNumber);
myMoSettings.setBankAccountType(bankAccountType);


// UI icons
Bitmap mymoIconbitmap = convertBase64StringToBitMap(mymoIconImg);
myMoSettings.setMyMoBitmapDrawable(mymoIconbitmap );

Bitmap arrowIconBitMap = convertBase64StringToBitMap(arrowIcon);
myMoSettings.setDownArrowBitmapDrawable(arrowIconBitMap );

Bitmap txnSuccessIconBitMap = convertBase64StringToBitMap(txnSuccessIcon);
myMoSettings.setTxnSuccessIconBitmapDrawable(txnSuccessIconBitMap );

Bitmap alertIconBitMap = convertBase64StringToBitMap(alertIcon);
myMoSettings.setAlertIconBitmapDrawable(alertIconBitMap );

Bitmap contactIconBitMap = convertBase64StringToBitMap(contactIcon);
myMoSettings.setContactIconBitmapDrawable(contactIconBitMap);

Bitmap processingIconBitMap = convertBase64StringToBitMap(processingIcon);
myMoSettings.setProcessingIconBitmapDrawable(processingIconBitMap);

// UI Color 
myMoSettings.setTextColor(textColor.trim());
myMoSettings.setEditboxBackgroundColor(editBoxBackClr.trim());
myMoSettings.setHistoryListHeaderColor(histHeaderBackClr);
myMoSettings.setSuccessMsgTextColor(txnSuccessTxtClr);
myMoSettings.setAlertMsgTextColor(alertTxtClr);
myMoSettings.setSendMoneyAmtTextColor(txnSuccessAmountTxtClr);
myMoSettings.setCalenderAndDateColor(calandarBtnTxtClr);
myMoSettings.setLoadMoreTextColor(loadMoreBtnTxtClr);

myMoSettings.setConfirmTxnYesButtonColor(confirmTxnYesBtnClr);
myMoSettings.setConfirmTxnNoButtonColor(confirmTxnNoBtnClr);

myMoSettings.setCancelTxnCloseButtonColor(closeBtnClr);
myMoSettings.setCancelTxnConfirmButtonColor(confirmCancelTxnBtnClr);

myMoSettings.setConfirmCancelTxnYesButtonColor(confirmCancelYesBtnClr);
myMoSettings.setConfirmCancelTxnNoButtonColor(confirmCancelNoBtnClr);

// Header and pay button text color
myMoSettings.setHeaderBtnTextColor(headerPayTxtClr.trim());

// Header and pay button background color
myMoSettings.setHeaderButtonBackgroundColor(headerPayBackClr.trim());

// UI Strings/Label changes
myMoSettings.setSendMoneyLabel(sendMoneyLbl.trim());
myMoSettings.setSendToAtmLabel(atmLbl.trim());
myMoSettings.setHistoryLabel(historyLbl.trim());
myMoSettings.setPayLabel(payLbl.trim());
myMoSettings.setSuccessMsgTextLabel(TransactionSuccessLbl);

// Configurable error/success and validation messages:
myMoSettings.setTextOFErrorCode016(textOfErrorCode016.trim());
myMoSettings.setTextOFErrorCode224(textOfErrorCode224.trim());
myMoSettings.setTextOFErrorCode236(textOfErrorCode236.trim());
myMoSettings.setTextOFErrorCode358(textOfErrorCode358.trim());
myMoSettings.setTextOFErrorCode370(textOfErrorCode370.trim());
myMoSettings.setTextOFErrorCode428(textOfErrorCode428.trim());
myMoSettings.setTextOFErrorCode501(textOfErrorCode501.trim());
myMoSettings.setTextOFErrorCode604(textOfErrorCode604.trim());
myMoSettings.setTextOFErrorCode888(textOfErrorCode888.trim());
myMoSettings.setTextOFErrorCode999(textOfErrorCode999.trim());
myMoSettings.setTextOFErrorCode1003(textOfErrorCode1003.trim());
myMoSettings.setTextOFErrorCode2054(textOfErrorCode2054.trim());
myMoSettings.setTextOFErrorCode2071(textOfErrorCode2071.trim());
myMoSettings.setTextOFErrorCode2077(textOfErrorCode2077.trim());
myMoSettings.setTextOFErrorCode2080(textOfErrorCode2080.trim());
myMoSettings.setTextOFErrorCode501(textOfErrorCode2082.trim());
myMoSettings.setTextOFErrorCode2084(textOfErrorCode2084.trim());
myMoSettings.setTextOFErrorCode2086(textOfErrorCode2086.trim());
myMoSettings.setTextOFErrorCode2087(textOfErrorCode2087.trim());
myMoSettings.setTextOFErrorCode2589(textOfErrorCode2589.trim());
myMoSettings.setTextOFErrorCode5000(textOfErrorCode5000.trim());
myMoSettings.setTextOFErrorCode5010(textOfErrorCode5010.trim());
myMoSettings.setTextOFErrorCode3059(textOfErrorCode3059.trim());

myMoSettings.setTextOfValidation001(textOfValidation001.trim());
myMoSettings.setTextOfValidation002(textOfValidation002.trim());
myMoSettings.setTextOfValidation003(textOfValidation003.trim());
myMoSettings.setTextOfValidation004(textOfValidation004.trim());
myMoSettings.setTextOfValidation005(textOfValidation005.trim());
myMoSettings.setTextOfValidation006(textOfValidation006.trim());
myMoSettings.setTextOfValidation007(textOfValidation007.trim());
myMoSettings.setTextOfValidation008(textOfValidation008.trim());
myMoSettings.setTextOfValidation009(textOfValidation009.trim());
myMoSettings.setTextOfValidation011(textOfValidation011.trim());

// Hide Show Header Buttons on keyboard
myMoSettings.setShowSendMoneyEnabled("Y");
myMoSettings.setShowSendToATMEnabled("Y");
myMoSettings.setShowHistoryEnabled("Y");
```
### Disable MyMo Call
```java
final MyMoSettings myMoSettings = MyMoSettings.getInstance(cordova.getActivity().getApplicationContext());
myMoSettings.disableMyMo();
```
## Examples with Screenshot
<div style="text-align:center; width:50%" >
<img src="../images/Android/Figure6.png" style="max-width:520px"/><br/>
<i>Image 1: Initialising SDK parameter with sample values.</i>
</div>
<br/>
<br/>

<div style="text-align:center; width:50%" >
<img src="../images/Android/Figure7.png" style="max-width:520px"/><br/>
<i>Image 2: Initialising SDK parameter with sample values (with branch code)</i>
</div>
<br/>
<br/>


<div style="text-align:center; width:50%" >
<div class="row";>
  <div class="column">
    <img src="../images/Android/Figure8.png" alt="Snow" style="max-width:520px">
  </div>
  <div class="column">
    <img src="../images/Android/Figure9.png" alt="Forest" style="max-width:520px">
  </div>
  </div>
  <i>Image 3: Initialising SDK parameter with sample values (with security options.)</i>
</div>


# KeyboardSDK Enable/Disable State

## IOS functionality 
        <ul>
        <li>In keyboard extension, Keyboard’s enabled or disabled state can be find out using isKeyboardEnabled() method</li>
        <li>User can use above method in following way</li>
        </ul>
        
```swift
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
