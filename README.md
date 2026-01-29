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


Console Bridge (C#)

Target: .NET 8.0
Type: Console Application
Architecture: x64




-- discord: baconroaster23
-- Credits To QuorumAPI
-- Scripts and Everything is on the Repo 
