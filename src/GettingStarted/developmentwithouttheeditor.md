# Development without the editor

It is possible to developt stuff without the editor, you just have to make a new project and setup some stuff. 
<br></br>

### **Download and install the engine**

Start by follow the instructions from the [installations](./installation.md) page and get everything upp and running. Dont worry if you have built the engine. everything will stil work.

### **Make and edit premake file for a new project and run scripts**

Start by making a new folder in the root of the BitEngine folder and name it like ```MyProject```

Navigate in to you folder and make a file called ```premake5.lua```. Now start editing that file and add this in it.

```lua
project "MyProject"
	kind "ConsoleApp"
	language "C++"
	cppdialect "C++17"
	staticruntime "off"
	
	fullOutputDir = "%{wks.location}bin\\" .. outputdir .. "\\%{prj.name}"
	targetdir ("%{wks.location}/bin/" .. outputdir .. "/%{prj.name}")
	objdir ("%{wks.location}/bin-int/" .. outputdir .. "/%{prj.name}")

	files {
		"src/**.h",
		"src/**.cpp"
	}

	includedirs{
		"%{wks.location}/BitEngine/vendor/spdlog/include",
		"%{wks.location}/BitEngine/src",
		"%{wks.location}/BitEngine/vendor",
		"%{IncludeDir.glm}",
		"%{IncludeDir.entt}",
		"%{IncludeDir.yaml_cpp}",
		"%{IncludeDir.imGui}",
		"%{IncludeDir.ImGuizmo}",
	}

	links {
		"BitEngine"
	}

	filter "system:windows"
		systemversion "latest"

		postbuildcommands {
            "xcopy /s /e /q /y /i \"$(SolutionDir)%{prj.name}\\assets\" \"%{fullOutputDir}\\assets\" > nul",
			"xcopy /s /e /q /y /i \"$(SolutionDir)%{prj.name}\\Resources\" \"%{fullOutputDir}\\Resources\" > nul",
        }

	filter "configurations:Debug"
		defines {"BT_DEBUG","BT_ENABLE_ASSERTS"}
		runtime "Debug"
		symbols "on"

	filter "configurations:Release"
		defines "BT_RELEASE"
		runtime "Release"
		optimize "on"

	filter "configurations:Dist"
		defines "BT_DIST"
		runtime "Release"
		optimize "on"
```

Don't forget to edit Line 1 to you folder name (In this cas mine is ```MyProject```)

After this navigate back to the root of BitEngine. Adn start editing the ```premake5.lua``` file in there.

At the top of this file change ```startupproject "BitEngine-Editor"``` to you project name.

```lua
include "./vendor/premake/premake_customization/solution_items.lua"
include "Dependencies.lua"

workspace "BitEngine"
	architecture "x86_64"
	startproject "MyProject"
    ...
```

At the bottom add this to the file

```lua
    ...
	include "BitEngine/vendor/ImGui"
	include "BitEngine/vendor/yaml-cpp"
group ""

include "BitEngine"
include "Sandbox"
include "BitEngine-Editor"
include "MyProject"
```

After all of this navigate to the scripts folder and run the ```Setup.bat``` file once again.

After this is done start the ```BitEngine.sln````file again and you project should be in there without any problems.

### **Make a window appear**

