# Setup

Make sure that the `TinCan/Properties/AssemblyInfo.cs` has been updated with new release version.

    TinCan -> Properties -> Assembly Information

Obtain the `TinCan.NET.pfx` file. This is required for the signed version and can't be included in the GitHub repository due to being public.

# Build

### Option 1 - Build in Visual Studio
Then set the Build Configuration to "Release-net35" and build the solution. (Verify `bin/Release/net35/TinCan.dll` has correct version.)

Repeat the previous step for "Release-net40", "Release-net45" and "Release-net45-signed", verifying the `TinCan.dll` in their respective directory under `bin\Release`.

To create the `nuget` package:

    cd TinCan
    ..\.nuget\nuget pack TinCan.csproj -sym -Prop Configuration=Release-net35
    
Note: Providing a `Configuration` property is mandatory, otherwise `nuget` will build the `Debug` configuration and include that in the package. The `<files>` portion of the `.nuspec` ensures all releases built previously are in the created `nuget` package.

### Option 2 - Build using ant

    ant package

This will build all releases to be included in the `nuget` package and package them into a `.nupkg`.

# Push release

    cd TinCan
    ..\.nuget\nuget push TinCan.(version).nupkg

Commit the updated assembly information file and push to master. Upload the generated `TinCan.(version).nupkg` as a GitHub tag release.
