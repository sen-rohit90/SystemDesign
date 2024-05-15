# 4. IdentityIQ Development 


This includes notes for the below and partially cover few of the topics: 

**4.1 Understand the purpose and use of rule libraries**

-   Rules and Scripts in IdentityIQ: [https://documentation.sailpoint.com/identityiq/help/systemadmin/rulesandscripts.html](https://documentation.sailpoint.com/identityiq/help/systemadmin/rulesandscripts.html#_gl=1*1etlqnm*_gcl_au*MzQ4MTM0MDA4LjE3MTU2MTA2OTM.)
### 4.2 Understand and leverage rule input/output arguments

-   Whitepaper: Rules in IdentityIQ 7.0 - 7.2:  [https://community.sailpoint.com/t5/Technical-White-Papers/Rules-in-IdentityIQ-7-](https://community.sailpoint.com/t5/Technical-White-Papers/Rules-in-IdentityIQ-7-0-7-2/ta-p/78176)[0-7-2/ta-p/78176](https://community.sailpoint.com/t5/Technical-White-Papers/Rules-in-IdentityIQ-7-0-7-2/ta-p/78176)
### 4.7 Know the common SailPoint API objects and methods, and how to leverage them

-   IdentityIQ SCIM API:  [https://developer.sailpoint.com/iiq/api](https://developer.sailpoint.com/iiq/api)
-   IdentityIQ Object Model and Usage:  [https://community.sailpoint.com/t5/Technical-](https://community.sailpoint.com/t5/Technical-White-Papers/IdentityIQ-Object-Model-and-Usage/ta-p/75090)[White-Papers/IdentityIQ-Object-Model-and-Usage/ta-p/75090](https://community.sailpoint.com/t5/Technical-White-Papers/IdentityIQ-Object-Model-and-Usage/ta-p/75090)
-   Beanshell Developer’s Guide:  [https://community.sailpoint.com/t5/Technical-White](https://community.sailpoint.com/t5/Technical-White-Papers/BeanShell-Developer-s-Guide-for-IdentityIQ/ta-p/74365)[Papers/BeanShell-Developer-s-Guide-for-IdentityIQ/ta-p/74365](https://community.sailpoint.com/t5/Technical-White-Papers/BeanShell-Developer-s-Guide-for-IdentityIQ/ta-p/74365)  IdentityIQ Wiki: Locking a SailPoint Object:
-   [https://community.sailpoint.com/t5/IdentityIQ-Wiki/Locking-a-SailPoint-Object/ta](https://community.sailpoint.com/t5/IdentityIQ-Wiki/Locking-a-SailPoint-Object/ta-p/79680)[p/79680](https://community.sailpoint.com/t5/IdentityIQ-Wiki/Locking-a-SailPoint-Object/ta-p/79680)
### 5.5 Understand common application rule types

-   Whitepaper: Rules in IdentityIQ:  [https://community.sailpoint.com/t5/Technical-](https://community.sailpoint.com/t5/Technical-White-Papers/Rules-in-IdentityIQ-7-0-7-2/ta-p/78176)[White-Papers/Rules-in-IdentityIQ-7-0-7-2/ta-p/78176](https://community.sailpoint.com/t5/Technical-White-Papers/Rules-in-IdentityIQ-7-0-7-2/ta-p/78176)

### 5.6 Understand common connector rule types

-   Whitepaper: Rules in IdentityIQ 7.0 - 7.2:  [https://community.sailpoint.com/t5/Technical-White-Papers/Rules-in-IdentityIQ-7-](https://community.sailpoint.com/t5/Technical-White-Papers/Rules-in-IdentityIQ-7-0-7-2/ta-p/78176)[0-7-2/ta-p/78176](https://community.sailpoint.com/t5/Technical-White-Papers/Rules-in-IdentityIQ-7-0-7-2/ta-p/78176)
### 6.1 Configure and leverage log4j

-   Log4j Support Guide:  [https://community.sailpoint.com/t5/Working-With-Support-](https://community.sailpoint.com/t5/Working-With-Support-Knowledge/Log4j-Support-Guide/ta-p/137421)[Knowledge/Log4j-Support-Guide/ta-p/137421](https://community.sailpoint.com/t5/Working-With-Support-Knowledge/Log4j-Support-Guide/ta-p/137421)

### 3.2 Understand the purpose of common certification rules

-   Whitepaper: Rules in IdentityIQ 7.0 - 7.2:  [https://community.sailpoint.com/t5/Technical-White-Papers/Rules-in-IdentityIQ-7-](https://community.sailpoint.com/t5/Technical-White-Papers/Rules-in-IdentityIQ-7-0-7-2/ta-p/78176)[0-7-2/ta-p/78176](https://community.sailpoint.com/t5/Technical-White-Papers/Rules-in-IdentityIQ-7-0-7-2/ta-p/78176)

### 7.5 Know the common IdentityIQ data objects and what they represent

-   IdentityIQ Object Model and Usage:  [https://community.sailpoint.com/t5/Technical](https://community.sailpoint.com/t5/Technical-White-Papers/IdentityIQ-Object-Model-and-Usage/ta-p/75090)[White-Papers/IdentityIQ-Object-Model-and-Usage/ta-p/75090](https://community.sailpoint.com/t5/Technical-White-Papers/IdentityIQ-Object-Model-and-Usage/ta-p/75090)

### 7.6 Understand the relationship between common data object models

-   Whitepaper: Object Model:  [https://community.sailpoint.com/t5/Technical-White-](https://community.sailpoint.com/t5/Technical-White-Papers/IdentityIQ-Object-Model-and-Usage/ta-p/75090)[Papers/IdentityIQ-Object-Model-and-Usage/ta-p/75090](https://community.sailpoint.com/t5/Technical-White-Papers/IdentityIQ-Object-Model-and-Usage/ta-p/75090)
# Notes

Let's look at some of the definitions and use cases: 

## What are Rules and Scripts?

Small segments of programmatic code which control or influence system behavior, allowing you to customize certain operations to meet your business needs. Rules and scripts are used throughout IdentityIQ to:
    

-   Define values in forms and provisioning policies
    
-   Define logic in workflow steps
    
-   Control the behavior or contents of certifications
    
-   Perform calculations or data manipulations in aggregation tasks
    
-   Manage or manipulate provisioning requests

## Scripts? 

Lines of code that are embedded within objects to perform logic only within the scope of a single usage

## Rules? 

Lines of code that are independent objects which can be referenced and re-used by multiple processes.

## What are the capabilities required?

One would either need System Administrator capability or the EditScripts  SPRight (8.3 onwards) to edit inline scripts. 
The **EditScripts** SPRight is not included in any standard capabilities by default. If you want to give script editing abilities to users other than System Administrators, you must either create a new capability for these users that includes the **EditScripts** SPRight, or add the **EditScripts** SPRight to an existing capability that can be assigned to those users.

Note that
![Rule and Scripts ](https://github.com/sen-rohit90/SystemDesign/blob/main/Rules&Scripts.JPG)

## What language is used?

BeanShell is the language used for rules and scripts. It is an interpreted language that uses Java-like syntax. (Lightweight scripting for Java) BeanShell provides several conveniences for the script-writing process, like loose typing of variables and the implicit import of key java classes. BeanShell dynamically executes standard Java syntax and extends it with common scripting conveniences such as loose types, commands, and method closures like those in Perl and JavaScript.

## What is context argument?
The context argument is a SailPointContext object, the entry point into the SailPoint API – giving you methods for accessing other objects and interacting with the SailPoint database.

## What is log argument?
The log argument is a Logger object, which lets you use Log4j, the same logging utility used by the IdentityIQ core product, to generate logging messages from your rules.

## What are Rule returns?
Rules often also return values which are used by the process that invoked them. Most of the time, rules require a certain type of value to be returned – that is, the IdentityIQ system is expecting a specific type of return value when a rule of that type is called. For example, a rule defining a policy violation owner is expected to return an identity object.

## How Are Rules Created? 
### 1. Using Rule UI Editor
- To edit an existing rule, first select the rule, then click the [...] button to open the Rule Editor.

- To create a new rule, click the [...] button without selecting an existing rule, and a blank Rule Editor window is opened where you can create a new rule.
	#### 	Rule Editor Fields
	The Rule Editor uses these fields to define the rule and its business logic:

	- Copy From Existing Rule

		If you want to reuse existing code in your new rule, select an existing rule to copy.

	- Rule Name

		Enter a unique name for the new rule, that clearly describes the purpose. It is useful to include the type of rule in the name, such as "Customization – My App," or "Exclusion – Inactive Users."

	- Description

		Enter text that describes the purpose of the rule and what it does.

	- Arguments and Returns

		These sections list the input variables (Arguments) that can be used in the script, and the return information (Returns). Click on any of the arguments or returns to show more detailed information. These fields cannot be changed in the Rule Editor.

	- Rule Type

		The rule type determines the purpose of the rule and where it can appear in dropdown lists in the IdentityIQ UI. In most cases, the Rule Editor does not allow you to change the Rule Type.

	- Rule Editor

		In the main editor of this UI, enter the BeanShell code for the rule. The rule cannot be saved until some code is entered. Note that no validation is performed; even if the rule is syntactically incorrect, it is accepted and saved. Incorrect rules may result in tasks, workflows or certifications failing to execute, and in errors and large stack traces in the log files.

### 2. Rule XML import
Rules can be written externally, through an IDE or text editor, and imported into the IdentityIQ instance. Standalone XML objects and imported into IdentityIQ through the **gear > Global Settings > Import from File** option, or through the IdentityIQ console, using the iiq console **import** command. A single rule XML file can contain one or more rules. The logic for the rule is written in BeanShell, but it must also be wrapped in an XML document

XML Structure: 

    <?xml version='1.0' encoding='UTF-8'?>  
    <!DOCTYPE Rule PUBLIC "sailpoint.dtd" "sailpoint.dtd">
    
	    <Rule>
    
	    </Rule>
    
    
   ## Printing the beanshell namespace
   If you’re unsure about what variables are available to your rule or script, you can use the snippet of BeanShell shown below to figure it out. This logic prints the name and value of each variable in the BeanShell namespace – in other words, all the variables known to BeanShell at that point in time.
   

    System.out.println("Beanshell namespace:");

    for (int i = 0 ; i &lt; this.variables.length ; i++) {
       String name = this.variables[i];
       if ("transient".equals(name)) { continue; } 
       Object value = eval(name);
       if (value == void)
           print(name + " = void");
       else if (value == null)
           print(name + " = null");
       else
           print(name + ": " + value.getClass().getSimpleName() + " = " + value);
    }

so, you iterate over this.variables and use eval() over each item. You can print this object xml. 

## What are Rule Libraries?
Many rule objects are just a single block of code, executed together as a unit. But IdentityIQ also allows you to create rule objects that contain multiple separate functions or methods. These are called rule libraries.

Rule libraries are a way you can manage collections of methods that can be accessed from within other rules. These can help promote code re-use.

If you find yourself continually writing the same segment of code over and over again, consider including that logic in a rule library, so you can access it from other rules. If you ever need to change it, you can change it in one place and have it changed everywhere automatically. As a best practice for artifact management, you should group related methods together in a rule library, creating as many rule libraries as you need for different logical groupings.

 

    <Rule name='Active Directory Utility'>
	   <Source>
	      public List getAppLinks(String appName, String nativeId) { // do stuff }
	      public String getAttributeOnLink(Link link) { // do stuff and return a String } 
	   </Source>
	</Rule>

To use this method in a rule, you need to include a reference to the Rule Library in the XML of that rule with a <ReferencedRules> element, then in the body of the rule itself, you can call the getAppLinks method or the  getAttributeOnLink and the system will find it in the rule library and execute its code.

    <Rule…>
	   <ReferencedRules>
	       <Reference class='Rule' name='Active Directory Utilit'/>
	   </ReferencedRules>
	   <Source>
	       getAppLinks(appName, String nativeId);
	       getAttributeOnLink(link);
	   </Source>
	</Rule>
IdentityIQ includes some rule libraries that are used by the **default** workflows. Examples of rule libraries are **Workflow Library, Approval Library, and LCM Workflow Library**	

## How are Rules executed?

### Debug 
- available on debug.jsf page. Note that println or logger statements are written to log file and not printed or displayed on output screen. Only returned output is displayed. Can only pass log and context. Doesn't have any option to pass any other argument. If rules need other values, one will need to hardcode that in the body of the rule. 
### IIQ Console 
- Runs as a command line interface. Loggers and print statements are displayed on the CLI window. You could provide additional attributes as arguments in an xml attributes map file rather than hardcoding them
 ### Rule runner task  
- There’s also a built-in task that allows you to set up stand-alone rules to run on a schedule. To do this, you:

	1.  Create a task from the Run Rule task type
	2.  Specify what rule it should run
	3.  Provide arguments to the rule if needed.

- The value returned from a rule is reported in the task results as its result status. This task type can 	speed up the process of implementing custom scheduled actions.




## Sample Example Rules (OOTB Collection)

Available here - 
[SystemDesign/examplerules.xml at main · sen-rohit90/SystemDesign (github.com)](https://github.com/sen-rohit90/SystemDesign/blob/main/examplerules.xml)[Example Rules xml](https://github.com/sen-rohit90/SystemDesign/blob/main/examplerules.xml)
	

## Where are API References available?
All API references are available <identityiq_home>\doc\javadoc\
## Quiz
#### Which of the following arguments are automatically provided to all rules and scripts? Choose all that apply.

-   config
    
    Correctly unchecked
    
-   context
    
    Correctly checked
    
-   application
    
    Correctly unchecked
    
-   currentUser
    
    Correctly unchecked
    
-   log
    
    Correctly checked
    
-   status
    
    Correctly unchecked
    

SUBMIT

  

Correct

#### How can you add a BeanShell rule to IdentityIQ?

Choose all that apply.

-   Compile and deploy it into a rule library
    
    Correctly unchecked
    
-   Wrap the BeanShell logic in a Rule XML object and import it
    
    Correctly checked
    
-   Type the BeanShell logic into the IdentityIQ Console
    
    Correctly unchecked
    
-   Enter and save the BeanShell logic through a Rule Editor UI page
    
    Correctly checked
    

SUBMIT

  

Correct



# API Introduction 

## What is Hibernate?
Object to Relational database mapping tool, to perform the translation between database records and the application's object model 

## XML serializaton
IIQ uses XML for serialization of its object to an exportable and human readable format. Used for debugging purposes. migrate object definitions from one evn to another, export and import, etc. 

## How to manipulate data of IIQ?
Those operations should be completed through the object model – using the API to retrieve the objects you need, and accessing their methods to read and modify data as appropriate.

You should never interact with IdentityIQ’s database directly – only through the object model, and by extension through Hibernate.

Just like you’d find in other object-oriented applications, IdentityIQ’s objects include get and set methods for accessing and modifying object properties.

[Modifying IIQ Data](https://github.com/sen-rohit90/SystemDesign/blob/main/IIQEngineerCertification/img/Hibernate.JPG)
![Modifying IIQ Data](https://github.com/sen-rohit90/SystemDesign/blob/main/IIQEngineerCertification/img/Hibernate.JPG)

## Extending Objects
Many of the objects in the IdentityIQ object model, inherit from a parent object called SailPointObject, including all top-level objects in the persistent store – that is, any object you can see in the Debug Pages Object Browser or can retrieve in the IdentityIQ Console.
Through SailPointObject’s support for extended attributes, any of those objects can record additional information specific to your business. They can be extended using placeholders or named attributes. By default, these attributes are stored in the database in a CLOB, a Character Large Object.

IdentityIQ supports creation of up to **20 placeholder attributes**, which are stored in database columns called _extended1, extended2_, _extended3_, and so on.

IdentityIQ also supports the creation of an **unlimited number of named extended attribute columns**.
## What is toXml method?
Helps to see the objects you’re working with in an easily consumable representation. All SailPointObject objects include a toXml method that writes that representation to a log file, so you can study and analyze its contents and structure.

example of plan xml

    <?xml version='1.0' encoding='UTF-8'?>

	<!DOCTYPE ProvisioningPlan PUBLIC "sailpoint.dtd" "sailpoint.dtd">

	<ProvisioningPlan nativeIdentity="Crystal.Schmidt" targetIntegration="LDAP" trackingId="ee6bb4a0471749a398b34202663a2737">

		<AccountRequest application="LDAP" nativeIdentity="cn=Crystal.Schmidt,ou=people,dc=training,dc=sailpoint,dc=com" op="Modify">

			<AttributeRequest name="groups" op="Add">

			<Value>

				<List>

					<String>cn=Users,ou=groups,dc=training,dc=sailpoint,dc=com</String>

					<String>cn=Employees,ou=groups,dc=training,dc=sailpoint,dc=com</String>

				</List>

			</Value>

			</AttributeRequest>

		</AccountRequest>

	<Attributes>

	<Map>

		<entry key="source" value="IdentityRefresh"/>

	</Map>

	</Attributes>

	</ProvisioningPlan>

## Some Important API and its uses
![Packages](https://github.com/sen-rohit90/SystemDesign/blob/main/IIQEngineerCertification/img/Important%20Packages.JPG)

**The SailPoint API package** is the entry point for many key processes, containing the SailPoint Context – the important feature from a rule-writing perspective.

**The connector package** contains many of our built in connectors, like the Delimited File and JDBC connectors. It also contains the abstract class you extend when creating custom connectors.

**The SailPoint Object** package is one you'll likely use frequently. This is where you’ll find the documentation for how to access the core data objects.

The **task package** is where you’ll find the abstract task executor that you’ll need to extend if you're going to be creating custom tasks.

Finally, the SailPoint tools package contains a **Utils** class which houses many utility methods that are useful in data manipulation in rules. There are methods that convert CSV lists to string lists or vice versa and others are useful date formatting methods, methods for deleting white space, and much more.

#### IMPORTANT - Read Object Model and Usage Whitepaper
### Quiz
**When you need to access data stored in IdentityIQ’s database in your rule and script extensions, you will write SQL statements to query the tables that hold the data.**

True

Correctly unselected

False

Correctly selected

SUBMIT

**Which of these methods is helpful for viewing the full contents of any SailPointObject and is often used in the development for debugging purposes?**

getAllAttributes()

Correctly unselected

toXml()

Correctly selected

viewObject()


## SailPointContext ?
The **SailPointContext** object is a critical component for working with IdentityIQ’s API in BeanShell rules and scripts. It is effectively the entry point to the API – the class that lets you retrieve and work with other objects.

The SailPointContext is passed as an argument in the variable called “context” to every rule or script hook-point in IdentityIQ. You'll always have a context at your disposal when writing BeanShell.

Key functions of the SailPointContext center around **searching objects, accessing system data, and controlling database transactions** and management tasks.

### Objects Retrieval
	### Search & Retrieve
	## Using GetObjects
	
	//not recommended
	//Get all objects
	List apps = context.getObjects(Application.class)

	//get filtered objects as per qo 
	List identities = context.getObjects(Identity.class, qo)

	## using search
	## gives ability to retrieve whole objects or selective attributes
	Iterator apps = context.search(Application.class, qo)

	## Get selective attributes
	Iterator users = context.search(Identity.class, qo, "name,status");
	Iterator users = context.search(Identity.class, qo, listOfProps);

### Single Object Retrieval
	 Identity id = context.getObjectByName (Identity.class, “Bob.Smith”);
	 or
	 Application app = context.getObjectById (Application.class, "ff80808161b51a2a0161b51a434a0002”);
	 
### Single Object Retrieval & Projection Query
The projection query finds all the objects that match the search criteria – in the example below, identities – but only returns a value that uniquely identifies the matching objects in the initial query, like its name or ID. Then you iterate over that set retrieving each object into memory one at a time, as you need it.

	List props = new ArrayList();
	props.add("name");
	Iterator users = context.search (Identity.class, qo, props);
	if (null != users) {
	     while (users.hasNext()) {
	       String name = users.next()[0];
	       Identity id = context.getObjectByName(Identity.class, name);
	     }
	}

### Counting objects
	int countObjects (class, QueryOptions)

	int count = context.countObjects (Identity.class, qo);
	if (count == 1)
	…
	else if (count > 1)
	{
	Iterator users = context.search (Identity.class, qo, "name");
	…
	}

### Filter examples in Query Options

**Filter.eq(”department”,”Accounting)** - Department equals Accounting  
**Filter.gt(“age”,21)** - Age greater than 21  
**Filter.like(“firstName”,”Ar”,MatchMode.START)** - First name starts with Ar  
**Filter.containsAll(“costCenter”,costCenterCodes);** - For multi-valued attributes, search for one or more matches with selectors like “Cost Center contains all of a set of cost center codes"  

**Filter.isnull(“region”)** 
**Filter.notnull(“region”)** - Boolean filters require just an attribute and operator, like isnull or notnull

### Some Combined Filter Examples
There are several ways to combine filters. You can use the operators  **and** and  **or** on the Filter class to combine filters. This can be straightforward or nested to multiple levels.

Examples: and / or filters

-   Filter f = Filter.and(Filter.eq("department", "Finance"), Filter.eq("manager.name", "Catherine.Simmons")

Returns identities who are in the Finance department who also have Catherine Simmons as a manager.

-   Filter f = Filter.or(Filter.eq("department", "Finance"), Filter.eq("manager.name", "Catherine.Simmons"))

Returns identities who are either in the Finance department or who have Catherine Simmons as a manager; only one of the criteria must be true.

-   Filter f = Filter.or(Filter.and(Filter.eq("department", "Finance"), Filter.eq("manager.name", "Catherine.Simmons")), Filter.eq("lastname", "Smith"));

The last example selects identities who are either (in the Finance department and report to Catherine Simmons) or (they have the last name Smith).

Plus, any separate filters that are added to the same QueryOptions will automatically be combined, treated as an add, not an or. In the QueryOptions filter below, both f1 and f2 would need to be met to match the filter:

qo.addFilter(f1);  
qo.addFilter(f2);

The course exercises include creating filters and the  _Filters and Filter Strings_  white paper on Compass include detailed options and examples.

### View System Data
To get the SystemConfiguration object, use the context’s getConfiguration method. From there, you can look up any variable in the system configuration by name – that is, any entry key in the system configuration attributes map – then use the value of that variable in your rule logic.

    Configuration sysConfig = context.getConfiguration();
    String serverRoot = sysConfig.get(“serverRootPath”);
    if (serverRoot != null)
    {
        String workItemPath = serverRoot + "/workitem/workItem.jsf?id=”
        …
    }

The SailPointContext also includes two different methods related to retrieving information about the logged-in user. The  **getUser** method returns the identity object for the user.

	Identity currUser = context.getUser();
	if (currUser != null) {
	    if (currUser.getAttribute(“department”).equals(“Accounting”)) {
	         log.debug(“User “ + currUser.getName() + “is in accounting department.”);
	    }
	}

Quiz
**Which of these SailPointContext methods supports a projection query, providing for better memory management efficiency?**

getObjects

Correctly unselected

getObjectById

Correctly unselected

search

Correctly selected

query

Correctly unselected

SUBMIT

  

Correct

**Which of these functions does QueryOptions provide in a search operation?**

Choose all that apply.

-   Filtering
    
    Correctly checked
    
-   Ordering
    
    Correctly checked
    
-   Result-set limits
    
    Correctly checked
    
-   Distinct searches
    
    Correctly checked
    

SUBMIT

  

Correct



## Object Model
**Identity object** has links. Links are created from Application object. Entitlements information is read from Application object. Entitlements can be created from Account and Group Aggregation.
![Identity Model](https://github.com/sen-rohit90/SystemDesign/blob/main/IIQEngineerCertification/img/Identy%20Object%20Model.png)

**Roles** object model. 
![Roles](https://github.com/sen-rohit90/SystemDesign/blob/main/IIQEngineerCertification/img/Role%20Object%20Model.png)

**Certification** object model
![Certification Object](https://github.com/sen-rohit90/SystemDesign/blob/main/IIQEngineerCertification/img/Certification%20Object%20Modelpng.png)

**Provisioning Object Model**
![Privsioning Object](https://github.com/sen-rohit90/SystemDesign/blob/main/IIQEngineerCertification/img/Provisioning%20Onject%20Models.png)


**Quiz**
**Which of these objects represents an entitlement in the Entitlement Catalog?**

Link

Correctly unselected

Bundle

Correctly unselected

ManagedAttribute

Correctly selected

CertificationItem

Correctly unselected

ProvisioningPlan

Correctly unselected

SUBMIT

  

Correct





## **Common Rules** 

**Aggregation Rules**

Aggregation rules involve manipulating data as it's read into IdentityIQ from the designated data source. There are two sets of rules that come into play in the aggregation process – one set that is common to all aggregations, and another set that is specific to each connector and vary from one application source type to another.

Flow ->
Connector reads accounts or groups and may manipulate the data as necessary. 
There could be lot of connector rules configured for data reading and other operations like filtering and merging. Post it, resource objects are created and sent for Aggregation rules. Rules like Customization Rule, Correlation Rule, Creation rule follow. Check the below images - 

![Aggregation Generic Rules Flow](https://github.com/sen-rohit90/SystemDesign/blob/main/IIQEngineerCertification/img/Aggregation%20Rules.png)

![LDAP Connector Flow](https://github.com/sen-rohit90/SystemDesign/blob/main/IIQEngineerCertification/img/LDAP.png)

![JDBC Connector Flow](https://github.com/sen-rohit90/SystemDesign/blob/main/IIQEngineerCertification/img/JDBC.png)

![Delimited Connector](https://github.com/sen-rohit90/SystemDesign/blob/main/IIQEngineerCertification/img/DelimitedFile.png)

**Certification Rules**
Some rules let you configure the content of access reviews during the campaign generation process:

-   **Certification Exclusion** rules allow you to filter out individual items or groups of items that meet the certification campaign’s defined criteria but that you still don’t want to include. For example, you might run a manager certification but only want to include employees, not contractors, so you could exclude all contractors and their associated entitlements.
-   **Certification Schedule Entity Selector** rules are almost the exact opposite of exclusion rules. They define the set of identities to include in the certification, so you target just the ones you want instead of collecting more than you need and filtering them out.

Even more rules are provided to allow you to manipulate the system’s behavior during a certification campaign:

-   **Pre-delegation rules** run during the campaign generation process to redirect parts or all of an access review to someone other than the person who would normally be assigned the items in the campaign. For example, your executive team might not do access reviews for their direct reports like a front-line manager would, so you could pre-delegate their items to their administrative assistants.
-   **Escalation rules** can redirect access reviews to a new owner if the certifier is not completing the work in a timely manner.
-   **Sign-off approver rules** are used to obtain a second level of approval of access review decisions before the system acts on them, requiring another person to sign-off on the reviewers' decisions.
-   **Phase enter/exit rules,** probably the most open-ended component of certification configurations, are executed as each certification phase starts or ends. For example, you may have a requirement to auto-revoke anything that wasn’t completed during the certification active period but to allow the access-holder to challenge the auto-revocation. You can put the auto-revoke logic into the challenge-period enter rule and let the built-in challenge-period functionality handle the rest.

** Workflow Rules **
While configuring workflows, hooks are available for rules at LifeCycle Manager request provisioning, Lifecycle events, setting up workflow variables,  define actions the workflow should perform, or calculate who should be assigned to complete a form or approval workitem. 

** Provisioning Policies Rules **
rules and scripts can be used to set attribute values in provisioning requests, through Provisioning Policy definitions.
In cases where your provisioning policy prompts a user for an attribute value instead of auto-calculating its value, you can write rules or scripts to display a fixed set of allowed values for the user to choose from. Or you can write validation logic that makes sure the value they provide fits within appropriate parameters. For example, you could validate that the office phone number a user enters is part of the corporate trunk of phone numbers.


**Quiz**

**A creation rule can be used with which process?**

Certification

Correctly unselected

Aggregation

Correctly selected

Escalation

Correctly unselected

SUBMIT

  

Correct

TAKE AGAIN

**An escalation rule can be used with which process?**

Aggregation

Correctly unselected

Exclusion

Correctly unselected

Certfication

Correctly selected

SUBMIT

  

Correct 


## **Beanshell Performance - Best Practices**
**Log Configuration**
- always use log4j (current version is log4j2) - available at <install dir>/WEB-INF/classes/log4j2.properties
![Sample log4j config](https://github.com/sen-rohit90/SystemDesign/blob/main/IIQEngineerCertification/img/log4jConfig.png)

This log variable is the passed to all rules in the application. So, if you set your Log4j properties to log at the debug level for one rule, it will log at the debug level for all rules when you use that log argument. A useful alternative, also a best practice, is to create custom loggers in your rules.

![Create Logger Object](https://github.com/sen-rohit90/SystemDesign/blob/main/IIQEngineerCertification/img/log4j_1.png)

  

First, create a logger object in the rule or script, specifying a name that reflects a standard naming convention for your installation and doesn’t conflict with the SailPoint namespace. This example uses "acme.rule.FinanceCorrelationRule" as a unique name.

![Specify Log Level](https://github.com/sen-rohit90/SystemDesign/blob/main/IIQEngineerCertification/img/log4j_2.png)

Next, in the Log4j properties file, use that same name to specify the log level for the rule. In Log4j2, this requires two lines in the properties file – one to specify the logger name and one to specify the log level. When not actively debugging the code, the logger can be set to error or warn.

  

![Include Trace](https://github.com/sen-rohit90/SystemDesign/blob/main/IIQEngineerCertification/img/log4j_3.png)

Optionally, when writing large or complex rules, you can proactively include trace statements every few lines. These trace statements won’t normally appear in your log file because your logger won’t usually be set that high, but when you need to track to isolate where problems are occurring in your rule, you can increase logging to that level and the logic is already in place to support troubleshooting.

### 

**Null and Void Checking**

In BeanShell, like in Java and many other languages, you need to guard against null values and null pointer exceptions.

Before you call a method on an object variable, you should make sure the variable is defined and set.

-   An unset variable is a  **null** variable.
-   An undefined variable is a  **void** variable.

Because BeanShell supports loose typing, variables don’t have to be declared, and BeanShell will let you use variables that aren’t yet defined, but this can lead to problems when a rule is executed.  
In the example below, manager is an Identity object.

    String mgrTitle = manager.getAttribute(“jobtitle”);

But, before using the getAttribute method on the manager variable you should check for both void and null conditions. In the example below, the script verifies that the targetIdentity is neither void nor null before it tries to retrieve that user’s manager with the getManager method.

    if ((targetIdentity != void) && targetIdentity != null))
    	Identity manager = targetIdentity.getManager();
    if (manager != null)
      	String mgrTitle = manager.getAttribute(“jobtitle”

	);

### 

**Locking Objects**

When your code will modify IdentityIQ objects, object locking is important for ensuring that multiple processes don’t try to update the same object at the same time. There are two types of locks used in IdentityIQ – persistent and transaction.

![Persistent vs Transactional](https://github.com/sen-rohit90/SystemDesign/blob/main/IIQEngineerCertification/img/Persistent%20vs%20Transaction%20Locks.JPG)

  

Object locking is supported by methods in the sailpoint.api.ObjectUtil class. There are several available signatures for those locking methods, which are covered in the Javadoc and in the BeanShell Developer’s Guide on Compass. You’ll see methods specifically around locking identities and certifications with persistent locks, such as:

-   lockIdentity
-   lockIdentityByName
-   lockIdentityById
-   lockCert
-   lockCertificationById

Identities are one of the most common targets of IdentityIQ operations and should always use a persistent lock.

There are also generic methods for getting persistent or transaction locks on other objects:

-   lockObject
-   transactionLock

  

### 

**Locking Objects - Identities**

Identity objects are often the target of operations in IdentityIQ. Locking is handled automatically in many key processes that commonly modify identities, including:

-   Account aggregations
-   Identity refresh tasks
-   Lifecycle manager workflows
-   Certification generation

When modifying identity objects outside these processes, you should be diligent about lock management.

### 

**Saving Objects**

Many rules expect you to change an object and return it, so IdentityIQ will save the object automatically. But you have great flexibility when writing rules and you might perform something beyond what was originally intended for the rule. If you’re accessing and modifying an object that the rule doesn’t expect you to change, the code that calls the rule may not perform the save automatically, so you’ll need to save that object yourself.

In the example below, the rule is setting a password in a place where IdentityIQ isn’t going to save the identity object automatically, so context.saveObject is used to save the user, and context.commitTransaction is used to commit it.

	// user is an Identity object	
	user.setPassword(newPassword);
	context.saveObject(user);
	context.commitTransaction();

This is only necessary in instances where IdentityIQ is not expecting the action you are performing and therefore isn’t set up to save the object you’re changing.

### 

**Processing Cursors**

When working with iterators, like the one you get with a projection query, you must not leave open cursors on the database connection. This situation occurs when code loops through a set of objects looking for a specific condition then breaks out of the loop partway through iterating the list.

There are two options to prevent this situation:

-   Ensure that you always process through the entire list, don’t break out of an iteration loop
-   Use the flushIterator method from the sailpoint.tools.Util class to clear the iterator when you are done with it

		QueryOptions qo = new QueryOptions();
		qo.addFilter(Filter.eq("application.name","Active_Directory");
		Iterator iter = context.search(Link.class, qo, "id");
		 
		while (iter.hasNext()){
		   Object[] row = (Object[]) iter.next();
		   String id = row[0];
		   // use id of the object to fetch it and process it 
		}

		Util.flushIterator(iter);

There is no harm in flushing an iterator even if it was already exhausted, so generally speaking, this is the safer approach.

### 

**Decache**

You should ensure your code properly handles cached objects. If you are working with a specific object and no longer need it, you can evict it from the in-RAM cache with a decache statement. The SailPoint Context’s decache method can be called with an object argument to clear just that object from memory.

	context.decache(object)

For example, if you need to re-retrieve an object and want to ensure that you have a fresh copy of it from the database, you can clear the old copy from the cache then re-fetch the object into your script variable.

When you want to clear all loaded objects from the cache, there’s a more open-ended decache method which takes no arguments.

	context.decache()

This decache method evicts and clears all the objects from the cache but does not close your database connection, so open database cursors are left intact.

As an example, you can use this method when iterating over large volumes of objects, such as every 100 objects, to clear the cache.

	Iterator iterator = context.search(objectClass, queryOptions, "id");
	if (iterator != null) {
	    while (iterator.hasNext()) {  
	        count++;
	        // Retrieve object and process
	        …
	        if (count%100==0)
	           context.decache();
	    }
	}

This is a recommended memory management practice. The above example runs a decache every 100 objects, freeing up all the memory that those objects have been occupying so it can be reused by this or another process. With potentially large objects like identity objects, this could amount to megabytes of memory being freed.

**Searching**
First, when performing queries in your custom code, use the projection query - search() with properties. This is significantly more efficient than getObjects.

  

In many cases, you only need an attribute or two anyway, so target your query to return just those attributes. Also, a projection query returns a **database cursor instead of loading the entire set of objects into memory**, making a difference in your system performance and heap space utilization.

  

Next, always try to filter your searches with a QueryOptions object that allows you to retrieve the minimum data you need. The less data your code has to process, the better. Let the query do as much of the work up front as possible.

**Iterative Rules**
The performance of your rules will, of course, impact the performance of your system. This is especially important in iterative rules – those that run multiple times within a single process.

  

Most rules that run in aggregation processes are iterative, and rules that are run by an Identity Refresh task will be run for every identity that task is examining. Examples include:

-   BuildMap, MergeMaps, Transformation, ResourceObjectCustomization, Correlation
-   Refresh, ManagerCorrelation

Rules that run during certification generation are also iterative. When IdentityIQ is determining who to exclude in an exclusion rule, it's going to examine every identity in the certification, which could be every identity in the system. A pre-delegation rule is also run for every certification item to determine whether to pre-delegate it and to whom.

  

Consider a buildmap rule that runs as part of an aggregation of 30,000 authoritative accounts.

-   Rule runs for every row in a 30,000 line file
-   Each row is processed in .02 seconds
-   .02 seconds * 30,000 rows = 600 seconds or 10 minutes

Even with sub-second performance, it can still have a performance impact. It adds up quickly when you consider the volume of data you may be working with. If that was 3,000,000 rows, or if the rule took 1 second each time it ran, it would be even more significant.

  

Look for opportunities to pull operations out of iterative rules. For example, if you need to retrieve data from an external database, don’t open a connection, perform a lookup, and close the connection in every rule run. Instead, perform the lookup once – outside of the iterative process – and store the data in a Custom Object in IdentityIQ’s database. In this way, your iterative rules can do a more efficient local data lookup.

  

Some rules even have state objects that can share values across related rules, so make use of those too.

**Meter Objects**
You can measure the performance of your rules to understand what is and isn’t working efficiently and to evaluate the effectiveness of any code changes made to improve performance.

  

The sailpoint.api.Meter class lets you collect statistics about execution timings for sections of code.

  

    import sailpoint.api.Meter;
    
    //Begin your code
    
    Meter.enterByName("MyMeter");
    
    //Do work
    
    Meter.exitByName("MyMeter");
    
    //End of code

  

You can import the class then call its enterByName method to mark the start of a process and its exitByName method to mark the end. The system will track statistics for the named meter:

-   A count of how many times it executes
-   The minimum, maximum and average run times

Include your whole rule under one meter name or have different parts of the rule tracked with different names.

  

You can also view the stats on the Call Timings page. To access the page, go to  **Debug Page - wrench icon - Call Timings**. You'll see the timings for some built-in IdentityIQ processes plus your custom meters.


**Quiz**

**Which of these is the best choice for logging in BeanShell rules, giving you the most granular control on when and where the system writes messages to your log files?**

Define a custom logger in your rule and configure its log level in the Log4j properties file

Correctly selected

Use the log variable that is passed to the rule automatically and control its log level in the Log4j properties file

Correctly unselected

Write System.out.println statements in your rule logic and turn them on and off through the system configuration

Correctly unselected

SUBMIT

  

Correct

TAKE AGAIN

It’s a good idea to call context.decache periodically to clear objects you are no longer using in your code. This method leaves any open database cursors intact, so it is safe to do inside the a loop you are using to process through an iterator from a search.

True

Correctly selected

False

Correctly unselected

SUBMIT

  

Correct

