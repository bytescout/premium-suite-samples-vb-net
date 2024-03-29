## How to remove empty pages with pdf extractor sdk in VB.NET and ByteScout Premium Suite

### Learn to code in VB.NET to remove empty pages with pdf extractor sdk with this step-by-step tutorial

The code displayed below will guide you to install an VB.NET app to remove empty pages with pdf extractor sdk. ByteScout Premium Suite: the set that includes 12 SDK products from ByteScout including tools and components for PDF, barcodes, spreadsheets, screen video recording. It can remove empty pages with pdf extractor sdk in VB.NET.

The SDK samples given below describe how to quickly make your application do remove empty pages with pdf extractor sdk in VB.NET with the help of ByteScout Premium Suite.  Simply copy and paste in your VB.NET project or application you and then run your app! If you want to use these VB.NET sample examples in one or many applications then they can be used easily.

All these programming tutorials along with source code samples and ByteScout free trial version are available for download from our website.

## REQUEST FREE TECH SUPPORT

[Click here to get in touch](https://bytescout.zendesk.com/hc/en-us/requests/new?subject=ByteScout%20Premium%20Suite%20Question)

or just send email to [support@bytescout.com](mailto:support@bytescout.com?subject=ByteScout%20Premium%20Suite%20Question) 

## ON-PREMISE OFFLINE SDK 

[Get Your 60 Day Free Trial](https://bytescout.com/download/web-installer?utm_source=github-readme)
[Explore SDK Docs](https://bytescout.com/documentation/index.html?utm_source=github-readme)
[Sign Up For Online Training](https://academy.bytescout.com/)


## ON-DEMAND REST WEB API

[Get your API key](https://pdf.co/documentation/api?utm_source=github-readme)
[Explore Web API Documentation](https://pdf.co/documentation/api?utm_source=github-readme)
[Explore Web API Samples](https://github.com/bytescout/ByteScout-SDK-SourceCode/tree/master/PDF.co%20Web%20API)

## VIDEO REVIEW

[https://www.youtube.com/watch?v=NEwNs2b9YN8](https://www.youtube.com/watch?v=NEwNs2b9YN8)




<!-- code block begin -->

##### ****Module1.vb:**
    
```
Imports System.IO
Imports Bytescout.PDFExtractor

''' <summary>
''' The example demonstrates detection of empty pages, splitting the document to separate 
''' pages excluding empty ones, then combine parts back to a single document.
''' </summary>
Module Module1

    Dim InputFile = ".\sample.pdf"
    Dim OutputFile = ".\result.pdf"
    Dim TempFolder = ".\temp"

    Sub Main()

        ' Create and setup Bytescout.PDFExtractor.TextExtractor instance
        Dim extractor As New TextExtractor("demo", "demo")
        
        ' Load PDF document
        extractor.LoadDocumentFromFile(InputFile)

        ' List to keep non-empty page numbers
        Dim nonEmptyPages = New List(Of String)()

        ' Iterate through pages 
        For pageIndex = 0 To extractor.GetPageCount() - 1
            ' Extract page text
            Dim pageText = extractor.GetTextFromPage(pageIndex)
            ' If extracted text is not empty keep the page number
            If pageText.Length > 0 Then
                nonEmptyPages.Add((pageIndex + 1).ToString())
            End If
        Next
        
        ' Cleanup
        extractor.Dispose()


        ' Form comma-separated list of page numbers to split ("1,3,5")
        Dim ranges As String = String.Join(",", nonEmptyPages)

        ' Create Bytescout.PDFExtractor.DocumentSplitter instance
        Dim splitter = new DocumentSplitter("demo", "demo")
        splitter.OptimizeSplittedDocuments = true

        ' Split document by non-empty in temp folder
        Dim parts = splitter.Split(InputFile, ranges, TempFolder)

        ' Cleanup
        splitter.Dispose()

        
        ' Create Bytescout.PDFExtractor.DocumentMerger instance
        Dim merger = New DocumentMerger("demo", "demo")

        ' Merge parts
        merger.Merge(parts, OutputFile)

        ' Cleanup
        merger.Dispose()

        ' Delete temp folder
        Directory.Delete(TempFolder, true)
        

        ' Open the result file in default PDF viewer (for demo purposes)
        Process.Start(OutputFile)

    End Sub

End Module

```

<!-- code block end -->    

<!-- code block begin -->

##### ****RemoveEmptyPagesExample.vbproj:**
    
```
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="15.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <Import Project="$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\Microsoft.Common.props" Condition="Exists('$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\Microsoft.Common.props')" />
  <PropertyGroup>
    <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
    <Platform Condition=" '$(Platform)' == '' ">AnyCPU</Platform>
    <ProjectGuid>{4A0EB4A0-C386-4F93-90B8-E6978A6E2077}</ProjectGuid>
    <OutputType>Exe</OutputType>
    <StartupObject>RemoveEmptyPagesExample.Module1</StartupObject>
    <RootNamespace>RemoveEmptyPagesExample</RootNamespace>
    <AssemblyName>RemoveEmptyPagesExample</AssemblyName>
    <FileAlignment>512</FileAlignment>
    <MyType>Console</MyType>
    <TargetFrameworkVersion>v4.0</TargetFrameworkVersion>
  </PropertyGroup>
  <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">
    <PlatformTarget>AnyCPU</PlatformTarget>
    <DebugSymbols>true</DebugSymbols>
    <DebugType>full</DebugType>
    <DefineDebug>true</DefineDebug>
    <DefineTrace>true</DefineTrace>
    <OutputPath>bin\Debug\</OutputPath>
    <DocumentationFile>RemoveEmptyPagesExample.xml</DocumentationFile>
    <NoWarn>42016,41999,42017,42018,42019,42032,42036,42020,42021,42022</NoWarn>
  </PropertyGroup>
  <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|AnyCPU' ">
    <PlatformTarget>AnyCPU</PlatformTarget>
    <DebugType>pdbonly</DebugType>
    <DefineDebug>false</DefineDebug>
    <DefineTrace>true</DefineTrace>
    <Optimize>true</Optimize>
    <OutputPath>bin\Release\</OutputPath>
    <DocumentationFile>RemoveEmptyPagesExample.xml</DocumentationFile>
    <NoWarn>42016,41999,42017,42018,42019,42032,42036,42020,42021,42022</NoWarn>
  </PropertyGroup>
  <PropertyGroup>
    <OptionExplicit>On</OptionExplicit>
  </PropertyGroup>
  <PropertyGroup>
    <OptionCompare>Binary</OptionCompare>
  </PropertyGroup>
  <PropertyGroup>
    <OptionStrict>Off</OptionStrict>
  </PropertyGroup>
  <PropertyGroup>
    <OptionInfer>On</OptionInfer>
  </PropertyGroup>
  <ItemGroup>
    <Reference Include="Bytescout.PDFExtractor, Version=9.0.0.3080, Culture=neutral, PublicKeyToken=f7dd1bd9d40a50eb, processorArchitecture=MSIL">
      <SpecificVersion>False</SpecificVersion>
      <HintPath>..\..\..\..\Program Files\Bytescout PDF Extractor SDK\net4.00\Bytescout.PDFExtractor.dll</HintPath>
    </Reference>
    <Reference Include="System" />
    <Reference Include="System.Data" />
    <Reference Include="System.Xml" />
    <Reference Include="System.Core" />
    <Reference Include="System.Xml.Linq" />
  </ItemGroup>
  <ItemGroup>
    <Import Include="Microsoft.VisualBasic" />
    <Import Include="System" />
    <Import Include="System.Collections" />
    <Import Include="System.Collections.Generic" />
    <Import Include="System.Data" />
    <Import Include="System.Diagnostics" />
    <Import Include="System.Linq" />
    <Import Include="System.Xml.Linq" />
  </ItemGroup>
  <ItemGroup>
    <Compile Include="Module1.vb" />
    <Compile Include="My Project\AssemblyInfo.vb" />
    <Compile Include="My Project\Application.Designer.vb">
      <AutoGen>True</AutoGen>
      <DependentUpon>Application.myapp</DependentUpon>
    </Compile>
    <Compile Include="My Project\Resources.Designer.vb">
      <AutoGen>True</AutoGen>
      <DesignTime>True</DesignTime>
      <DependentUpon>Resources.resx</DependentUpon>
    </Compile>
    <Compile Include="My Project\Settings.Designer.vb">
      <AutoGen>True</AutoGen>
      <DependentUpon>Settings.settings</DependentUpon>
      <DesignTimeSharedInput>True</DesignTimeSharedInput>
    </Compile>
  </ItemGroup>
  <ItemGroup>
    <EmbeddedResource Include="My Project\Resources.resx">
      <Generator>VbMyResourcesResXFileCodeGenerator</Generator>
      <LastGenOutput>Resources.Designer.vb</LastGenOutput>
      <CustomToolNamespace>My.Resources</CustomToolNamespace>
      <SubType>Designer</SubType>
    </EmbeddedResource>
  </ItemGroup>
  <ItemGroup>
    <Content Include="sample.pdf">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </Content>
    <None Include="My Project\Application.myapp">
      <Generator>MyApplicationCodeGenerator</Generator>
      <LastGenOutput>Application.Designer.vb</LastGenOutput>
    </None>
    <None Include="My Project\Settings.settings">
      <Generator>SettingsSingleFileGenerator</Generator>
      <CustomToolNamespace>My</CustomToolNamespace>
      <LastGenOutput>Settings.Designer.vb</LastGenOutput>
    </None>
  </ItemGroup>
  <Import Project="$(MSBuildToolsPath)\Microsoft.VisualBasic.targets" />
</Project>
```

<!-- code block end -->