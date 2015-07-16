+++
date = 2015-05-06T11:09:35Z
title = "Enhancements"
type = "docs"
[menu.doctype]
  parent = "Developer"
weight = 2
+++

This is a work in progress where I am cherry picking what resources I want to let come in via a plugin.  
At the moment I am only accounting for a header and footer string for the console output pages.  



[Pingo.Theme Reference Project](https://github.com/ghstahl/PingoConsole/tree/master/Pingo.Theme)

1. Create a class library project  
    - Name it **_"My.PingoConsole.Theme"_**
2. Add this project as a reference in your console app  
3. Add the following code to your **_"My.PingoConsole.Theme"_** project  

    ~~~c#
    [Export(typeof(Pingo.CommandLine.Contracts.Help.IHelpResource))]
    public class MakeItMineTheme : Pingo.CommandLine.Contracts.Help.IHelpResource
    {
        public string Header { get { return Resources.Common.Header; } }
        public string Footer { get { return Resources.Common.Footer; } }
    }
    ~~~  
      I have my strings comming out of resources.  