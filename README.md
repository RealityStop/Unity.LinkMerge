Custom Package Link Merger
==========================

If you use Reflexion, Unity could wrongly assume that your assembly is unused and 
[strip your code](https://docs.unity3d.com/Manual/ManagedCodeStripping.html) when
compiling with IL2CPP backend. 

`link.xml` files are ignored when placed in UPM packages 

## Usage

Add a `linkmerge.xml` file at your package root.  
Fill the document with your assemblies

```xml
<linker>
    <assembly fullname="Your.PackageName1.Runtime" preserve="all"/>
    <assembly fullname="Your.PackageName2.Runtime" preserve="all"/>
</linker>
```

If your package is installed via [openupm](https://openupm.com) registry, you 
can add this package as dependency 

```json
// package.json
// ...
"dependencies": {
  "com.realitystop.linkmerge": "1.0.0"
},
// ...
```