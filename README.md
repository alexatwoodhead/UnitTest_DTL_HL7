# UnitTest_DTL_HL7
HL7 DTL TestCase Creator and Runner Framework

## How to use
The following will describe how to quickly get started with testing existing HL7 to HL7 Transforms.<br/>
Note the framework can also process:
- Object to HL7 Message
- Object to HL7 Segment
- HL7 message to HL7 Segment
- HL7 Segment to HL7 Message

### Step 1 - Import class "UnitTest.DTL.HL7TestCase" into target namespace

### Step 2 - Generate new TestCase(s)
This method analyses the namespace for matching DTL implemented classes.
For each DTL found, a new TestCase is created when one doesn't already exists. (Existing classes will not be overwritten).

Example:
```objectscript
Do ##class(UnitTest.DTL.HL7TestCase).GenerateTestCases("UnitTest.DTL.TestTrans.","UnitTest.Test.DTL.TestTrans.",0,,0,1,.pStatus)
```
Parameters:
* matchPackage - The facility will search for any transform classes that match this package path<br/>
* targetPackage - The base target page to generate new TestCase classes in<br/>
* copySubPackageNames - If enabled generate TestCase classes in sub packages as discovered from matched transforms<br/>
* addToProject - If specified. Attempt to automatically add classes to the named Studio Package.
* listOnly - If enabled only list the classes that would be generated
* pStatus - List of errors encountered. 

Example variations:
```objectscript
// List Only Test, match ending in dot
Do ##class(LabTechUK.UnitTest.DTLTestCaseBase).GenerateTestCases("MEXX.Radiology.dtl.","MEXX.Radiology.test.dtl",1,,1,1,.pStatus)
// List Only match not ending in dot
Do ##class(LabTechUK.UnitTest.DTLTestCaseBase).GenerateTestCases("MEXX.Radiology.dtl","MEXX.Radiology.test.dtl",1,,1,1,.pStatus)
// List Only, No copy sub packages, match ending in dot
Do ##class(LabTechUK.UnitTest.DTLTestCaseBase).GenerateTestCases("MEXX.Radiology.dtl.","MEXX.Radiology.test.dtl",0,,1,1,.pStatus)
// List Only, No copy sub packages, match not ending in dot
Do ##class(LabTechUK.UnitTest.DTLTestCaseBase).GenerateTestCases("MEXX.Radiology.dtl","MEXX.Radiology.test.dtl",0,,1,1,.pStatus)
// Actually generate TestCases
// match ending in dot, follow sub package name convention
Do ##class(LabTechUK.UnitTest.DTLTestCaseBase).GenerateTestCases("MEXX.Radiology.dtl.","MEXX.Radiology.test.dtl",1,,0,1,.pStatus)
```


### Step 3 - Optional Adjust Compare expressions
The source and target schemas have been extracted from the analyzed DTL<br/>
The generated compare method compares Expected with Actual HL7 values.<br/>
Some DTL expressions like Incrementing Counters and Current Date of tranfrom are volatile for each message.<br/>
> 
> This is the Unique Selling Point of this UnitTest approach!!<br/>
>
> To exclude unique transform differences simply
> comment out unwanted compare experessions as shown
> .

