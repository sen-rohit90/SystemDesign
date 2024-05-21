

## Enterprise Localization of IdentityIQ

IdentityIQ can be configured to display text labels, tooltip help text, and object descriptions in different languages for different users based on their browser language preferences. This is commonly referred to as “localization”.

## About Message Files

IdentityIQ manages localization of the user interface based on the end user’s browser language settings. Text labels and tooltip help text in the IdentityIQ application are controlled by  _message keys_, which map to entries in language-specific  _message files_  to display text according to each user’s browser settings.

## About Object Descriptions

IdentityIQ supports creation of object descriptions in multiple languages, displaying the appropriate description to users based on their browser language settings and simple system configuration options.

## SailPoint-Provided Message Files

The standard message key files provided by SailPoint with any IdentityIQ installation are located in the identityiq.jar file within the  _[IdentityIQ installation directory]/WEB-INF/lib_  directory. Within that jar file, they are located in the  _/sailpoint/web/messages_  directory.

![](https://community.sailpoint.com/legacyfs/online/sailpoint/278900_pastedImage_2.png)

Figure 1: Messages and Help Files in identityiq.jar File

**iiqMessages_xx.properties** file which controls the text labels in the UI and an **iiqHelp_xx.properties** file which controls the tooltip help text

Users whose browsers specify languages that are not supported by SailPoint-supplied message files are always shown the text values from the generic (non-language-specific) **iiqMessages.properties** and **iiqHelp.properties** files; out of the box, these files are copies of the English-language versions, so the default language is English.

**NOTE**: **None of these files should be edited inside the identityiq.jar file since this jar file is replaced with every upgrade**. However, they can be used as references or as templates for creating custom entries or custom versions as described in  _Creating Custom Message Files_  and  _Customizing Specific Message File Entries_ sections below.

## Creating Custom Message Files

Customers may want to add additional languages or country-specific test sets by creating their own additional message and help files. They can do so by copying an  **iiqMessages_xx.properties**  and an  **iiqHelp_xx.properties**  file out of the identityiq.jar file into the [_IdentityIQ installation directory]/WEB-INF/classes/sailpoint/web/messages_  directory, renaming it according to their desired language or locale, and editing the entries.

For example, to create a British English version, copy the iiqMessages.properties (or iiqMessages_en.properties) file, rename it iiqMessages_en_GB.properties, and edit the entries to reflect British English spellings for words; do the same for the iiqHelp.properties (or iiqHelp_en.properties) file. The tags are case-sensitive, so ensure your formatting matches the language tag (i.e. if your language tag is en_GB, then iiqMessages_en_GB.properties will match, but iiqMessages_EN_gb.properties will not match).

To create a version for a non-supported language such as Danish, copy any of the provided iiqMessages_xx.properties and iiqHelp_xx.properties files, rename them iiqMessages_da.properties and iiqHelp_da.properties and translate all of the phrases from the chosen language into Danish.

**NOTE:**  Be sure to create your messages file with correctly written properties. For some languages, you may need to  **convert non-ASCII characters to hexadecimal encoding**.

In some cases, new entries must be added to the  **faces-config.xml**  file to support additional language files, as explained in  _Adding Supported Languages_  below.

The **faces-config.xml** file (found in _[IdentityIQ Installation Directory]/WEB-INF_) specifies a list of supported locales. IdentityIQ consults this list to determine which message files to acknowledge and use, so customers who are adding new language files or country-specific language files may need to make additions to this list to tell IdentityIQ to use their additional message key files.

## Customizing Specific Message File Entries

Customers may sometimes want to override specific entries in the iiqMessages.properties files (or language-specific versions) or may want to add their own custom message keys to support localization of installation-specific UI components. These alterations should be managed through the  **iiqCustom.properties**  file (and  **iiqCustom_xx.properties**  and  **iiqCustom_xx_yy.properties**  files) in their  _IdentityIQ installation directory]/WEB-INF/classes/sailpoint/web/messages_ directory.

## Message Key Files Order of Application

The various iiqMessages, iiqHelp, and iiqCustom properties files are used in a specific order. If the user’s browser language preference has been selected as xx_yy, IdentityIQ will look for message key entries in these files (if they exist) in this order and will display the UI text for the first match it finds:

