
# Vulkan Pipeline Interceptor Framework

This repository contains the source project for a basic [Vulkan layer](https://www.khronos.org/registry/vulkan/specs/1.3/html/vkspec.html#layers) framework that can be adapted for custom rendering pipelines.

More about [Vulkan](https://www.khronos.org/registry/vulkan/specs/1.3/html/vkspec.html) and the [Vulkan Loader](https://www.khronos.org/registry/vulkan/specs/1.3/loader.html).

Prerequisites:

- Visual Studio 2022 or above;
- Conan package manager (installed via command line or Visual Studio Installer);
- Python 3.10+ interpreter (installed via Visual Studio Installer or externally available in your PATH).

Customization:

- Find documentation and tutorials on the [wiki](https://github.com/vulkan-dev-tools/layer-intercept/wiki);
- Find the sample code from the tutorials in the [example branches](https://github.com/vulkan-dev-tools/layer-intercept/branches/all?query=samples%2F).

DISCLAIMER: This software is distributed as-is, without any warranties or conditions of any kind. Use at your own risks.

---

# Vulkan Viewport Calibration

**DISCLAIMER: This software is distributed as-is, without any warranties or conditions of any kind. Use at your own risks!**

Version: 0.3.2

**This document contains instructions on how to use Vulkan viewport calibration [layer](https://www.khronos.org/registry/vulkan/specs/1.3/html/vkspec.html#layers).**

## Purpose

The camera positioning within your virtual environment when running 3D applications is a fundamental aspect of spatial accuracy. Most GPU-accelerated applications offer basic viewport reset functionality, though few provide the granular control needed for precise alignment with physical hardware setups.

Vulkan Viewport Calibration (VVC) provides millimeter-level translation adjustment and sub-degree rotation precision on all three axes. Configurations can be persisted across sessions for reproducible camera positioning.

Limitations:

- The viewport calibration layer targets Windows 64-bit exclusively.
- The software functions only with applications utilizing Vulkan rendering pipeline.

## Contact

On explicit user request you can support development via [Open Collective](https://opencollective.com/vk-calibration)

## Installation

### Run installer executable

Execute the installation binary `Setup_Vulkan-ViewportCalibration_<version>.exe` and follow the prompts.

Installation notes:
- Deploying to a subdirectory under `program files` ensures compatibility with GPU driver injection mechanisms.
- Administrator privileges required during installation.
- Installation logs available at `%TEMP%\Install Log <yyyy-mm-dd xxx>.txt` for troubleshooting.

### Optional: Confirm correct installation

Verification using [Vulkan Configurator](https://vulkan.lunarg.com/):
- Install Vulkan Configurator
- Launch GPU control panel software (e.g. NVIDIA Control Panel, AMD Radeon Software)
- Navigate to `Layers` tab
- Verify presence of `VK_LAYER_VKTOOLS_viewport_calibration` with version `v3`

### Update

Download latest installer from [release page](https://github.com/vulkan-dev-tools/viewport-calibration/releases). Directory changes require prior uninstallation.

### Uninstall

Remove via Windows Settings/Control Panel standard procedure. Option provided during uninstall to retain or purge AppData configurations.

## How to use

Initial setup requires 4 configuration steps:
1. **adapt configuration parameters:** Define keyboard binding matching your application's viewport reset command.
2. **establish reference position:** Numeric keypad shortcuts require NumLock activation.
3. **invoke calibration via shortcut:** Apply reference position using `execute` shortcut (NumPad 5 by default).
4. **persist reference configuration:** Save satisfactory positions to configuration file for session persistence.

## Configuration

Configuration files located at `...\Users\*<Username>*\AppData\Local\Vulkan-ViewportCalibration\`.

Default configuration file `Vulkan-ViewportCalibration.toml` created on initial installation.

### Configuration sections

- `[startup]`: control layer behavior on application initialization
- `[output]`: application interaction binding
- `[input]`: layer interaction bindings
- `[reference]`: stored reference position loaded on startup

## Logging

Layer writes operational logs to `...\Users\<Username>\AppData\Local\Vulkan-ViewportCalibration\Vulkan-ViewportCalibration.log`.

For reproducible issues, leverage Windows Performance Recorder (WPR) with profile `tools\Trace_Vulkan-ViewportCalibration.wprp` for detailed diagnostics.

[Trace logging documentation](https://docs.microsoft.com/en-us/windows/win32/tracelogging/trace-logging-portal)

