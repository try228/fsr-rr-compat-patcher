# FSR RR Compatibility Patcher

A small utility for applying a local compatibility patch to `amd_fidelityfx_denoiser_dx12.dll` used by AMD FidelityFX Ray Regeneration (RR).

The patch is intended for testing RR 1.1 and 1.2 on hardware/configurations where the original runtime compatibility check prevents initialization.

This project **does not redistribute AMD binaries**. The patcher operates on a locally supplied copy of `amd_fidelityfx_denoiser_dx12.dll`.

## Supported RR versions

* **RR 1.2** — patch required
* **RR 1.1** — patch required
* **RR 1.0** — patch not required

### RR 1.0 testing

I currently need a **compiled sample/application containing RR 1.0** from **FSR SDK 2.1.0 or 2.1.1** for testing and verification.

If you have a compiled RR 1.0 sample from either SDK version, please open an **Issue** and provide it there, preferably together with the SDK version and relevant build information.

The SDK itself is **not required for end users of this patcher**.

## Requirements

For testing RR on RDNA 3, you will need:

* A patched VKD3D-Proton build:
  **[patched VKD3D-Proton build](https://github.com/try228/vkd3d-proton-FSR_RR/releases/tag/FSR_RR_on_RDNA_3)**
* `dxgi.dll` from DXVK:
  **[DXVK](https://github.com/doitsujin/dxvk/releases)**
* Your own copy of `amd_fidelityfx_denoiser_dx12.dll`

## Applying the patch

Place the patcher in the same directory as:

```text
amd_fidelityfx_denoiser_dx12.dll
```

Then run the patcher from that directory:

```bash
./patch_rr
```

The patcher modifies the local DLL in place.

**Make a backup of the original DLL before applying the patch.**

## Running RR on RDNA 3

When launching an application using RR on RDNA 3 with the patched VKD3D-Proton build, set:

```bash
DXIL_SPIRV_CONFIG=wmma_rdna3_workaround
```

For example:

```bash
DXIL_SPIRV_CONFIG=wmma_rdna3_workaround ./your-application
```

The environment variable is **not required when running the patcher**. It is used by the DXIL-to-SPIR-V translation path when running the RR application on RDNA 3.

You will also need the patched VKD3D-Proton build and the required `dxgi.dll` from DXVK in the application's environment.

### Example directory

```text
test/
├── fsr-rr-patcher
├── amd_fidelityfx_denoiser_dx12.dll
├── dxgi.dll
└── ...
```

## Scope

This project is intended as an unofficial compatibility and testing tool for FidelityFX Ray Regeneration.

It does not redistribute AMD's SDK, runtime DLLs, samples, or other proprietary binaries.

Users are expected to provide their own copies of the required files.

## Disclaimer

This project is not affiliated with, endorsed by, or sponsored by AMD.

The patcher modifies a locally supplied third-party binary. Use it at your own risk and keep an unmodified copy of the original DLL for restoration.
