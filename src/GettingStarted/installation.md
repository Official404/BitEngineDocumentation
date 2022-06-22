# Installation

Currently it is quite easy to install BitEngine
But unfortunately you still have to compile the code by your self because I havent built a working executable you can just donwload.

So for the mement here are the steps to get things going.
<br></br>
## Windows
### Prerequsites:
Befor you start with the instalation you need to have some stuff installed and ready.
- Git
- Visual Studio 2022
- Python

#### Git:
Git can be installed at there [website](https://git-scm.com)
#### Visual Studio 2022:
And the same goes for Visual Studio 2022. It can be installed from there [website](https://visualstudio.microsoft.com). It is important that you install visual studio 2022. any other versions may not work.
There is a fix if you want to run itthru Visual Studio 2019 tho. Read [Installation for Visual Studio 2019](./installation_for_visualstudio2019.md).
#### Python:
THis can be installed thru the Windows Store. Just search for Python and it sould appear (I usually use Python 3.10).

### Github Download:
Start by cloning the reposatory from Github like this.

```bash
git clone [BitEngine Github link here]
```

After that you have to initialise and update the submodules. (This step can be done in the first step by adding ```--recursive``` at the end)

```bash
cd BitEngine
```
```bash
git submodule init
```
```bash
git submodule update
```

### Run setup scripts scripts:

After this navigate to the scripts folder and launche the ```Setup.bat``` file
```bash
cd /Scripts/
```
```bash
./Setup.bat
```

Some problems may occure wile runing the script.
- It may ask you to install vulkan before continuing. Do so and run the script once again after it is done!
- It may get stuck on asking you if you want to install a pakage for python. Press yes and then just press ```Ctrl + C``` and run the script again and it sould work.

### Start Visual Studio
After this press the solution file in the navigate back to the main folder and run the solutions file that has appeared.

```bash
cd ..
```
```bash
./BitEngine.sln
```

After this just press ```F5``` and run the program and it sould build and start.