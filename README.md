# Custom Package Link Merger
==========================

## Overview
Unity employs aggressive stripping when compiling for mobile devices and the web 
[strip your code](https://docs.unity3d.com/Manual/ManagedCodeStripping.html), which can cause assemblies that are only referenced via reflection to be stripped from the build output.

Additionally, `link.xml` files are ignored when placed in UPM package assemblies, preventing the easiest solution.

This repo contains a build script that can be added to your packages that will inject a custom `linkmerge.xml` file from your package into the project temporarily during the build process.  In this way, package-based assemblies can signal to Unity that they should not be stripped.

The script is multi-instance safe, with all `linkmerge.xml` files being merged together into a single link.xml, regardless of how many packages reference the build script.


## Usage

Add a `linkmerge.xml` file at your package root.  
Fill the document with your assemblies

```xml
<linker>
    <assembly fullname="Your.PackageName1.Runtime" preserve="all"/>
    <assembly fullname="Your.PackageName2.Runtime" preserve="all"/>
</linker>
```

And add the BuildHelper.cs file to your Editor asmdef.  **You're good to go!**



Alternatively, if your package is installed via the [openupm](https://openupm.com) registry, you 
can add this package as dependency with the following:

```json
// package.json
// ...
"dependencies": {
  "com.realitystop.linkmerge": "1.0.0"
},
// ...
```
