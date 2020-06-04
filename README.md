# UnityStyleGuide
For files, directories, scripts and a lot of other thing

# Thanks
This guide has been brazenly copied and supplemented from these sources for your convenience :)

Let's thank these guys and give them a star.

https://github.com/stillwwater/UnityStyleGuide#folders

https://github.com/raywenderlich/c-sharp-style-guide#brace-style

# Table of Contents

- [Asset Naming](#asset-naming)
    - [Folders](#folders)
    - [Non-code assets](#non-code-assets)
- [File structure](#file-structure)
    - [Assets](#assets)
    - [Scripts](#scripts)
    - [Models](#models)
- [Source code](#source-code)
    - [Naming](#naming)
    - [Declarations](#declarations)
    - [Brace Style](#brace-style)
    - [Recomendations](#recomendations)
- [Workflow](#workflow)
    - [Models](#models)
    - [Textures](#textures)
    - [Configuration files](#configuration-files)
    - [Localization](#localization)
- [Suffixes and Shortcuts](#suffixes-and-shortcuts)
    - [General Prefixex](#general-prefixes)
    - [Texure Suffixes](#texture-suffixes)

# Asset Naming

First of all, no\ spaces\ on file or directory names.

## Folders

`PascalCase`

Prefer a deep folder structure over having long asset names.

Directory names should be as concise as possible, prefer one or two words. If a directory name is too long, it probably makes sense to split it into sub directories.

Try to have only one file type per folder. Use `Textures/Trees`, `Models/Trees` and not `Trees/Textures`, `Trees/Models`. That way its easy to set up root directories for the different software involved, for example, Substance Painter would always be set to save to the Textures directory.

If your project contains multiple environments or art sets, use the asset type for the parent directory: `Trees/Jungle`, `Trees/City` not `Jungle/Trees`, `City/Trees`. Since it makes it easier to compare similar assets from different art sets to ensure continuity across art sets.

### Debug Folders

`[PascalCase]`

This signifies that the folder only contains assets that are not ready for production. For example, having an `[Assets]` and `Assets` folder.

## Non-Code Assets

If the asset name is long, choose the word order depending on what categories / subcategories you want to group assets: 
Use `tree_small` not `small_tree`. While the latter sound better in English, it is much more effective to group all tree objects together instead of all small objects.

`camelCase` where necessary. Use `weapon_miniGun` instead of `weapon_gun_mini`. Avoid this if possible, for example, `vehicles_fighterJet` should be `vehicles_jet_fighter` if you plan to have multiple types of jets.

Prefer using descriptive suffixes instead of iterative: `vehicle_truck_damaged` not `vehicle_truck_01`. If using numbers as a suffix, always use 2 digits. And **do not** use it as a versioning system! Use `git` or something similar.

### Persistent/Important GameObjects

`_snake_case`

Use a leading underscore to make object instances that are not specific to the current scene stand out.

### Debug Objects

`[SNAKE_CASE]`

Enclose objects that are only being used for debugging/testing and are not part of the release with brackets.

# File Structure

```
Root
+---Assets
+---Build
\---Tools           # Programs to aid development: compilers, asset managers etc.
```

## Assets

```
Assets
+---Art
|   +---Materials
|   +---Models      # FBX and BLEND files
|   +---Prefabs
|   +---Textures    # PNG files
|   +---UI
|   +---VFX         # Visual effects, particles, etc
+---Audio
|   +---Music
|   \---Sound       # Samples and sound effects
+---Code
|   +---Scripts     # C# scripts
|   \---Shaders     # Shader files and shader graphs
+---Docs            # Wiki, concept art, marketing material
+---Level           # Anything related to game design in Unity
|   +---Prefabs
|   +---Scenes
|   \---UI
\---Resources       # Configuration files, localization text and other user files.
```

## Scripts

Use namespaces that match your directory structure.

A Framework directory is great for having code that can be reused across projects.

The Scripts folder varies depending on the project, however, `Environment`, `Framework`, `Tools` and `UI` should be consistent  across projects.

```
Scripts
+---Environment
+---Framework
+---NPC
+---Player
+---Tools
\---UI
```

## Models

Separate files from the modelling program and ready to use, exported models.

```
Models
+---Blend
\---FBX
```

# Source Code

## Naming ##

Use the naming convention of the programming language. For C# and shader files use `PascalCase`, as per C# convention.

### Namespaces

Namespaces are all **PascalCase**, multiple words concatenated together, without hyphens ( - ) or underscores ( \_ ). The exception to this rule are acronyms like GUI or HUD, which can be uppercase:

**AVOID**:

```csharp
com.raywenderlich.fpsgame.hud.healthbar
```

**PREFER**:

```csharp
RayWenderlich.FPSGame.HUD.Healthbar
```


### Classes & Interfaces

Classes and interfaces are written in **PascalCase**.

```csharp
public class SomeClass{}
```

### Methods

Methods are written in **PascalCase**.

```csharp
private void DoSomething()
```

### Parameters

Parameters are written in **camelCase**.

```csharp
private void DoSomething(Vector3 location)
```

 
### Fields

All non-static fields are written **camelCase**. Per Unity convention, this includes **public fields** as well.

For example:

```csharp
public class MyClass 
{
    public int publicField;
    private int _myPrivate;
    protected int _myProtected;
}
```

Do not use **public**. Prefer properties.

Prefer to use _ prefix for **private, protected and internal fields**.

```csharp
private int _myPrivate = 0;
```

If you need to show field in the inspector, but field is **private** use `[SerializeField]`:

```csharp
[SerializeField] private int _myPrivate = 0;
```

Static fields are the exception and should be written in **PascalCase**:

```csharp
public static int TheAnswer = 42;
```

For const fields use **UPPER_CASE**:

```csharp
public const int MY_CONST_VALUE = 0;
```

### Enums 

Use **PascalCase** for enum:

```csharp
enum SampleEnum
{
    FirstValue,
    SecondValue
}
```

## Declarations ##

### Access Level Modifiers

Access level modifiers should be explicitly defined for classes, methods and member variables.

### Fields & Variables

Prefer single declaration per line.

**AVOID:**

```csharp
private string username, twitterHandle;
```

**PREFER:**

```csharp
private string username;
private string twitterHandle;
```

**BUT:**

You can use multiple declaration for **really** similar fields.

```csharp
private xPos, yPos, zPos = 0;
public GameObject wallLeft, wallRight, wallUp, wallDown;
```

### Properties

All properties are written in **PascalCase**. For example:

```csharp
public int PageNumber 
{
    get { return pageNumber; }
    set { pageNumber = value; }
}
```

Also you can use a short option:

```csharp
public int PageNumber => pageNumber;
```

### Actions

Actions are written in **PascalCase**. For example:

```csharp
public event Action<int> ValueChanged;
```

### Misc

In code, acronyms should be treated as words. For example:

**AVOID:**

```csharp
XMLHTTPRequest
String URL
findPostByID
```  

**PREFER:**

```csharp
XmlHttpRequest
String url
findPostById
```

## Attributes

A lot of different attributes here: https://assetstore.unity.com/packages/tools/utilities/naughtyattributes-129996#description

This assset even `[SerializeField]` properties.

## Declaration order: ##
1. private, protected fields (in this order)
2. properties
3. private, protected, public methods (in this order)

## Brace Style

All braces get their own line as it is a C# convention:

**AVOID:**

```csharp
class MyClass {
    void DoSomething() {
        if (someTest) {
          // ...
        } else {
          // ...
        }
    }
}
```

**PREFER:**

```csharp
class MyClass
{
    void DoSomething()
    {
        if (someTest)
        {
          // ...
        }
        else
        {
          // ...
        }
    }
}
```

Conditional statements are always required to be enclosed with braces,
irrespective of the number of lines required.

**AVOID:**

```csharp
if (someTest)
    doSomething();  

if (someTest) doSomethingElse();
```

**PREFER:**

```csharp
if (someTest) 
{
    DoSomething();
}  

if (someTest)
{
    DoSomethingElse();
}
```

## Recomendations ##

• Avoid using shortcut names like **i** and **t**, use **index** and **temp**. Do not use Hungarian notation or use it only for private members. Do not shorten the words, use number, not num.
• It is recommended that names of control elements include prefixes that describe the type of element. For example: **txtSample, lblSample, cmdSample or btnSample**. The same recommendation applies to local variables of complex types: 

```csharp
ThisIsLongTypeName tltnSample = new ThisIsLongTypeName ();
```

• Do not use public or protected fields, use properties instead;
• Use automatic properties;
• Always specify the private access modifier, even if it is allowed to omit it;
• Always initialize variables, even when automatic initialization exists.

# Suffixes and Shortcuts

### General Prefixes

Prefix   | Meaning
:------|:-----------------
`lbl`    | Label
`btn`    | Button
`txt`    | Textbox
`img`    | Image
`chk`    | CheckBox
`rdo`    | RadioButton
`grp`    | GroupBox
`err`    | Error
`mnu`    | MainMenu
`tmr`    | Timer
`lstv`   | ListView
`sbr`    | ScrollBar
`trk`    | TrackBar
`prob`   | ProgressBar
`rtxt`   | RichTextBox
`tip`    | ToolTip
`cmnu`   | ContextMenu
`tbr`    | ToolBar
`statb`  | StatusBar
`proc`   | Process

### Texture Suffixes

Suffix | Texture
:------|:-----------------
`_AL`  | Albedo
`_SP`  | Specular
`_R`   | Roughness
`_MT`  | Metallic
`_GL`  | Glossiness
`_N`   | Normal
`_H`   | Height
`_DP`  | Displacement
`_EM`  | Emission
`_AO`  | Ambient Occlusion
`_M`   | Mask


# Workflow

## Models

File extension: `FBX`

Even though Unity supports Blender files by default, it is better to keep what is being worked on and what is a complete, exported model separate. This is also a must when using other software, such as Substance for texturing.

Use `Y up`, `-Z forward` and `uniform scale` when exporting.

## Textures

File extension: `PNG`, `TIFF` or `HDR`

Choose either a `Specularity/Glossiness` or `Roughness/Metallic` workflow. This depends on the software being used and what your artists are more comfortable with. Specularity maps have the advantage of being having the possibility to be RGB maps instead of grayscale (useful for tinted metals), apart from that there is little difference between the result from either workflow.

### Texture Suffixes

Suffix | Texture
:------|:-----------------
`_AL`  | Albedo
`_SP`  | Specular
`_R`   | Roughness
`_MT`  | Metallic
`_GL`  | Glossiness
`_N`   | Normal
`_H`   | Height
`_DP`  | Displacement
`_EM`  | Emission
`_AO`  | Ambient Occlusion
`_M`   | Mask

### RGB Masks

It is good practice to use a single texture to combine black and white masks in a single texture split by each RGB channel. Using this, most textures should have:

```
texture_AL.png  # Albedo
texture_N.png   # Normal Map
texture_M.png   # Mask
```

Channel | Spec/Gloss        | Rough/Metal
:-------|:------------------|:-----------
R       | Specularity       | Roughness
G       | Glossiness        | Metallic
B       | Ambient Occlusion | Ambient Occlusion

#### The blue channel can vary depending on the type of material:

 - For character materials use the `B` channel for *subsurface opacity/strength*
 - For anisotropic materials use the `B` channel for the *anisotropic direction map*
 
 ## Configuration Files

File extension: `INI`

Fast and easy to parse, clean and easy to tweak.

`XML`, `JSON`, and `YAML` are also good alternatives, pick one and be consistent.

Use binary file formats for files that should not be changed by the player. For multiplayer games store configuration data on a secure server.

## Localization

File extension: `CSV`

Widely used by localization software, makes it trivial to edit strings using spreadsheets.
