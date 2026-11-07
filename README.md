# AI Trainer V3 updates

This public repository contains signed, compiled update downloads and update-hosting instructions. V3 application project source, personal settings, recordings and credentials are not published here.

## Latest update

[AI Trainer 3.1.61](https://github.com/xgt2010x-a11y/ai-training-updates/releases/tag/v3.1.61) improves optional YOLO-guided recovery when native meter tracking misses short Arrow2 fills. Native tracking continues on every frame; the selected shooting method remains the only release timer. The update also includes cumulative Titan + P5G integration, CV Predictive and local feedback-log improvements.

In an existing V3 installation, open **Updates**, check for updates and download. Choose **Install and restart** when ready. Each computer keeps its own profiles, capture and controller settings, timing values, pairings, recordings and TensorRT configuration.

Version 3.1.61 is a small program-component update for compatible existing V3 installations. Its ZIP is an updater payload, not a standalone fresh installation. It preserves the runtime libraries and models already installed on the PC; it does not bundle trained models or third-party runtimes. A compatible local model is required for optional YOLO assistance. Without one, native meter tracking continues. Separately obtained models and runtimes retain their own license requirements.

Recorded-image and isolated updater tests passed. Those checks do not establish live shooting accuracy on every court.

## Repository contents

Release assets contain the signed `stable.json` manifest and the compiled component ZIP. The Git repository itself contains this README and the update-hosting workflow. GitHub's automatically generated source archives contain those repository files, not the private V3 application project.

[Latest release](https://github.com/xgt2010x-a11y/ai-training-updates/releases/latest)