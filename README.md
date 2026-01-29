# BC-Injection

BridgeCsharp‑Injection

BC‑Injection is a lightweight Batch → C# bridge that allows Batch scripts to trigger C# API functionality through a Console Application.

This project demonstrates a practical method for integrating Batch automation with a C# API that cannot be accessed directly from .bat files.

Overview

Batch scripts cannot directly invoke methods inside C# DLLs.
BC‑Injection solves this by introducing a C# Console Application that acts as a controlled bridge between Batch and the API.

<img width="311" height="160" alt="image" src="https://github.com/user-attachments/assets/148f01a6-4e07-40d2-8148-fdcbeb8bc0cc" />
<img width="671" height="352" alt="image" src="https://github.com/user-attachments/assets/2c8512cf-fd6a-42f2-b91e-af0ae91ac06b" />



The Batch script is responsible only for user interaction and command dispatch.
All logic and API interaction remain in C#.

*Disclaimer: All runtime files must remain in the Data directory.*


Build Configuration (Console Bridge)

# The Console Application must be built with the following settings:

- Framework: .NET 8.0

- Architecture: x64

- Configuration: Release

- Platform Target: x64

- Prefer 32‑bit: Disabled

Incorrect configuration may result in silent failures.

# Functions:
QuorumBridge.exe attach
QuorumBridge.exe attach_state
QuorumBridge.exe state
QuorumBridge.exe exec script.lua


# Console Bridge (C#)

- Target: .NET 8.0
- Type: Console Application
- Architecture: x64

using System;
using System.IO;
using QuorumAPI;
// Please Give Credits To me and For The QuorumAPI 
namespace BCInjection
{
    class Program
    {
        static void Main(string[] args)
        {
            if (args.Length == 0)
                return;

            switch (args[0].ToLower())
            {
                case "autoupdate":
                    QuorumQuorumAPI.AutoUpdate();
                    Console.WriteLine("AutoUpdate completed.");
                    break;

                case "attach":
                    QuorumAPI.AttachAPI();
                    Console.WriteLine("Attach called.");
                    break;

                case "attach_state":
                    int attachResult = QuorumAPI.AttachAPIWithState();
                    Console.WriteLine(attachResult == 1 ? "Attached" : "Attach failed");
                    break;

                case "state":
                    int state = QuorumAPI.GetAttachState();
                    Console.WriteLine(state == 1 ? "Attached" : "Not attached");
                    break;

                case "exec":
                    // Execution currently unreliable (WIP)
                    if (args.Length < 2)
                        return;

                    string script = File.ReadAllText(args[1]);
                    QuorumAPI.ExecuteScript(script);
                    Console.WriteLine("Execution requested.");
                    break;
            }
        }
    }
}


# Keep in mind This is My Batch Script You Could Modify it

@echo off
cd Data
title  Batch Executor QuorumAPI - BaconRoaster
setlocal EnableDelayedExpansion

echo choose with Numbers:
echo 1. Attach
echo 2. Executue Script
set /p Input=Choose:
if %Input% EQU 1 goto attach
if %Input% EQU 2 goto exec
:attach
pause
set /p "script=Type your script: "
> temp.lua echo(!script!
QuasarBridge.exe attach
QuasarBridge.exe exec temp.lua
pause

# Known Limitations

- Script execution is unreliable and may not execute even when reported as successful

- Execution state validation is incomplete

- Single‑line script input only

- These limitations are related to API state handling rather than the bridge logic itself.

# Planned Improvements

- Reliable execution state validation

- Multi‑line script input support

- Improved execution feedback

- Cleaner command handling

- Optional silent/background mode

# Disclaimer

This project is provided for educational and experimental purposes only.
The author assumes no responsibility for misuse.
