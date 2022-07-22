<p align="center">
    <img src="Logo.png" width="400" max-width="90%" alt="StatiC#" />
</p>

<p align="center">
    <a href="https://docs.microsoft.com/en-us/dotnet/csharp/">
        <img src="https://img.shields.io/badge/C%23-10.0-blue?style=flat" alt="C# 10.0" />
    </a>
    <a href="https://dotnet.microsoft.com">
        <img src="https://img.shields.io/badge/.NET-6.0-blueviolet?style=flat" />
    </a>
    <img src="https://img.shields.io/badge/Platforms-Win+Mac+Linux-green?style=flat" />
    <img src="https://img.shields.io/badge/Version-0.1.0--alpha9-green?style=flat" />
    <a href="https://www.nuget.org/packages/StatiCSharp">
        <img src="https://img.shields.io/nuget/v/StatiCSharp?color=orange" />
    </a>
</p>

Welcome to **StatiC#**, a static website generator written in C#. It enables entire websites to be built using C#. Custom themes can be used by editing the integrated default theme or by importing a theme.

---

StatiC# provides everything you need to create a website with all the files needed to upload onto a webserver.  

If you want to quickstart with your new website, you can start with the [default configuration](https://github.com/RolandBraunDev/StatiCSharp/tree/develop/Documentation/ProjectTemplate) and build up from there. Here is an example:

```C#
using StatiCSharp;

var myAwesomeWebsite = new Website(
    url: "https://yourdomain.com",
    name: "My Awesome Website",
    description: @"Description of your website",
    language: "en-US",
    sections: "posts, about"            // Select which folders should be treated as sections.
);

var manager = new WebsiteManager(
    website: myAwesomeWebsite,
    source: @"/path/to/your/project"    // Path to the folder of your website project.
);

manager.Make();
```


## Add StatiC# to your project

To get started, create a new console application at a path of your choice. Let's say that your new website is called *myWebsite*:

```
$ dotnet new console -n myWebsite
```
After .NET has created the project files open `myWebsite.csproj` and add StatiC# as a package reference. The file should then look something like this:

```
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net6.0</TargetFramework>
    <ImplicitUsings>enable</ImplicitUsings>
    <Nullable>enable</Nullable>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="StatiCSharp" Version="0.1.0-alpha9" />
  </ItemGroup>

</Project>
```

Then you can get started using StatiC# by importing it at the beginning of your `Program.cs`:

```C#
using StatiCSharp;
```

## Quick start

You can use StatiC#'s [project template](/Documentation/ProjectTemplate) to quick start or follow the following steps to set up your project manually.  
Nevertheless its recommended to read this readme to get a understanding how StatiC# works.  

StatiC# expects three folders to work with at the path given during the initialization of the WebsiteManager.  
  
`Content`: This folder contains the markdown files that our website depents on.  
`Output`: Here the final website with all the necessary files will be saved.  
`Resources`: Put all your static files in here. All files will be copied, without any manipulation, to the output. Folders are migrated.  

It's recommented to put those folders within your project folder of *myWebsite*. Your folder should look something like this:

```
├── myWebsite
│   ├── Content
│   ├── Outout
│   ├── Resources
│   ├── myWebsite.csproj
│   ├── Program.cs
```
StatiC# renders four different types of sites:  

*index*: The homepage of your website  
*pages*: Normal sites e.g. your about page.  
*sections*: Sites that contain items e.g. articles in a specific field.  
*items*: The sites that are part of a section.  
  
Add some content to your website by adding your markdown files to the `Content` folder. Check out the [documentation](/Documentation) for a [template file](Documentation/HowTo/content-template.md):

```
├── myWebsite
│   ├── Content
│   │   ├── index.md                    // This is your homepage.
│   │   ├── posts                       // Contains all items for the posts section.
│   │   │   ├── index.md                // Content of the section site.
│   │   │   ├── your-first-post.md      // Item within the posts section.
│   │   │   ├── your-second-post.md     // Another item within the posts section.
│   │   ├── about                       // Contains a page.
│   │   │   ├── index.md                // Content of the about page.
│   │   │   ├── another-page.md         // Content of another page.
│   ├── Outout
│   ├── Resources
│   ├── myWebsite.csproj
│   ├── Program.cs
```

Store your content in folders and StatiC# cares about the rest. All folders are treated as pages unless their name is used to build a section.  

Finally set up the parameters in `Program.cs` in your *myWebsite* project:

```C#
using StatiCSharp;

var myAwesomeWebsite = new Website(
    url: "https://yourdomain.com",
    name: "My Awesome Website",
    description: @"Description of your website",
    language: "en-US",
    sections: "posts, about"            // Select which folders should be treated as sections.
);

var manager = new WebsiteManager(
    website: myAwesomeWebsite,
    source: @"/path/to/your/project"    // Path to the folder of your website project.
);

manager.Make();
```

Run the project and your new awesome website will be generated in the `Output` directory:
```
$ dotnet run
```

Check out the [documentation](/Documentation) for further information.

## Dependencies

- [Microsoft .NET](https://dotnet.microsoft.com/)
- [Markdig](https://github.com/xoofx/markdig)



## Contributions and support

StatiC# is developed completely open, and your contributions are more than welcome.

Before you start using StatiC# in any of your projects, please have in mind that it’s a hobby project and there is no guarantee for technical correctness or future releases.  

Since this is a very young project, it’s likely to have many limitations and missing features, which is something that can really only be discovered and addressed as you use it. While StatiC# is used in production on my personal website, it’s recommended that you first try it out for your specific use case, to make sure it supports the features that you need.  

If you wish to make a change, [open a Pull Request](https://github.com/RolandBraunDev/StatiCSharp/pull/new) — even if it just contains a draft of the changes you’re planning, or a test that reproduces an issue — and we can discuss it further from there.

I hope you’ll enjoy using StatiC#!
