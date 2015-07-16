+++
date = 2015-05-07T11:09:35Z
title = "Create Command Plugin"
type = "docs"
[menu.doctype]
  parent = "Tutorial"
weight = 2
+++

1. Install the _**Pingo.Commandline.PluginTemplate**_ Extension  
    - direct: [Extension](https://visualstudiogallery.msdn.microsoft.com/7b579419-fdbd-4b47-880c-261409120bb9)
    - Visual Studio 2013: Tools -> Extensions and Updates... -> Online
    - restart visual studio 2013  
2. Create a new Project  
    - Use the newly installed _**Pingo.Commandline.PluginTemplate**_
    - Name it _**"My.Sweet.Command"**_
    - A wizard prompt asks for what your command name should be.
        - Enter _**"Sweet"**_
    - Press "Done"  
    - Build _**"My.Sweet.Command"**_
    - Add the _**"My.Sweet.Command"**_ project as a reference to _**"ConsoleMe"**_
    - Build **_"ConsoleMe"_**
3. Done and Run!  
    You should see your _**"Sweet"**_ command in the list of now usable commands.  
4. Modify your command project to suit.
5. You can now uninstall the **_Pingo.JsonConverters.Commands_** and **_Pingo.TestCommands_** nugets from _**"ConsoleMe"**_, Unless you really want to keep them in there for their profound **_awesomeness_**.
