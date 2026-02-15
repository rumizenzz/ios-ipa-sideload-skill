---
name: ios-ipa-sideload
description: "Autonomously sideloads iOS apps (.ipa files) onto an iPhone or iPad. Use this skill when a user wants to install an iOS application that is unavailable in their region's App Store, such as Douyin or other region-locked apps. It handles finding the IPA file from trusted sources, guiding the user through the installation with Sideloadly, and completing the on-device trust process."
---

# iOS IPA Sideloader

## Overview

This skill provides a fully autonomous, guided workflow for installing iOS applications from outside the official App Store, a process known as "sideloading." It is designed to be simple and safe, handling the technical complexities while prompting the user only for necessary physical actions (like plugging in their device) or confirmations. The primary workflow uses Sideloadly, a popular and reliable tool for this purpose.

## Agentic Contract: Autonomous & User-Guided

This skill operates with a high degree of autonomy to simplify a complex process. Here is the contract:

- **One-Shot Intake**: The skill will ask for all necessary information upfront (e.g., the app you want to install).
- **Autonomous Execution**: It will then perform all possible steps on its own, including finding the correct IPA file, downloading it, and preparing for installation.
- **Guided Physical Actions**: The skill will pause and provide clear, simple instructions when a physical action is required from you. This includes:
    - Plugging your iPhone into your computer.
    - Tapping "Trust" on your device.
    - Confirming your Apple ID credentials for the signing process.
- **Secure Credential Handling**: If you choose to cache your Apple ID, it will be stored securely using the native OS keychain (Windows DPAPI or macOS Keychain). It is only ever sent to Apple for the app signing process.
- **Success Definition**: The skill's job is complete when the requested application is successfully installed on your device, the developer profile is trusted, and the app is ready to be opened.

## Workflow

The skill follows a structured, multi-phase process to ensure a successful and safe installation.

### Phase 1: Pre-Flight Check & Setup

1.  **Platform Detection**: The skill first determines whether you are running on Windows or macOS to provide the correct instructions and execute the appropriate commands.
2.  **Prerequisite Verification**: It checks for the necessary software:
    - **Sideloadly**: The core tool for installation. If not found, the skill will guide you to [sideloadly.io](https://sideloadly.io) to download and install it.
    - **iTunes/Finder**: Required for the computer to communicate with the iPhone. The skill will ensure the "Sync with this iPhone over Wi-Fi" (Windows) or "Show this iPhone when on Wi-Fi" (Mac) setting is enabled.

### Phase 2: IPA Acquisition

1.  **Trusted Source Search**: The skill will search for the requested application's `.ipa` file on **Decrypt.day**, which is the designated trusted source for clean, decrypted IPAs.
2.  **File Validation**: Before downloading, the skill verifies the file's integrity by checking its **Bundle ID** and **file size** against known good values to avoid scams or malicious files.
3.  **Secure Download**: The IPA file is downloaded to a temporary, secure location in the sandbox environment.

### Phase 3: Sideloading via Sideloadly

1.  **Device Connection Prompt**: The skill will pause and ask you to connect your iPhone to your computer using a USB cable.
2.  **Apple ID Prompt**: It will then ask for your Apple ID email. This is required by Sideloadly to "sign" the app, which is a standard part of the process that makes your iPhone trust the installation. You will be asked if you want to cache the credentials for future use.
3.  **Automated Installation**: The skill will then programmatically execute Sideloadly, passing the downloaded `.ipa` file and your Apple ID to begin the installation.

### Phase 4: On-Device Trust

1.  **Trust Prompt**: After Sideloadly completes, the app icon will appear on your iPhone's home screen, but it will not open yet. The skill will pause again and provide simple, illustrated instructions for the final step.
2.  **Guided Trust Process**: It will guide you to navigate to **Settings > General > VPN & Device Management** on your iPhone, where you will see your Apple ID listed as a "Developer App." You will be instructed to tap on it and then tap "Trust."

### Phase 5: Completion & Cleanup

1.  **Success Confirmation**: The skill will ask you to confirm that the app now opens successfully on your device.
2.  **7-Day Rule Explanation**: It will provide a clear explanation of the 7-day signing limit for free Apple IDs and instruct you on how to easily "refresh" the app once a week by simply re-running the skill or connecting your phone and running Sideloadly again.
3.  **Cleanup**: The temporary IPA file is securely deleted from the sandbox.

## Critical Constraints

- This skill will **never** ask for your Apple ID password directly in the chat. Secure password entry will be handled by the Sideloadly application or a secure OS-level prompt.
- The skill will only download IPAs from the pre-vetted source (Decrypt.day) to minimize security risks.
- The user is responsible for understanding the potential risks of sideloading applications and for the apps they choose to install.
