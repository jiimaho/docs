---
title: "JSON Serialization"
ms.date: "03/30/2017"
ms.assetid: 3c2c4747-7510-4bdf-b4fe-64f98428ef4a
---
# JSON Serialization
This sample demonstrates how to use the <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> to serialize and deserialize data in the JavaScript Object Notation (JSON) format. This serialization engine converts JSON data into instances of .NET Framework types and back into JSON data. <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> supports the same types as <xref:System.Runtime.Serialization.DataContractSerializer>. The JSON data format is especially useful when writing Asynchronous JavaScript and XML (AJAX)-style Web applications. AJAX support in Windows Communication Foundation (WCF) is optimized for use with ASP.NET AJAX through the ScriptManager control. For examples of how to use Windows Communication Foundation (WCF) with ASP.NET AJAX, see the [AJAX Samples](ajax.md).  
  
> [!NOTE]
> The set-up procedure and build instructions for this sample are located at the end of this topic.  
  
 The sample uses a `Person` data contract to demonstrate serialization and deserialization.  

```csharp
[DataContract]
class Person
{
    [DataMember]
    internal string name;

    [DataMember]
    internal int age;
}
```

 To serialize an instance of the `Person` type to JSON, create the <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> first and use the `WriteObject` method to write JSON data to a stream.  

```csharp
Person p = new Person();
//Set up Person object...
MemoryStream stream1 = new MemoryStream();
DataContractJsonSerializer ser = new DataContractJsonSerializer(typeof(Person));
ser.WriteObject(stream1, p);
```

 The memory stream contains valid JSON data.
  
```json  
{"age":42,"name":"John"}  
```  
  
 The sample demonstrates deserializing from JSON data into an object. You then rewind the stream and call `ReadObject`.  

```csharp
Person p2 = (Person)ser.ReadObject(stream1);
```

 Examining the `p2` object reveals that the JSON data has been deserialized correctly.  
  
> [!IMPORTANT]
>  The samples may already be installed on your machine. Check for the following (default) directory before continuing.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples. This sample is located in the following directory.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Ajax\JsonSerialization`  
  
#### To set up, build and run the sample  
  
1. Build the solution JsonSerialization.sln as described in [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
2. Run the resulting console application.  
