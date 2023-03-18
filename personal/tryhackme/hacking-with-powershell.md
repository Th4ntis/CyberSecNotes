# Hacking with Powershell

This room can found [here](https://tryhackme.com/room/powershell). It covers: what is Powershell , how it works, basic Powershell commands, windows enumeration with Powershell, and Powershell scripting

Machine credentials:

* Username: Administrator
* Password: BHN2UVw0Q

## Task 2

This also allows Powershell to execute .NET functions directly from its shell. Most Powershell commands, called _cmdlets,_ are written in .NET.&#x20;

Unlike other scripting languages and shell environments, the output of these _cmdlets_ are objects, making Powershell somewhat object oriented. This also means that running cmdlets allows us to perform actions on the output object, which makes it convenient to pass output from one _cmdlet_ to another. The normal format of a _cmdlet_ is represented using **Verb-Noun.**

Common verbs to use include:

* Get
* Start
* Stop&#x20;
* Read
* Write
* New
* Out

Full list of approved verbs are [here](https://docs.microsoft.com/en-us/powershell/scripting/developer/cmdlet/approved-verbs-for-windows-powershell-commands?view=powershell-7).

### Question 1: What is the command to get help about a particular cmdlet(without any parameters)?

`Get-help`

## Task 3

`Get-Command` and `Get-Help` are our best friends!

**Using Get-Help**

Get-Help displays information about a _cmdlet._ To get help about a particular command, run `Get-Help Command-Name`

We can also understand how exactly to use the command by passing in the `-examples` flag.

![](<../../.gitbook/assets/image (125).png>)

#### Using Get-Command

Get-Command gets all the _cmdlets_ installed on the current Computer. This _cmdlet_ allows for pattern matching such as `Get-Command Verb-*` or `Get-Command *-Noun`

Running `Get-Command New-*` to view all the _cmdlets_ for the verb new displays:

![](<../../.gitbook/assets/image (2) (1) (1) (1).png>)

#### Object Manipulation

If we want to actually manipulate the output, we need to figure out a few things:

* passing output to other _cmdlets_
* using specific object _cmdlets_ to extract information

The Pipe ( | ) is used to pass output from one _cmdlet_ to another. A major difference compared to other shells is that instead of passing text or string to the command after the pipe, powershell passes an object to the next cmdlet. Like every object in object oriented frameworks, an object will contain methods and properties.&#x20;

We can think of methods as functions that can be applied to output from the _cmdlet_ and we can think of properties as variables in the output from a cmdlet. To view these details, pass the output of a _cmdlet_ to the Get-Member _cmdlet_ `Verb-Noun | Get-Member`&#x20;

An example of running this to view the members for Get-Command is:

`Get-Command | Get-Member -MemberType Method`

![](<../../.gitbook/assets/image (17) (1).png>)

#### Creating Objects From Previous _cmdlets_

One way of manipulating objects is pulling out the properties from the output of a cmdlet and creating a new object. This is done using the `Select-Object` _cmdlet._&#x20;

An example of listing the directories and just selecting the mode and the name:

![](<../../.gitbook/assets/image (12) (1) (1).png>)

We can also use the following flags to select particular information:

* first - gets the first x object
* last - gets the last x object
* unique - shows the unique objects
* skip - skips x objects

#### Filtering Objects

When retrieving output objects, we _may_ want to select objects that match a very specific value. We can do this using the `Where-Object` to filter based on the value of properties.&#x20;

The general format of the using this _cmdlet_ is:

`Verb-Noun | Where-Object -Property PropertyName -operator Value`

`Verb-Noun | Where-Object {$_.PropertyName -operator Value}`

The second version uses the $\_ operator to iterate through every object passed to the Where-Object cmdlet.

**Powershell is sensitive so make sure we don't put quotes around the command**

Where `-operator` is a list of the following operators:

* \-Contains: if any item in the property value is an exact match for the specified value
* \-EQ: if the property value is the same as the specified value
* \-GT: if the property value is greater than the specified value

Full list of operators can be found [here](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/where-object?view=powershell-6).

An example of checking the stopped processes:

![](<../../.gitbook/assets/image (112) (1).png>)

#### Sort Object

When a _cmdlet_ outputs a lot of information, we may need to sort it to extract the information more efficiently. We do this by pipe lining the output of a _cmdlet_ to the `Sort-Object` _cmdlet_.

The format of the command would be

`Verb-Noun | Sort-Object`

An example of sort the list of directories:

![](<../../.gitbook/assets/image (44).png>)

### Question 1: What is the location of the file "interesting-file.txt"

`C:\Program Files` - Running `Get-ChildItem -Path C:\ -Recurse -File interesting*.txt -ErrorAction SilentlyContinue` will give us our answer.

![](<../../.gitbook/assets/image (127).png>)

### Question 2: Specify the contents of this file

`notsointerestingcontent` - Running `Get-Content 'C:\Program Files\interesting-File.txt.txt'` will give us our answer

![](<../../.gitbook/assets/image (83).png>)

### Question 3: How many cmdlets are installed on the system(only cmdlets, not functions and aliases)?

`6638` - Running `Get-Command -CommandType Cmdlet | measure` will give us our answer. Using Measure calculates the numeric properties of objects, and the characters, words, and lines in string objects, such as files of text. Helpful when parsing or searching for larger amount(s) of information.

![](<../../.gitbook/assets/image (181).png>)

### Question 4: Get the MD5 hash of interesting-file.txt

`49A586A2A9456226F8A1B4CEC6FAB329` - Running `Get-FileHash 'C:\Program Files\interesting-file.txt.txt' -Algorithm MD5` will give us our answer.

![](<../../.gitbook/assets/image (79).png>)

### Question 5: What is the command to get the current working directory?

`Get-Location`

![](<../../.gitbook/assets/image (87).png>)

### Question 6: Does the path "C:\Users\Administrator\Documents\Passwords" Exist(Y/N)?

`N` - Running `Get-Location -Path 'C:\Users\Administrator\Documents\Passwords'` will give us our answer

![](<../../.gitbook/assets/image (145).png>)

### Question 7: What command would you use to make a request to a web server?

`Invoke-WebRequest`

![](<../../.gitbook/assets/image (11) (1) (1).png>)

### Question 8: Base64 decode the file b64.txt on Windows

ihopeyoudidthisonwindows- Find the file first, `Get-ChildItem -Path C:\ -Recurse -File b64.txt -ErrorAction SilentlyContinue`

![](<../../.gitbook/assets/image (185).png>)

Now we can decode the base64 and output to a file, then get the contents of the new file.

`certutil -decode 'C:\Users\Administrator\Desktop\b64.txt' decoded.txt`

`Get-Content 'C:\Users\Administrator\Desktop\decoded.txt'`

![](<../../.gitbook/assets/image (48).png>)

## Task 4

The first step when you have gained initial access to any machine would be to enumerate. We'll be enumerating the following:

* users
* basic networking information
* file permissions
* registry permissions
* scheduled and running tasks
* insecure files

Your task will be to answer the following questions to enumerate the machine using Powershell commands!&#x20;

### Question 1: How many users are there on the machine?

`5` - Running `Get-LocalUser` will give us our answer

![](<../../.gitbook/assets/image (168).png>)

### Question 2: Which local user does this SID(S-1-5-21-1394777289-3961777894-1791813945-501) belong to?

`Guest` - Running `Get-LocalUser -SID "S-1-5-21-1394777289-3961777894-1791813945-501"` gives us our answer

![](<../../.gitbook/assets/image (171).png>)

### Question 3: How many users have their password required values set to False?

`4` - Run `Get-LocalUser | Where-Object -Property PasswordRequired -Match false` to find the answer.

![](<../../.gitbook/assets/image (41).png>)

### Question 4: How many local groups exist?

`24` - Run `Get-LocalGroup | Measure` to find the answer

![](<../../.gitbook/assets/image (123).png>)

### Question 5: What command did you use to get the IP address info?

`Get-NetIPAddress`

![](<../../.gitbook/assets/image (96).png>)

### Question 6: How many ports are listed as listening?

`20` - Run `Get-NetTCPConnection | Where-Object -Property State -Match Listen | Measure` to find our answer.

![](<../../.gitbook/assets/image (178).png>)

### Question 7: What is the remote address of the local port listening on port 445?

`::` - Running `Get-NetTCPConnection | Where-Object -Property State -Match Listen | findstr "445"` will show us our answer.

![](<../../.gitbook/assets/image (92).png>)

### Question 8: How many patches have been applied?

`20` - Run `Get-Hotfix` and count OR `Get-Hotfix | Measure`

![](<../../.gitbook/assets/image (10) (1) (1).png>)

### Question 9: When was the patch with ID KB4023834 installed?

`6/15/2017 12:00:00 AM` - In the above screenshot we can find the answer, BUT we can always run `Get-Hotfix | findstr "KB4023834"` OR `Get-Hotfix -Id KB4023834`

### Question 10: Find the contents of a backup file.

`backpassflag` - First we find the backup file `Get-ChildItem -Path C:\ -include *.bak* -File -Recurse -ErrorAction SilentlyContinue`

![](<../../.gitbook/assets/image (395).png>)

Now we get the contents of that file `Get-Content 'C:\Program Files (x86)\Internet Explorer\passwords.bak.txt'`

![](<../../.gitbook/assets/image (408).png>)

### Question 11: Search for all files containing API\_KEY

`fakekey123` - We can run `Get-ChildItem C:* -Recurse | Select-String -pattern API_KEY` to find the answer. After a while we see an error code.

![](<../../.gitbook/assets/image (82).png>)

### Question 12: What command do you do to list all the running processes?

`Get-Process`

![](<../../.gitbook/assets/image (39).png>)

### Question 13: What is the path of the scheduled task called new-sched-task?

`/` - We can run `Get-ScheduledTask -TaskName new-sched-task` and obtain our answer

![](<../../.gitbook/assets/image (119).png>)

### Question 14: Who is the owner of the C:\\?

`NT SERVICE\TrustedInstaller` - Running `Get-Acl c:/` will show us the owner.

![](<../../.gitbook/assets/image (105) (1).png>)

## Task 5

We'll be using PowerShell ISE(which is the Powershell Text Editor). To show an example of this script, let's use a particular scenario. Given a list of port numbers, we want to use this list to see if the local port is listening. Open the listening-ports.ps1 script on the Desktop using Powershell ISE. Powershell scripts usually have the _.ps1_ file extension.&#x20;

```
$system_ports = Get-NetTCPConnection -State Listen
$text_port = Get-Content -Path C:\Users\Administrator\Desktop\ports.txt
foreach($port in $text_port){
    if($port -in $system_ports.LocalPort){
        echo $port
     }
}
```

On the first line, we want to get a list of all the ports on the system that are listening. We do this using the Get-NetTCPConnection _cmdlet_. We are then saving the output of this _cmdlet_ into a variable. The convention to create variables is used as:

```
$variable_name = value
```

On the next line, we want to read a list of ports from the file. We do this using the Get-Content _cmdlet._ Again, we store this output in the variables. The simplest next step is iterate through all the ports in the file to see if the ports are listening. To iterate through the ports in the file, we use the following

```powershell
foreach($new_var in $existing_var){}
```

This particular code block is used to loop through a set of object. Once we have each individual port, we want to check if this port occurs in the listening local ports. Instead of doing another for loop, we just use an if statement with the `-in` operator to check if the port exists the LocalPort property of any object. A full list of if statement comparison operators can be found [here](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about\_comparison\_operators?view=powershell-6). To run script, just call the script path using Powershell or click the green button on Powershell ISE:

![](<../../.gitbook/assets/image (150).png>)

Now that we've seen what a basic script looks like - it's time to write one of your own. The emails folder on the Desktop contains copies of the emails John, Martha and Mary have been sending to each other(and themselves). Answer the following questions with regards to these emails(try not to open the files and use a script to answer the questions). \


Scripting can be a bit difficult, but [here](https://learnxinyminutes.com/docs/powershell/) is a good resource to use.

### Question 1: What file contains the password?

`Doc3m` - So we can essentially make a script that will run powershell commands from a file by storing them into variables and calling them throughout the script.

```
$path = "C:\Users\Administrator\Desktop\emails*"
$string_pattern = "password"
$command = Get-ChildItem -Path $path -Recurse | Select-String -Pattern $String_patterne
cho $command
```

![](<../../.gitbook/assets/image (118).png>)

### Question 2: What is the password?

`johnisaleggend99` - From the script/command we wrote above, it has our answer as well.

### Question 3: What files contains an HTTPS link?

`Doc2Mary` - We can edit our script above and change the string from `password` to `https://`

```
$path = "C:\Users\Administrator\Desktop\emails*"
$string_pattern = "https://"
$command = Get-ChildItem -Path $path -Recurse | Select-String -Pattern $String_patterne
cho $command
```

![](<../../.gitbook/assets/image (182).png>)