```objectscript
/// Class Generated on 2022-08-14 19:19:11 using TestCase Generator V
/// <!--
/// do ##class(UnitTest.Test.DTL.TestTrans.TransformSource2).Debug()
/// -->
Class UnitTest.Test.DTL.TestTrans.TransformSource2 Extends UnitTest.DTL.HL7TestCase [ ProcedureBlock ]
{

Parameter SourceSchema = "2.5:ADT_A01";

Parameter TargetSchema = "2.5:ADT_A01";

Parameter TransformClass = "UnitTest.DTL.TestTrans.TransformSource2";

Method Compare(expectedTarget As EnsLib.HL7.Message, actualTarget As EnsLib.HL7.Message, source As EnsLib.HL7.Message)
{
 // Add your path assertions here. For example: //
  do ..AssertPathEquals(expectedTarget,"MSH:SendingApplication.NamespaceID",actualTarget,"MSH:SendingApplication.NamespaceID")
  do ..AssertPathEquals(expectedTarget,"MSH:SendingApplication.UniversalID",actualTarget,"MSH:SendingApplication.UniversalID")
  do ..AssertPathEquals(expectedTarget,"MSH:SendingApplication.UniversalIDType",actualTarget,"MSH:SendingApplication.UniversalIDType")
  do ..AssertPathEquals(expectedTarget,"MSH:SendingFacility.NamespaceID",actualTarget,"MSH:SendingFacility.NamespaceID")
  //do ..AssertPathEquals(expectedTarget,"MSH:SendingFacility.UniversalID",actualTarget,"MSH:SendingFacility.UniversalID")
  do ..AssertPathEquals(expectedTarget,"MSH:SendingFacility.UniversalIDType",actualTarget,"MSH:SendingFacility.UniversalIDType")
  do ..AssertPathEquals(expectedTarget,"MSH:ReceivingApplication.NamespaceID",actualTarget,"MSH:ReceivingApplication.NamespaceID")
  do ..AssertPathEquals(expectedTarget,"MSH:ReceivingApplication.UniversalID",actualTarget,"MSH:ReceivingApplication.UniversalID")
  do ..AssertPathEquals(expectedTarget,"MSH:ReceivingApplication.UniversalIDType",actualTarget,"MSH:ReceivingApplication.UniversalIDType")
  do ..AssertPathEquals(expectedTarget,"MSH:ReceivingFacility.NamespaceID",actualTarget,"MSH:ReceivingFacility.NamespaceID")
  do ..AssertPathEquals(expectedTarget,"MSH:ReceivingFacility.UniversalID",actualTarget,"MSH:ReceivingFacility.UniversalID")
  do ..AssertPathEquals(expectedTarget,"MSH:ReceivingFacility.UniversalIDType",actualTarget,"MSH:ReceivingFacility.UniversalIDType")
  //do ..AssertPathEquals(expectedTarget,"MSH:DateTimeOfMessage.Time",actualTarget,"MSH:DateTimeOfMessage.Time")
  
  ...
}
  
XData TESTMessageSource
{
<test><![CDATA[
<!-- Your Source HL7 Message or Segment content goes here -->
]]></test>
}

XData TESTMessageTarget
{
<test><![CDATA[
<!-- Your Expected output for HL7 Message or Segment content goes here -->
]]></test>
}

}
```

