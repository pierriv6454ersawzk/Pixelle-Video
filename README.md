# Pixelle-Video

A fork of [AIDC-AI/Pixelle-Video](https://github.com/AIDC-AI/Pixelle-Video) — an open-source video generation framework powered by diffusion models.

## Overview

Pixelle-Video provides a flexible pipeline for text-to-video and image-to-video generation using state-of-the-art diffusion-based architectures. This fork includes additional features, optimizations, and quality-of-life improvements over the upstream project.

## Features

- 🎬 **Text-to-Video**: Generate videos from natural language descriptions
- 🖼️ **Image-to-Video**: Animate static images into dynamic video sequences
- ⚡ **Optimized Inference**: Memory-efficient attention and quantization support
- 🧩 **Modular Pipeline**: Easily swap schedulers, encoders, and decoders
- 🐳 **Docker & DevContainer Support**: Reproducible development and deployment environments

## Requirements

- Python 3.10+
- CUDA 11.8+ (for GPU acceleration)
- 24 GB+ VRAM recommended for full-resolution generation

## Installation

### From Source

```bash
git clone https://github.com/your-org/Pixelle-Video.git
cd Pixelle-Video
pip install -e .
```

### With Optional Dependencies

```bash
# Install with all extras (training, evaluation, etc.)
pip install -e ".[all]"

# Install with training support only
pip install -e ".[train]"
```

### Using Docker

```bash
docker build -t pixelle-video .
docker run --gpus all -it pixelle-video
```

## Quick Start

### Text-to-Video

```python
from pixelle_video import PixelleVideoPipeline

pipeline = PixelleVideoPipeline.from_pretrained("pixelle-video/pixelle-video-base")
pipeline = pipeline.to("cuda")

video_frames = pipeline(
    prompt="A serene mountain lake at sunrise with mist rising from the water",
    num_frames=24,
    height=480,
    width=720,
    num_inference_steps=50,
).frames

# Save output
from pixelle_video.utils import export_to_video
export_to_video(video_frames, "output.mp4", fps=8)
```

### Image-to-Video

```python
from pixelle_video import PixelleVideoI2VPipeline
from PIL import Image

pipeline = PixelleVideoI2VPipeline.from_pretrained("pixelle-video/pixelle-video-i2v")
pipeline = pipeline.to("cuda")

image = Image.open("input.jpg")

video_frames = pipeline(
    image=image,
    prompt="The scene comes to life with gentle movement",
    num_frames=24,
).frames
```

## Development

### Using DevContainer (Recommended)

Open this repository in VS Code and select **"Reopen in Container"** when prompted. The devcontainer will automatically set up the full development environment.

### Manual Setup

```bash
pip install -e ".[dev]"
pre-commit install
```

### Running Tests

```bash
pytest tests/ -v
```

### Building Documentation

```bash
mkdocs serve
```

## Project Structure

```
Pixelle-Video/
├── pixelle_video/          # Core library
│   ├── pipelines/          # Inference pipelines
│   ├── models/             # Model architectures
│   ├── schedulers/         # Diffusion schedulers
│   └── utils/              # Utility functions
├── scripts/                # Training & evaluation scripts
├── tests/                  # Unit and integration tests
├── docs/                   # Documentation source
└── examples/               # Example notebooks and scripts
```

## Contributing

Contributions are welcome! Please read our [Contributing Guide](CONTRIBUTING.md) and open a pull request.

## License

This project is licensed under the Apache 2.0 License — see the [LICENSE](LICENSE) file for details.

## Acknowledgements

- Original implementation by [AIDC-AI](https://github.com/AIDC-AI/Pixelle-Video)
- Built on top of [Diffusers](https://github.com/huggingface/diffusers) by Hugging Face
