#DOLBOEB.INJECTOR

As some of you might have heard, the lsass & csrss meme is probably going to be patched in few weeks so i'm releasing this here

How to use:

1) Use proper manualmapper to inject the DOLBOEB.INJECTOR.dll into lsass.exe (Xenos/Blackbone or anything that initializes TLS & SEH/C++ exceptions support)
2) Open up C:\Windows\System32\config\systemprofile\AppData\Roaming, you'll see 2 files there, first one is ntmapper-log.txt, it's a log file, and second one is ntmapper-control.txt, it's a configuration/command file. You have to open up the ntmapper-control.txt and paste the injection configuration in the following format:

TargetProcessName.exe
C:\Path\To\Your\Cheat\Dll.dll
ImportingModule.dll
ExportingModule.dll
ExportedFunc
OpenProcessOrNot (yes - will open the handle / no - will try to find one)
CreateThreadOrNot (yes - will create a new thread / no - will hijack an existing one)
Overwrite module or not (yes - will hollow a legit module in target process, no - will just allocate memory for the DLL)
Wait 10s before injection (yes/no)
Module to overwrite.dll

Once you've saved the configuration file, the injector is gonna start waiting for process and once process arrived it's gonna try injecting.

- STILL WORKS ON MOST BE GAMES
- Manual mapping is pasted from @striekcarl
- Been made in 2 days by me under ton of red bull cans
- x64 only
- Right now it is detected and sigged although it was UD on BE for full five months lmao
- Is sigged to shit and is going to get you banned in one hour
- Has every detection vector an lsass injector can possibly have
- Requires you to provide C++ exception support otherwise it's gonna fuckup the lsass (use Xenos/Blackbone)
- Doesn't copy headers
- Stays in lsass forever and doesn't try to be stealthy at all
- Doesn't initialize TLS & SEH
- Doesn't resolve some imports like D3D ones (D3DCompile for example) - you're gonna get a crash if you'll try injecting working PUBG chams. To fix the issue, use GetProcAddress internally to resolve missing imports
- Just an awful piece of shit, an example how NOT to write an injector

How it works - it basically just manually maps the image into target process using lsass's handle and then just calls the entrypoint via IAT hook (it searches for the exporter-importer-importedfunc chain you've specified then hooks the IAT of specified importing module with a shellcode that simply calls DllMain)

I rewrote it some time ago so my current injector is fast, convinient, stealthy, and doesnt fuckup the imports.

Don't tell me the code is shit because i pretty much know it's shit, i didn't craft it especially to show off on UC so w/e.