### Step 4 - Add Some Messages
For a single Test DTL Source message and Target expected output message, simply replace the provided message template above with HL7 message content.
```objectscript
XData TESTMessageSource
{
<test><![CDATA[
MSH|^~\&|MSH:3.1^MSH:3.2^MSH:3.3|MSH:4.1^MSH:4.2^MSH:4.3|MSH:5.1^MSH:5.2^MSH:5.3|MSH:6.1^MSH:6.2^MSH:6.3|MSH:7.1^MSH:7.2|MSH:8|MSH:9.1^MSH:9.2^MSH:9.3|MSH:10|MSH:11.1^MSH:11.2|MSH:12.1^MSH:12.1&MSH:12.2&MSH:12.3&MSH:12.4&MSH:12.5&MSH:12.6^MSH:12.3.1&MSH:12.3.2&MSH:12.3.3&MSH:12.3.4&MSH:12.3.5&MSH:12.3.6|MSH:13|MSH:14|MSH:15|MSH:16|MSH:17
EVN|EVN:1|EVN:2.1^EVN:2.2|EVN:3.1^EVN:3.2|EVN:4|EVN:5(1).1^EVN:5(1).2.1&EVN:5(1).2.2&EVN:5(1).2.3&EVN:5(1).2.4&EVN:5(1).2.5^EVN:5(1).3^EVN:5(1).4^EVN:5(1).5^EVN:5(1).6^EVN:5(1).7^EVN:5(1).8^EVN:5(1).9.1&EVN:5(1).9.2&EVN:5(1).9.3^EVN:5(1).10^EVN:5(1).11^EVN:5(1).12^EVN:5(1).13^EVN:5(1).14.1&EVN:5(1).14.2&EVN:5(1).14.3^EVN:5(1).15^EVN:5(1).16.1&EVN:5(1).16.2&EVN:5(1).16.3&EVN:5(1).16.4&EVN:5(1).16.5&EVN:5(1).16.6^EVN:5(1).17.1.2^EVN:5(1).18^EVN:5(1).19.1&EVN:5(1).19.2^EVN:5(1).20.1&EVN:5(1).20.2^EVN:5(1).21^EVN:5(1).22.1&EVN:5(1).22.2&EVN:5(1).22.3&EVN:5(1).22.4&EVN:5(1).22.5&EVN:5(1).22.6&EVN:5(1).22.7&EVN:5(1).22.8&EVN:5(1).22.9^EVN:5(1).23.1&EVN:5(1).23.2&EVN:5(1).23.3&EVN:5(1).23.4&EVN:5(1).23.5&EVN:5(1).23.6&EVN:5(1).23.7&EVN:5(1).23.8&EVN:5(1).23.9|EVN:6.1^EVN:6.2|EVN:7.1^EVN:7.2^EVN:7.3
...
]]></test>
}

XData TESTMessageTarget
{
<test><![CDATA[
MSH|^~\&|MSH:3.1^MSH:3.2^MSH:3.3|MSH:4.1^MSH:4.2^MSH:4.3|MSH:5.1^MSH:5.2^MSH:5.3|MSH:6.1^MSH:6.2^MSH:6.3|MSH:7.1^MSH:7.2|MSH:8|MSH:9.1^MSH:9.2^MSH:9.3|MSH:10|MSH:11.1^MSH:11.2|MSH:12.1^MSH:12.1&MSH:12.2&MSH:12.3&MSH:12.4&MSH:12.5&MSH:12.6^MSH:12.3.1&MSH:12.3.2&MSH:12.3.3&MSH:12.3.4&MSH:12.3.5&MSH:12.3.6|MSH:13|MSH:14|MSH:15|MSH:16|MSH:17
EVN|EVN:1|EVN:2.1^EVN:2.2|EVN:3.1^EVN:3.2|EVN:4|EVN:5(1).1^EVN:5(1).2.1&EVN:5(1).2.2&EVN:5(1).2.3&EVN:5(1).2.4&EVN:5(1).2.5^EVN:5(1).3^EVN:5(1).4^EVN:5(1).5^EVN:5(1).6^EVN:5(1).7^EVN:5(1).8^EVN:5(1).9.1&EVN:5(1).9.2&EVN:5(1).9.3^EVN:5(1).10^EVN:5(1).11^EVN:5(1).12^EVN:5(1).13^EVN:5(1).14.1&EVN:5(1).14.2&EVN:5(1).14.3^EVN:5(1).15^EVN:5(1).16.1&EVN:5(1).16.2&EVN:5(1).16.3&EVN:5(1).16.4&EVN:5(1).16.5&EVN:5(1).16.6^EVN:5(1).17.1.2^EVN:5(1).18^EVN:5(1).19.1&EVN:5(1).19.2^EVN:5(1).20.1&EVN:5(1).20.2^EVN:5(1).21^EVN:5(1).22.1&EVN:5(1).22.2&EVN:5(1).22.3&EVN:5(1).22.4&EVN:5(1).22.5&EVN:5(1).22.6&EVN:5(1).22.7&EVN:5(1).22.8&EVN:5(1).22.9^EVN:5(1).23.1&EVN:5(1).23.2&EVN:5(1).23.3&EVN:5(1).23.4&EVN:5(1).23.5&EVN:5(1).23.6&EVN:5(1).23.7&EVN:5(1).23.8&EVN:5(1).23.9|EVN:6.1^EVN:6.2|EVN:7.1^EVN:7.2^EVN:7.3
...
]]></test>
}
```
Additional Source and expected output messages can be added as datablocks.
Simply use names starting with "TEST" and ending with <em>Source</em> or <em>Target</em> accordingly.
The additional tests are automatically added to the unit test run.

For programatically adding new Source messages and optionally generated outputs see method <em>AddTestFromMessageBody</em>
```objectscript
set tSC=##class(UnitTest.Test.DTL.TestTrans.TransformSource2).AddTestFromMessageBody("EnsLib.HL7.Message",2790,1,.sourceXdataName,.targetXdataName)
```
Populate Test XData blocks with message content<br/>
Parameters:<br/>
 - source Classname - eg: EnsLib.HL7.Message
 - sourceId - Saved ObjectId
 - generateDTLResult - "1" = Yes, "0"= No
 - sourceXdataName - Optional ByRef for output review
 - targetXdataName - Optional ByRef for output review


### Step 4 - Core UnitTest runner dependency
The generated TestCases have the TestSuite of "TestDTL".<br/>
In the namespace the global ^UnitTestRoot must point at a real local directory. For example:
```objectscript
zw ^UnitTestRoot
^UnitTestRoot="C:\temp"
```
For a TestSuite of "TestDTL", this means a directory with name "TestDTL" is required to exist. For example:
```Text
c:\temp\TestDTL
```
This is more to do with a dependency of the core UnitTest framework.<br/>
The TestCase will alert you if the directory doesn't exist or a different TestSuite is used.
```objectscript
Parameter TestSuite = "MyOtherTestSuite";
```

### Step 4 - Run the TestCase
This will generate output on the console, with either success of failure 
```objectscript
do ##class(UnitTest.Test.DTL.TestTrans.TransformSource2).Debug()
```

