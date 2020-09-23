<div align="center">

## Embed and extract DLLs or any other file


</div>

### Description

This is my first tutorial here on Planet Source Code.

This is to show a user how to add a file to the program such as a DLL that can be extracted to the folder with the program in it or anywhere the DLL needs to be placed.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[kicktd](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/kicktd.md)
**Level**          |Beginner
**User Rating**    |4.7 (14 globes from 3 users)
**Compatibility**  |VB\.NET
**Category**       |[Files](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/files__10-2.md)
**World**          |[\.Net \(C\#, VB\.net\)](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/net-c-vb-net.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/kicktd-embed-and-extract-dlls-or-any-other-file__10-4600/archive/master.zip)





### Source Code

<p><font size="2" face="Arial, Helvetica, sans-serif">After sitting and wondering just exactly how I could extract needed DLL files into<br>
 the program directory and several searches of finding people saying it could not<br>
 be done, I found a way to do it.<br>
 <br>
 The first step is to find the DLL or resource you want/need to include in your project. <br>
 Find the file and drag it into your VB.NET Solution or right click on your form in the <br>
 solution explorer -> Add... -> Add Existing Item... and in the Files of type drop down <br>
 box select All Files (*.*) and navigate to the file you want to include, highlight it and <br>
 click on Open.<br>
 <br>
 You will now see the file in your Solution Explorer. Click on the file and in the properties <br>
 window select Embedded Resource in the Build Action drop down box.<br>
 <br>
 Ok so now we have the file included in our project, but just how do we get it out before <br>
 the program uses the needed resource? Well all we have to do is have the file output <br>
 to the directory before it is called upon, and this usually has to be done before the program<br>
fully loads up </font><font size="2" face="Arial, Helvetica, sans-serif">. First before we get into details, you must know the
 forms name. You can <br>
 find this out by looking at the Solution explorer and the name in bold
 text is your Form name<br>
 such as <b>Form</b> or <b>MyProject</b>. You will need to know this in the upcoming section.<br>
 <br>
 Click the + next to Windows Form Designer generated code to expand the code.<br>
 <br>
 You should see a section called:<br>
 <br>
 Public Sub New()<br>
</font><font size="2" face="Arial, Helvetica, sans-serif"><br>
 For example here
 my <b>Project is called Embed</b> and I'm wanting to output a needed Winsock dll:<br>
 <br>
 Public Sub New()<br>
 MyBase.New()<br>
 'Get our needed .DLL<br>
 GetResource(Application.StartupPath & "\", "AxInterop.MSWinsockLib.dll", "<b>Embed</b>.AxInterop.MSWinsockLib.dll")<br>
 'This call is required by the Windows Form Designer.<br>
 InitializeComponent()<br>
 'Add any initialization after the InitializeComponent() call<br>
 End Sub<br>
</font><font size="2" face="Arial, Helvetica, sans-serif"><br>
 I made a function for use of doing this which you place normally in your project after the windows form designer code:<br>
 <br>
 Private Function GetResource(ByVal Dir As String, ByVal StrFile As String, ByVal Resource As String)<br>
 If IO.File.Exists(Dir & StrFile) = False Then<br>
 Dim output As New IO.FileStream(Dir & StrFile, IO.FileMode.Create, IO.FileAccess.Write)<br>
 Dim buffer(System.Reflection.Assembly.GetExecutingAssembly.GetManifestResourceStream(Resource).Length - 1) As Byte<br>
 System.Reflection.Assembly.GetExecutingAssembly.GetManifestResourceStream(Resource).Read(buffer, 0, System.Reflection.Assembly.GetExecutingAssembly.GetManifestResourceStream(Resource).Length)<br>
 output.Write(buffer, 0, System.Reflection.Assembly.GetExecutingAssembly.GetManifestResourceStream(Resource).Length)<br>
 System.Reflection.Assembly.GetExecutingAssembly.GetManifestResourceStream(Resource).Close()<br>
 output.Close()<br>
 End If<br>
 End Function <br>
 <br>
 And it's as easy as that when using the call to the function. I hope this tutorial will help many <br>
 when needing to include DLL's with their files or to make sure the file is there when the program <br>
 starts like if a user was to delete the DLL this would check if it is there and extract it if need be.</font></p>

