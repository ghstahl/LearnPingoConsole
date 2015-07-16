+++
date = 2015-05-06T11:09:35Z
title = "Parser"
type = "docs"
[menu.doctype]
  parent = "Developer"
weight = 1
+++

Firstly, Pingo Console doesn't care what parser you use for your commands, as that is in isolation.
 
Keep it simple.  A lot of parsers, including the one I like, have help and description baked in.  Pingo Console's opinion is that help is separate, which reduces what a parser actually does down to its simplest parts.  I don't use the help or description stuff from the parser I use, or any for that matter.  
 
My parser of choice: 
[Pingo Variant: Fluent Command Line Parser](https://github.com/ghstahl/fluent-command-line-parser)
 
For most everything I do the below parsing example is about as complicated as I get.  The only thing my parser is missing is a mutual exclusion option, but I will add that when I need it.
 
```c#
public class TestArgumentParser
{
    public string SourcePath { get; private set; }
    public string OutputPath { get; private set; }
 
    public void Parse(string[] args)
    {
        var parser = new Fclp.FluentCommandLineParser();
 
        parser.Setup<string>(CaseType.CaseInsensitive, Resources.Common.OptionLongName_Source,
            Resources.Common.OptionShortName_Source)
            .Required()
            .Callback(value => SourcePath = value);
 
        parser.Setup<string>(CaseType.CaseInsensitive, Resources.Common.OptionLongName_Output,
            Resources.Common.OptionShortName_Output)
            .Required()
            .Callback(value => OutputPath = value);
 
        var result = parser.Parse(args);
        if (result.HasErrors)
        {
            throw new Exception(result.ErrorText);
        }
    }
}
```