```Text AssertEquals:2.5:ADT_A01->NK1(1):NextofKinAssociatedPartysIde(1).AssigningFacility.UniversalID=2.5:ADT_A01->NK1(1):NextofKinAssociatedPartysIde(1).AssigningFacility.UniversalID:Expected="NK1(1):33.6.2", Actual="NK1(1):33.6.2" (passed)                                                                                      LogMessage:Duration of execution: 1.522151 sec.
      TestMessage failed
    UnitTest.Test.DTL.TestTrans.TransformSource2 failed
  Skipping deleting classes
  TestDTL failedUse the following URL to view the result:
http://192.168.101.1:52773/csp/sys/%25UnitTest.Portal.Indices.cls?Index=44&$NAMESPACE=DTL_TEST                                                                Some tests FAILED in suites:
  TestDTL
```
### Step 5 - Review the results
Drill down into results using the URL generated by Core UnitTest functionality above.

* Where the source Transform uses an expression that is invalid for the source schema, this will be flagged by the UnitTest<br/>
![Assert Failed Unable To Access Property Path](/images/UnableToAccessPropertyPath.png "Assert Failed Unable To Access Property Path")

* Where each expected value from the input TestMethodTarget DTL did not match the Actual value produced in the tranform, this will be highlighted.<br/>
This helps trap breaking changes either in Schema or Transform maintenance.<br/>
![Assert Failed ExpectedNotActual](/images/ExpectedNotActual.png "Assert Failed ExpectedNotActual")

* Where the Source and Target(Expected) HL7 messages are not schema conforming<br/>
![Assert Failed OverrideSegmentValidation](/images/OverrideSegmentValidation.png "Assert Failed OverrideSegmentValidation")<br/>
As the message suggests: The validation can be disabled in generated TestCase, to continue path validation regardless of segment structure.
```objectscript
Parameter RequireValidSegmentStructure = 0;
```

* Unable to read the HL7 from Source and Target XData blocks<br/>
Please check Source and Target messages were added to generated TestCase<br/>
![Assert Failed UnableToCorrelateHL7](/images/UnableToCorrelateHL7.png "UnableToCorrelateHL7")
```Text
AssertFail:Correlate Message TESTMessageSource->ERROR #5001: Unable to ImportFromString with classname_"UnitTest.Test.DTL.TestTrans.TransformSource2"_XData "TESTMessageSource" with Schema "2.5:ADT_A01" (failed)  <<==== **FAILED**   TestDTL:UnitTest.Test.DTL.TestTrans.TransformSource2:TestMessage                                LogMessage:Duration of execution: .005246 sec.
      TestMessage failed
    UnitTest.Test.DTL.TestTrans.TransformSource2 failed
  Skipping deleting classes
  TestDTL failed
```

# Bonus Features
Extending the available core UnitTest Assertions the generated DTL TestCase provides new capabilities:

## AssertListContainsPath
Usecase to constrain the output of a transformation to a range of values.
Usecase 1:<br/.
There is a side-effect when the first time a transform is run it has the first value.
The second time a transform is run it has the second value.
Subsequent transforms also have the second value.
It is better to be able to constrain by unit tests the two possible values than to not constrain these output values at all.<br/>
Usecase 2:<br/>
Recieve order update messages by the Hospital System from a Radiology System.<br/>
Validate the OrderStatus is constrained to a list of expected values.<br/>
Description of parameters:<br/>
pTarget - An instance of EnsLib.HL7.Message or EnsLib.HL7.Segment<br/>
pTargetPath - The virtual document path to extract test value from. eg: "MSH:9.2" <br/>
pList - An ObjectScript list containing a list of values for equality eg: $LISTBULID("AB","B","C")<br/>
Usage :
```objectscript
do ..AssertListContainsPath(actualTarget,"OBR:ResultStatus",$LB("F","K"))
```
## AssertListNotContainsPath
Converse of the Assert function AssertListContainsPath.<br/>
Description of parameters:<br/>
 - pTarget - An instance of EnsLib.HL7.Message or EnsLib.HL7.Segment<br/>
 - pTargetPath - The virtual document path to extract test value from. eg: "MSH:9.2" <br/>
 - pList - An ObjectScript List containing a list of values for equality eg: $LISTBULID("AB","B","C")<br/>
Usage :
```objectscript
do ..AssertListNotContainsPath(actualTarget,"OBR:ResultStatus",$LB("P","E"))
```

## AssertObjectExists
Extending Assert method to validate that for object references:
 - The expected value is not empty
 - The actual value after transformation is not empty
 - Both the expected value and the actual value match

## AssertObjectListLengthEqual
Check counts of sub-elements in path resolve to equal length lists
 - Return 0 = ASSERT fail
 - Return 1 = ASSERT OK
 
## AssertPathEqualsNotEmpty
Extending Assert method to validate that for virtual document path:
 - The expected value is not empty
 - The actual value after transformation is not empty
 - Both the expected value and the actual value match

