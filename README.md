# VB.Net-Lib-PiperTTS
VB.Net Lib - Piper TTS (Text to Speech) Easy to Use Function for Integrating Piper.exe into your WinForms Applications



# PiperTTS - Text to Speech (TTS) with Piper

## Requirements

- .NET Framework 4.7.2 or higher
- NuGet Package: `NAudio 2.2.1`
- NuGet Package: `NAudio.Asio 2.2.1`
- NuGet Package: `NAudio.Core 2.2.1`
- NuGet Package: `NAudio.Midi 2.2.1`
- NuGet Package: `NAudio.Wasapi 2.2.1`
- NuGet Package: `NAudio.WinForms 2.2.1`
- NuGet Package: `NAudio.WinMM 2.2.1`
- [piper.exe](https://github.com/rhasspy/piper/releases) - Download the `piper_windows_amd64.zip` from GitHub releases
- [Piper ONNX voice Model](https://github.com/rhasspy/piper#voices) - Download a voice model you like (e.g., `en_GB-jenny_dioco-medium.onnx`)
- [Piper JSON voice Config](https://github.com/rhasspy/piper#voices) - Download the corresponding JSON config for the chosen ONNX file.

## Installation Instructions

1. **Download Piper Executable:**
   - Download `piper_windows_amd64.zip` from [GitHub releases](https://github.com/rhasspy/piper/releases).

2. **Unzip Piper Files:**
   - In Visual Studio's **Solution Explorer**, create a subfolder called `PiperTTS`.
   - Unzip the contents of `piper_windows_amd64.zip` into the `PiperTTS` folder.

3. **Create Subfolders:**
   - Inside the `PiperTTS` folder, create two subfolders: `VoiceModels` and `WavOutput`.

4. **Download and Place Model Files:**
   - Download a set of `.ONNX` and `.JSON` voice model files (e.g., `en_GB-jenny_dioco-medium.onnx` and `en_GB-jenny_dioco-medium.json`).
   - Place these files inside the `VoiceModels` subfolder.

5. **Include Files in Solution:**
   - At the top of Visual Studio's **Solution Explorer**, click the **Show All Files** icon to reveal the unzipped files.
   - Using **Solution Explorer**, iterate through **every file** and sub-file (including voice model files) and mark all as `Always copy` or `Copy if Newer` in the **Properties** pane.

6. **Update Global Variables (if applicable):**
   - If you renamed the folders in steps 2 and 3, remember to update the following global variables:
     - `PiperDirectory`
     - `modelPath`
     - `configPath`
     - `outputFilePath`

## Description

The **PiperTTS** module provides a highly configurable function for generating speech from text using **PiperTTS** in near real-time. Piper works on low-end hardware, such as a Raspberry Pi 4, and is capable of real-time speech generation with minimal CPU and memory usage. On more powerful hardware, it runs in real-time.

The function works asynchronously, allowing you to either await its completion for synchronous-like behavior or choose not to wait. It avoids blocking the UI thread, enabling smooth user interface interactions.

### Features:
- **Callback Function:** You can pass a callback function to update the UI or trigger notifications once speech generation is complete.
- **Streaming or Wave File Output:** Stream the audio directly to speakers, or output it to a `.wav` file. You can even set it to autoplay the `.wav` file after generation.
- **Text Queueing:** To prevent overloading Piper, the module queues text and processes it in order, ensuring no overlap of audio.
- **Partial Text Streaming:** If text is sent while playback is in progress, it will be queued until Piper is ready to process it. Partial strings (such as from an LLM) are also handled with appropriate pauses.
- **Cancellation Support:** You can cancel ongoing speech synthesis at any time using cancellation tokens.
- **Configurable Speech Parameters:** Adjust speech tempo, sentence gaps, and noise parameters for customization.
- **Force Speech Mode:** The `ForceSpeak` option forces speech processing even for incomplete or small text.

## Example Usage

### Main Function
```vb
' Default function: stream directly to speakers
Await Speak(userInput)
