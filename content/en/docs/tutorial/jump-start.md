+++
date = 2015-05-07T11:09:35Z
title = "Jump Start"
type = "docs"
[menu.doctype]
  parent = "Tutorial"
weight = 1
+++

Requirements: Visual Studio 2013

The Pingo Console framework is modeled after how nuget.exe works.  It produces a standalone exe, with all its dlls embedded as resources.  No need for after the fact packing to turn a c# console app with a bunch of supporting dlls into a single standalone exe.  Most the work in the framework deals with how help is managed and how plugins are to serve help content to the display engine.  The motivation of the framework was to deal with what a console app should be before you actually bring in the code to make it do something.  

At the end of this tutorial we will have created a fully working console app that does some Json conversions, and we will do it without writing hardly any code.  The main thing to get out of this tutorial is to understand how the parts come together to form the app.


### Anatomy of the App.  
1. Console Starter Project  
	This is the stock Microsoft C# project.
	
2. _**Pingo.EmbeddedAssemblies**_ Nuget  
	This is used to create an app that has its assemblies embedded as resources.
	
3. _**Pingo.Console**_ Nuget  
	This is the core framework engine.  I really don't want to expose too much from this project as I didn't write these classes to be consumed externally.
	
4. _**Pingo.CommandLineHelp**_ Nuget  
	This is the Help engine that is really a display engine for help.
	
5. Plugins  
	These are written by you to provide help content and the actually command.
    
### Step by Step instructions 
    A VSIX to do all this will soon follow.  
1. Create a new console project  
    - Name it _**"ConsoleMe"**_
    - Enable Nuget Restore for your Solution
2. Make your Console App a Single Exe  
    - install nuget: _**Pingo.EmbeddedAssemblies**_
    - Agree to the file replacement prompts 
3. Bring in the Pingo Console Kit  
    - install nuget: _**Pingo.CommandLineHelp**_
    - install nuget: **_Pingo.Console_**
4. Bring in a few stock commands  
    - install nuget: _**Pingo.JsonConverters.Commands**_
    - install nuget: _**Pingo.TestCommands**_
5. Edit Program.cs  
    This is the only code that should added to the hosting app.  
    
      ~~~c#
      using System;
      using System.Runtime.CompilerServices;
      using Pingo.CommandLine.Composite;

      namespace ConsoleMe
      {
        class Program
        {
            private static void Main(string[] args)
            {
                AppDomain.CurrentDomain.AssemblyResolve 
                    += new ResolveEventHandler(ConsoleMe.PingoEmbeddedAssemblies.AssemblyResolver.OnResolveAssembly);
                MainCore(args);
            }

            [MethodImpl(MethodImplOptions.NoInlining)]
            private static void MainCore(string[] args)
            {
                Pingo.CommandLine.EntryPoint.Program.MefRunnerEntryPoint(new EntryAssemblyEmbeddedMefAssemblies(), args);
            }
        }
      }
      ~~~  
6. Build and Run 