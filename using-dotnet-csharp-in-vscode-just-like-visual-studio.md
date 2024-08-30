If you are a .NET developer and always wondered if it was possible to have a quality time when developing in VSCode, or for some reason needs to use the editor instead of Visual Studio - it is possible and keeping all the basic functionalities with quality. In this article I will show how I adapted my VSCode (personal and professional - they are separated) to run that tech.

## Initial setup

If you are using .NET for the first time or perhaps setting up a computer from zero, I recommend you to install .NET 8 or superior, just in order to make the **C# Dev Kit** extension work properly when you first install it (we will discuss more about it in the next section). After that, you can have the .NET versions that you want to work on. You can check the options to install dotnet [here](https://dotnet.microsoft.com/). After setting everything up with your dotnet versions, we can start thinking about the extensions that we can install.

## A quick overview about the extensions

Clearly, we are going to use a lot of extensions to mimic the .NET features that we have in Visual Studio, I personally don't see it as a bad thing, but it can vary from person to person. It is also important to clarify that this article follows my experience and these extensions can not be the exact perfect fit for you, but they were - and are - for me, and for a long time (that's why I am writing this article). The extensions are:

- **Main ones**
  - C# Dev Kit
  - C# Curly Formatter
  - C# Namespace Completion
  - .NET Core Test Explorer
  - .NET Stalker Debugger
  - Visual NuGet
- **Optional ones (only appearance)**
  - Studio Icons
  - Visual Studio 2019 Theme
 
# 🧩 C# Dev Kit

This is the most important extension of our list, it is basically a "extension package" containing everything you need to basically run C# in your VSCode - most of things depending on the usage of the .NET CLI and very raw. The original extension description says:
> C# Dev Kit helps you manage your code with a solution explorer and test your code with integrated unit test discovery and execution, elevating your C# development experience wherever you like to develop (Windows, macOS, Linux, and even in a Codespace).

In most cases, this extension usually offers *everything* you need to use .NET with the most basic features - even including testing and breakpoints, but personally, I ran into a lot of problems when trying to use these features, like everything stopping suddenly or not working at all, without apparent problem that required trial and error closing and reopening the IDE and even uninstalling and reinstalling the extension several times (and that is what made me go look for other extensions to fix the faults).