1.  iiqCustom_xx_yy.properties
2.  iiqCustom_xx.properties
3.  iiqCustom.properties
4.  iiqMessage_xx_yy.properties and iiqHelp_xx_yy.properties
5.  iiqMessages_xx.properties and iiqHelp_xx.properties override files in WEB-INF/classes/sailpoint/web/messages directory
6.  iiqMessages_xx.properties and iiqHelp_xx.properties in identityiq.jar file
7.  iiqMessages.properties and iiqHelp.properties override files in WEB-INF/classes/sailpoint/web/messages directory
8.  iiqMessages.properties and iiqHelp.properties in identityiq.jar file
## An Example of Customization

Let's look at an example where a company has offices in France and Belgium, and wants to customize some of the translated French messages for the employees in France, and provide a slightly different customization for French-speaking employees in Belgium.

In this example, we'll customize the Welcome message on the login screen to change it from generic "Bienvenue" to "Bienvenue à Acme" for employees in France, and "Bienvenue à Acme Belgique" for French-speaking employees in Belgium.

1.  Make a copy of the  **iiqCustom.properties**  file, and name it  **iiqCustom_fr.properties**. (This file is located in the  _[IdentityIQ installation directory]/WEB-INF/classes/sailpoint/web/messages_  directory and is just an empty placeholder file, out of the box).
2.  Extract the French-language message file (**iiqMessages_fr.properties**) from the  **identityiq.jar.**
3.  Open  **iiqMessages_fr.properties**  and find the message key for the Welcome screen:  
      
    ![Bienvenue.png](https://community.sailpoint.com/legacyfs/online/sailpoint/93850_Bienvenue.png)
4.  Copy this message key, then open the  **iiqCustom_fr.properties**  file you created in step 1, and paste the message key into it.
5.  In  **iiqCustom_fr.properties**, edit the Welcome message to say "Bienvenue \u00E0 Acme" (\u00E0 is the unicode character for the letter a with an acute accent: à); save the file.  
      
    ![BienvenueFrance.PNG](https://community.sailpoint.com/legacyfs/online/sailpoint/93851_BienvenueFrance.PNG)
6.  Next, create a separate custom properties file for the Belgians: make a copy of  **iiqCustom_fr.properties**  and name it  **iiqCustom_fr_BE.properties**.
7.  Edit the Welcome message in the Canadian (**iiqCustom_fr_BE.properties**) file to say "Bienvenue \u00E0 Acme Belgique"; save the file.  
      
    ![](https://community.sailpoint.com/legacyfs/online/sailpoint/278906_pastedImage_6.png)
8.  Because  **fr_BE**  is not a SailPoint-supported locale (although  **fr**  without the region specifier is), you must edit the  **faces-config.xml**  file to add  **fr_BE**  as a supported locale:
    1.  Open the  **faces-config.xml**  file (found in  _[IdentityIQ Installation Directory]/WEB-INF_)
    2.  In the  < locale-config>  section, add this line:  
        <supported-locale>fr_BE</supported-locale>
    3.  Save  **faces-config.xml**
9.  **IMPORTANT**: Restart your application server.

Now, users with their browser set to  **fr_BE**  will see this message at login:

![](https://community.sailpoint.com/legacyfs/online/sailpoint/278907_pastedImage_7.png)

Users with their browser set to fr_FR  **or any other French-language locale**, such as Cameroon, or Morocco, will see the default French-language Welcome message:

![](https://community.sailpoint.com/legacyfs/online/sailpoint/212335_pastedImage_0.png)

(Users with fr_CA will see the messages from the SailPoint-provided fr_CA file).

Remember that customizations which specify both language and region (**iiqCustom_xx_yy.properties**) are used before customizations that specify only the language (**iiqCustom_xx.properties**), but the  **iiqCustom_xx_yy.properties**  will only be used if it exactly matches the user's language setting in the browser. This is why, in our example, users with a browser set to other French-language locales will see the default  **fr**  version of the Welcome message, and only users with browsers set to  **fr_BE**  will see the Belgian French Welcome.
# Configuring IdentityIQ for Localized Object Descriptions
To enable localized descriptions for additional languages, click the  **gear**  icon and select  **Global Settings**  (or in versions 6.4 and earlier,  **System Setup) >** **IdentityIQ Configuration**  ->  **Miscellaneous**. Add the desired languages to the  **Supported Languages**  field and click  **Save**.

![L10Nsettings.png](https://community.sailpoint.com/legacyfs/online/sailpoint/93855_L10Nsettings.png)

**NOTE**: If this  **Default Language**  is out of sync with the language of the text in the default iiqMessages.properties file, users with browsers specifying unsupported languages will see the UI labels in one language and the object description in a different one.

![](https://community.sailpoint.com/legacyfs/online/sailpoint/93858_pastedImage_1.png)


