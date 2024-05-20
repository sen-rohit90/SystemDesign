
This include notes for the below chapters
### 4.8 Know how to customize and use email templates

-   Whitepaper: Email Template Usage and Customization:  [https://community.sailpoint.com/t5/Technical-White-Papers/Email-Template](https://community.sailpoint.com/t5/Technical-White-Papers/Email-Template-Usage-and-Customization/ta-p/78164)[Usage-and-Customization/ta-p/78164](https://community.sailpoint.com/t5/Technical-White-Papers/Email-Template-Usage-and-Customization/ta-p/78164)
-   Whitepaper: Email Template Arguments:  [https://community.sailpoint.com/t5/Technical-White-Papers/Email-Template-](https://community.sailpoint.com/t5/Technical-White-Papers/Email-Template-Arguments/ta-p/73115)[Arguments/ta-p/73115](https://community.sailpoint.com/t5/Technical-White-Papers/Email-Template-Arguments/ta-p/73115)
-   Whitepaper: Best Practices: Email Configuration:  [https://community.sailpoint.com/t5/Technical-White-Papers/Best-Practices-Email-](https://community.sailpoint.com/t5/Technical-White-Papers/Best-Practices-Email-Configuration/ta-p/75930)[Configuration/ta-p/75930](https://community.sailpoint.com/t5/Technical-White-Papers/Best-Practices-Email-Configuration/ta-p/75930)

## Email Templates & Customizations

The default email templates ship with the product and can be found in the [IdentityIQ Installation Directory]/WEB-INF/config directory in the files: emailtemplates.xml and lcmemailtemplates.xml.
There is a third file called emailtemplatesSample.xml
Email templates are stored as XML objects and can be viewed or modified through the IdentityIQ Debug pages.

To import a template through the user interface, click the **gear** menu **> Global Settings**  **> Import from File**. Click **Browse** to select the email template’s XML file from the file system and click Import.

You can use the console’s import command to import the file.
Import files may contain one or more EmailTemplate objects. However, if a file contains more than one object, the import methods expect the set of objects to be wrapped in a <sailpoint> </sailpoint>  block, as shown here.

    <?xml version='1.0' encoding='UTF-8'?>  
    <!DOCTYPE sailpoint PUBLIC "sailpoint.dtd" "sailpoint.dtd">  
    <sailpoint>  
    <EmailTemplate name="Template 1">  
    ...  
    </EmailTemplate>  
    <EmailTemplate name="Template 2">  
    ...  
    </EmailTemplate>  
    </sailpoint>


**Lifecycle Manager Emails**

Lifecycle Manager uses process variables and step arguments for selecting which email templates to use with various lifecycle events. These are set up within workflow definitions (**Setup > Business Processes**) either as a process variable, step argument, or work item configuration email notification template.

In this workflow, Identity Correlation, the Notify User step is used to send an email.

![LCMIdentityCorrelationEmail1.png](https://community.sailpoint.com/legacyfs/online/sailpoint/100231_LCMIdentityCorrelationEmail1.png)

Looking at the individual step (Notify User), we see that the step action is a call to the sendEmail workflow library method.

![LCMIdentityCorrelationEmail2.png](https://community.sailpoint.com/legacyfs/online/sailpoint/100232_LCMIdentityCorrelationEmail2.png)

The template argument to that step specifies which email template to use. If you wanted to use a different default template, you would specify a different template in this part of the workflow. The default email template can also sometimes be overridden with an argument passed to the workflow.

![LCMIdentityCorrelationEmail3.png](https://community.sailpoint.com/legacyfs/online/sailpoint/100233_LCMIdentityCorrelationEmail3.png)


***Email Template XML***

    <?xml version='1.0' encoding='UTF-8'?>  
	<!DOCTYPE EmailTemplate PUBLIC "sailpoint.dtd" "sailpoint.dtd">  
	<EmailTemplate created="1450215706777" id="40288e8151a797210151a7979099013b" name="Delegation Revocation">  
	  <Body>$requesterName has revoked the following work item from you: $workItemName.  This work item will no longer appear in your queue.  
	    </Body>  
	  <Description>  
	      Email Template for notifying work item owners that their delegation  
	      work item has been revoked.  
	    </Description>  
	  <Signature>  
	    <Inputs>  
	      <Argument name="workItemName" type="string">  
	        <Description>The description property of the delegation WorkItem.</Description>  
	      </Argument>  
	      <Argument name="certification" type="Certification">  
	        <Description>The Certification object containing the delegated item.</Description>  
	      </Argument>  
	      <Argument name="requesterName" type="string">  
	        <Description>The display name of the Identity that requested the delegation.</Description>  
	      </Argument>  
	    </Inputs>  
	  </Signature>  
	  <Subject>Work item revoked: $workItemName</Subject>  
	</EmailTemplate>

|Nested Element| Purpose  |
|--|--|
|Subject  | Subject line for the email message	 |
|Body	| 	  Body, or main content, of the email message	 |
|Signature |Hashmap of arguments to the email template. The signature for each template cannot be changed through the XML. Arguments to each template vary based on the associated system activity to which they apply. Properties and methods belonging to any object passed as an argument are available to include in the message, but other objects that are not part of the template’s signature cannot be retrieved to use in the email message.	|
|Inputs | Nested element within Signature, signifying the input arguments to the template	|
|Arguments | Nested element within Signature and Inputs; this element names and specifies the type of each input argument to the template|
|Description|Indicates descriptive information for the reader of the XML; describes the element in which it is nested (e.g. <Description> within <Argument> describes the argument’s usage; <Description> within the <EmailTemplate> describes the purpose and usage of the template itself) |
|From|Sender email address; if this is not specified in the template, the default sender specified on the **gear** > **Global Settings** (or in versions 6.4 and prior, **System Setup**) **> IdentityIQ Configuration** window’s Default From Address is used. |




**EmailTemplate Arguments**


**name** - Short but descriptive name for template; uniquely identifies email template

**cc, bcc** - Carbon Copy and Blind Carbon Copy recipients for the email

**NOTE**: The **to** attribute is not specified in the email template because it is determined programmatically as the email is sent and would be overridden.


## Apache Velocity Engine

IdentityIQ email templates are processed through an open-source engine called  [Velocity](http://velocity.apache.org/). Velocity is a Java-based template engine that allows web page designers to reference methods defined in Java code. IdentityIQ’s email templates make use of the Velocity Template Language to dynamically specify the email messages’ contents and generate custom email messages specific to the recipient, work item, and action involved.

|Reference Type|  Examples| Additional Information	
|--|--|--|
| Variables | $identityName,  ${identityName}, $!identityName | These three syntaxes are generally interchangeable in VTL. Shorthand notation (the first example) is the most commonly used, but each of the other two is required in special cases. The {} syntax allows concatenation with other text and the ! syntax suppresses printing when the variable is null.
| | $customer.Address| Returns the value corresponding to the _Address_ key in a _customer_ hash table
||$identity.DisplayName|  Invokes the getDisplayName() method on the identity object.NOTE: Property notation resolves to the getter method corresponding to the property name, not to an instance variable itself. Nested objects’ properties can also be retrieved through this notation. Example: $item.Certification.Name invokes the getName() method on the Certification object retrieved through the getCertification() method on the item object
|| $ identity.getBundles($ application), $ identity.hasRole($ role,‘true’) | Used for all non-getter methods and for any methods that require arguments


## Directives (Commands)

These are the key commands of the Velocity Template Language that are most frequently used in IdentityIQ email templates to dynamically determine the text that is printed in each email message.
|Command / Directive|	Usage  | Example
|--|--|--|
| #If… #elseif… #else… #end | Conditional evaluation | #if($requester) requested by $requester.displayableName. #{end}|
|#foreach… #end	|Loop through a list of objects	|      #foreach ($attrReq in $acctReq.attributeRequests) ... #end
|#set	|	Establish the value of a reference |	#set ($identityName = “John.Smith”), #set ($book.Title = “War and Peace”)



## SPTools Function Library

Immediately before any template is submitted for evaluation by the Velocity engine, the spTools argument is added to the VelocityContext so the template can access its methods. SpTools is a function library that contains a few localization utility methods to help with message formatting -- primarily date formatting. The methods available within spTools are listed in the table below:
|Method| Description  |
|--|--|
| String formatDate(Object date) |   Formats the passed-in date object to a string representation using the IIQ default date and time styles (both the java.util.dateformat SHORT formats), formatted per the norms of the server’s default locale and timezone |
| String formatDate(Object date, Integer dateStyle, Integer timeStyle) | Formats the passed-in date object to a string representation using the specified date and time styles, formatted per the norms of the server’s default locale and timezone. NOTE: The styles are represented by constant values: SHORT = 3, MEDIUM = 2, LONG = 1, FULL = 0 ; dateStyle and timeStyle correspond to java.text.DateFormat constants; see the Sun Javadocs for details
| String formatDate(Object date, String formatString) | Formats the date according to the specified formatString (uses the java.text.SimpleDateFormat method) |
|String getMessage(String key) | Returns an internationalized message from the message catalog corresponding to the provided key |
|String escapeHtml( String string) |   Converts HTML special characters to their entity equivalents ; Example: escapeHtml('<div class="article">This is an article</div>') .............Returns: &lt;div class="article"&gt;This is an article&lt;/div&gt;

## Sending an Email from a Rule

Some installations may require notifications to be sent based on events that are not covered by the automated system notifications. Rules can often be used to drive these notifications. The example below shows how to send an email from a rule.

    <?xml version='1.0' encoding='UTF-8'?>  
	<!DOCTYPE sailpoint PUBLIC "sailpoint.dtd" "sailpoint.dtd">  
	<sailpoint>  
	<Rule language="beanshell" name="Test Email Sending" type="BuildMap">  
	  <Description>Debugging Tool - Sends a sample email out via the email server.</Description>  
	   <Signature returnType="Map">  
	    <Inputs>  
	     <Argument name="log">  
	      <Description>  
	      The log object associated with the SailPointContext.  
	      </Description>  
	     </Argument>  
	     <Argument name="context">  
	      <Description>  
	        A sailpoint.api.SailPointContext object that can be used to query the database if necessary.  
	      </Description>  
	     </Argument>  
	    </Inputs>  
	   </Signature>  
	<Source>  
	// Library inclusions for BeanShell  
	import sailpoint.api.*;  
	import sailpoint.object.*;  
	import sailpoint.tools.*;  
	import java.util.*;  
	import java.lang.*;  
	import java.text.*;  
	// Point this to the “To” email address  
	String emailDest = "adam.hampton@example.com";  
	// Specify the email template name in tplName  
	String tplName = "SailPoint - Test Email Sending";  
	EmailTemplate template = context.getObjectByName(EmailTemplate.class, tplName);  
	if (null == template) {  
	   log.error("ERROR: could not find email template [ " + tplName + "]");  
	   return;  
	}  
	Map args = new HashMap();  
	// Add all args needed by the template like this  
	args.put("testField1", "This is a test of template parameters.");  
	EmailOptions ops = new EmailOptions(emailDest, args);  
	context.sendEmailNotification(template, ops);  
	return;  
	</Source>  
	</Rule>  
	</sailpoint>


## Redirect to Email

The Redirect to Email option actually sends the email messages through the designated SMTP server, but routes them all to a specified email address instead of delivering them to the email address recorded for the target identity. The named email box can then be examined to verify that all emails were sent and appear as expected. This can be particularly helpful when trying to validate email messages with HTML content. This setting is most commonly used in the User Acceptance Testing (UAT) environment.

To use this option, the SMTP server must be set up and the IdentityIQ server must be able to communicate with it (locally or over the network). To select this mail setting:

1.  Choose  **Email Notification Type: Redirect to Email.**
2.  Specify the email address to which all emails should be sent as the Redirection Email Address.
3.  Choose an  **Encryption**  type, if desired.
4.  Specify the  **Default SMTP Host**  and  **Default SMTP Port**  for sending emails.  
    NOTE: Make sure there are no trailing space characters in the  **Default SMTP Host**  name. This can occur when the value for this field is copied and pasted from a Word document or email, and a trailing space is automatically copied with the string; it results in email sending failure because the JVM fails to resolve the host name.
5.  Provide the  **Username**  and  **Password**  IdentityIQ will use to authenticate to the SMTP server, if required by the server. (You will also need to confirm the password.)

![EmailRedirectToEmail.png](https://community.sailpoint.com/legacyfs/online/sailpoint/102271_EmailRedirectToEmail.png)

## SMTP

The SMTP option sends emails to the intended recipients through the named SMTP server. The settings for it are identical to the Redirect to Email option except that a Redirection Email Address is not specified. This option is almost always chosen for the production environment.

To select this mail setting:

1. Choose  **Email Notification Type: SMTP**.

2. Choose an  **Encryption**  type, if desired.

3. Specify the  **Default SMTP Host**  and  **Default SMTP Port**  for sending emails.

NOTE: Make sure there are no trailing space characters in the Default SMTP Host name. This can occur when the value for this field is copied and pasted from a Word document or email, and a trailing space is automatically copied with the string; it results in email sending failure because the JVM fails to resolve the host name.

4. Provide the  **Username**  and  **Password IdentityIQ**  must use to authenticate to the SMTP server, if required by the server. (You will also need to confirm the password.)

![EmailSMTP.png](https://community.sailpoint.com/legacyfs/online/sailpoint/102273_EmailSMTP.png)

# Configuring Email Settings through XML

Instead of setting the email configuration through the UI in each environment (such as build, test, and production), some customers find it more efficient to include the email settings they want to use in the XML files that are included in the environment build process. Most of the email settings are recorded in the  **SystemConfiguration Configuration**  object.

Configuration objects can use the  _merge import_  option, through which customizations can be merged from a separate XML file into the standard object. Using the merge import option is typically more efficient than modifying the  **SystemConfiguration Configuration**  object, because it lets you manage and promote email settings across environments independently, without the risk of affecting any other customizations or settings in the general System Configuration.

**NOTE**: The **Maximum Email Retries** value is saved in a **RequestDefinition** object named **Email Request,** as the attribute **retryMax**.

## Redirect to File

Import this XML to modify the  **SystemConfiguration**  to redirect all emails to a file. (Substitute installation-specific values in the map entries.)

	<?xml version="1.0" encoding="UTF-8"?>  
	<!DOCTYPE sailpoint PUBLIC "sailpoint.dtd" "sailpoint.dtd">  
	<sailpoint>  
	    <ImportAction name='merge'>  
	        <Configuration name='SystemConfiguration'>  
	            <Attributes>  
	                <Map>  
	                    <entry key="emailNotifierType" value="redirectToFile"/>  
	                    <entry key="redirectingEmailNotifierFilename" value="/home/spadmin/iiqmbox.txt"/>  
	                    <entry key="defaultEmailFromAddress" value="admin@example.com"/>  
	                    <entry key="suppressDuplicateEmails">  
	                        <value>  
	                            <Boolean>true</Boolean>  
	                        </value>  
	                    </entry>  
	                </Map>  
	            </Attributes>  
	        </Configuration>  
	    </ImportAction>  
	</sailpoint>

## Redirect to Email

Import this XML to modify the SystemConfiguration to redirect all emails to a single email address. (Substitute installation-specific values in the map entries.)

<?xml version="1.0" encoding="UTF-8"?>  
<!DOCTYPE sailpoint PUBLIC "sailpoint.dtd" "sailpoint.dtd">  
	<sailpoint>  
	    <ImportAction name='merge'>  
	        <Configuration name='SystemConfiguration'>  
	            <Attributes>  
	                <Map>  
	                    <entry key="emailNotifierType" value="redirectToEmail"/>  
	                    <entry key="redirectingEmailNotifierAddress" value="test_email_address@example.com"/>  
	                    <entry key="defaultEmailFromAddress" value="admin@example.com"/>  
	                    <entry key="defaultEmailHost" value="mail.example.com"/>  
	                    <entry key="defaultEmailPort" value="25"/>  
	                    <entry key="smtp_username" value="mailuser"/>  
	                    <entry key="smtp_password" value="P@ssw0rd"/>  
	                    <entry key="suppressDuplicateEmails">  
	                        <value>  
	                            <Boolean>true</Boolean>  
	                        </value>  
	                    </entry>  
	                </Map>  
	            </Attributes>  
	        </Configuration>  
	    </ImportAction>  
	</sailpoint>

## SMTP

Import this XML to modify the SystemConfiguration to send all emails to their intended target recipients through the specified SMTP server. (Substitute installation-specific values in the map entries.)

<?xml version="1.0" encoding="UTF-8"?>  
<!DOCTYPE sailpoint PUBLIC "sailpoint.dtd" "sailpoint.dtd">  
	<sailpoint>  
	    <ImportAction name='merge'>  
	        <Configuration name='SystemConfiguration'>  
	            <Attributes>  
	                <Map>  
	                    <entry key="emailNotifierType" value="SMTP"/>  
	                    <entry key="defaultEmailFromAddress" value="admin@example.com"/>  
	                    <entry key="defaultEmailHost" value="mail.example.com"/>  
	                    <entry key="defaultEmailPort" value="25"/>  
	                    <entry key="smtp_username" value="mailuser"/>  
	                    <entry key="smtp_password" value="P@ssw0rd"/>  
	                    <entry key="suppressDuplicateEmails">  
	                        <value>  
	                            <Boolean>true</Boolean>  
	                        </value>  
	                    </entry>  
	                </Map>  
	            </Attributes>  
	        </Configuration>  
	    </ImportAction>  
	</sailpoint>

# Helpful Email Testing Resources

These two resources can be helpful with various email testing and debugging tasks:

-   Request List page
-   ClearEmailQueue command

## Request List

When emails are generated from IdentityIQ operations, they are created as Request objects and added to a queue which is managed by the request handler service. Request objects encapsulate the required information and the process (i.e. an executor class) for fulfilling a task, which allows the tasks to be queued and processed in the background. In general, emails are processed and sent immediately by the request handler, but there is also a retry capability for these items if they fail.

If the sending of an email notification fails with an SMTP error, it is left in the Request queue for retry. Requests, both pending and complete, can be viewed through a hidden IdentityIQ UI page at URL:  [IdentityIQ Base URL]/monitor/requests/requests.jsf.

Check this page to identify problems if the expected email messages are not generated.

![RequestListEmails.PNG](https://community.sailpoint.com/legacyfs/online/sailpoint/102277_RequestListEmails.PNG)

NOTE: By default, the first retry for a failed email request occurs one hour after the initial send attempt. Subsequent retries are scheduled using a basic decay algorithm that doubles the delay between attempts after each failed retry (e.g. 2 hours, then 4 hours, then 8 hours, etc.). If the requestDefinition for email requests specifies a retryInterval (recorded in number of seconds), that value will be used as the delay time for the first retry and subsequent retries will be scheduled by doubling that value (e.g. if the retryInterval is 300, the first retry will occur after 5 minutes and subsequent retries will occur after 10 minutes, then 20, etc.).

By default, successful emails are deleted from the request list immediately when they are sent, so you will not see successfully sent emails in your request list. If you wanted to retain successfully processed requests in the list, you can alter the Email Request RequestDefinition object by adding a resultExpiration attribute and setting it to the number of days to retain them.

![](https://community.sailpoint.com/legacyfs/online/sailpoint/197314_pastedImage_2.png)

## ClearEmailQueue Command


The clearEmailQueue command selectively deletes only unsent emails from the request queue, leaving other types of requests in the queue. This command requires no arguments. It deletes all pending emails, whether never sent or failed due to a sending error. Enter the command at the iiq console prompt.

> clearEmailQueue
# Other Email Configuration Options

These additional entries can optionally be added to the  **SystemConfiguration**  object to control the timing and handling of email sending. These options are not commonly used and are only available through XML, not through UI fields. They can be included in the same merge import XML files described in the Configuring Email Settings through XML section above.
| **SystemConfiguration Entry**  | **Functionality**  |
|--|--|
| < entry key=”defaultEmailGap” value=”0”/>| Minimum gap in milliseconds between emails (should be set to zero if the send-immediately flag below is specified) |
| < entry key=”defaultEmailGap” value=”0” /> |  Specifies that emails should be sent immediately instead of backgrounded on the request queue (should not be set to true while non-zero email gap is specified); this is rarely used since it means that the notifications cannot be retried if a failure occurs|
| < entry key=”emailNotifierClass” value=”sailpoint.example.CustomNotifierClass”/>| Allow designation of a custom email notifier class that overrides the standard 3 options; if set, this overrides any value specified in emailNotifierType.


## Custom EmailNotifier Class

Customers can implement other forms of email notification with a custom EmailNotifier class. This class must implement the EmailNotifier interface, which is documented in the IdentityIQ Javadocs.

For example, a custom email notifier could be used to implement custom notification options such as mobile push notification, WebSphere MQ, etc. The shell of this class is shown below for illustration; the specific logic (represented by the doNotifications method called by sendEmailNotification here) would have to be custom written. Since the sendEmailNotification method is passed a SailPointContext, the custom notifier could perform lookups in the IdentityIQ database to retrieve any information stored on the Identity (or any other object) required for its processing.

	package sailpoint.example;  
	import sailpoint.api.EmailNotifier;  
	import sailpoint.api.SailPointContext;  
	import sailpoint.server.SMTPEmailNotifier;  
	import sailpoint.object.Configuration;  
	import sailpoint.object.EmailOptions;  
	import sailpoint.object.EmailTemplate;  
	public class ExampleNotificationSender implements EmailNotifier {  
	    public void sendEmailNotification( SailPointContext context, EmailTemplate template, EmailOptions options )  
	        throws GeneralException, EmailException {  
	        // Send notifications (fictional method)...  
	        doNotifications( template.getTo(), template );  
	    }  
	}

A custom EmailNotifier class could also be used to implement multilingual support for emails. A custom EmailNotifier class could determine the appropriate language for the recipient (e.g. based on an Identity extended attribute) and change the template to a language-specific template accordingly. It could then hand the message to the SMTPEmailNotifier to finish sending. (Note that this is one of several options for implementing multilingual email support and may not be the easiest.)

`
          
        // Use SailPointContext to look up an extended identity attribute that  
        // specifies locale  
        String lang_suffix = null;  
        EmailTemplate newTemplate = template;  
        Filter myFilter = Filter.eq("email", template.getTo());  
  
        QueryOptions qo = new QueryOptions();  
        qo.addFilter(myFilter);  
          
        List IdentList = context.getObjects(Identity.class, qo);  
        if (null != IdentList) {  
            // should be only one because email is unique  
            for (Identity toIdent : IdentList) {  
                lang_suffix = toIdent.getAttribute("language");  
            }  
        }  
      
        // Pick the new email template based on that locale  
        // could use a cross-reference map in a Custom object or name the templates  
        // so a language-specific suffix separates them (-EN, -FR, etc.)  
        // (this example illustrates the suffix option)  
          
        if (lang_suffix != null) {  
          
            String templ_name = template.getName() + "-" + lang_suffix;  
            EmailTemplate templ = context.getObject(EmailTemplate.class,templ_name);  
            // Compile the newly picked template  
            newTemplate = templ.compile(context, context.getConfiguration(), options);  
        }  
  
        // hand off the email notification to the SMTPEmailNotifier once  
        // the correct language-specific template has been chosen  
        SMTPEmailNotifier smtp = new SMTPEmailNotifier();  
        smtp.sendEmailNotification(context, newTemplate, options);  
          
    }  
	}
