# Murf Python SDK

![Murf AI Logo](https://murf.ai/public-assets/home/Murf_Logo.png)

[![fern shield](https://img.shields.io/badge/%F0%9F%8C%BF-Built%20with%20Fern-brightgreen)](https://buildwithfern.com?utm_source=github&utm_medium=github&utm_campaign=readme&utm_source=https%3A%2F%2Fgithub.com%2Fmurf-ai%2Fmurf-python-sdk)
[![pypi](https://img.shields.io/pypi/v/murf)](https://pypi.python.org/pypi/murf)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/gist/devgeetech-murf/bbe2c7eb01433f4a151f0fd2be23b1c8/murf-python-sdk.ipynb)

## Table of Contents

- [Overview](#overview)
- [Installation](#installation)
- [Getting Started](#getting-started)
- [Features](#features)
- [Asynchronous Usage](#asynchronous-usage)
- [Error Handling](#error-handling)
- [Advanced Configuration](#advanced-configuration)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

The Murf Python SDK offers seamless integration with the [Murf AI](https://murf.ai/) [text-to-speech software](https://murf.ai/text-to-speech), enabling developers and creators to convert text into lifelike speech effortlessly. With over 130 natural-sounding voices across 13+ languages and 20+ speaking styles, Murf provides unparalleled speech customization for a wide range of applications. The SDK is designed for both synchronous and asynchronous workflows, featuring robust error handling, advanced configuration options, and support for real-time applications.

---

## Installation

Check out the [HTTP API documentation](https://murf.ai/api/docs/introduction/quickstart).

Install the SDK using pip:

```bash
pip install murf
```

---

## Getting Started

Here's a quick example to get you started with the Murf SDK:

```python
from murf import Murf

# Initialize the client with your API key
client = Murf(api_key="YOUR_API_KEY")

# Generate speech from text
audio = client.text_to_speech.generate(
    format="MP3",
    sample_rate=44100.0,
    text="Hello, world!",
    voice_id="en-US-natalie",
)

# Save the audio to a file
with open("output.mp3", "wb") as f:
    f.write(audio)
```

For more detailed information, refer to the [official documentation](https://murf.ai/api/docs/introduction/quickstart).

---

## Features

- **Text-to-Speech Conversion:** Transform text into natural-sounding speech.
- **Multilingual Support:** Access voices in over 13 languages, including English, French, German, Spanish, Italian, Hindi, Portuguese, Dutch, Korean, Chinese (Mandarin), Bengali, Tamil, and Polish.

![Murf AI Languages](https://murf.ai/public-assets/home/Murf_Lang.png)

- **Multiple Voice Styles:** Choose from 20+ speaking styles to suit your application's needs.
- **Advanced Voice Customization:** Adjust parameters like pitch, speed, pauses, and pronunciation for optimal output. Fine-grained controls let you tailor the voice output to match your specific requirements.
- **Multiple Audio Formats:** Generate audio in various formats (e.g., MP3, WAV) with configurable sample rates for optimal quality.
- **Real-Time Processing:** Benefit from asynchronous API calls that support non-blocking, real-time audio generation and streaming scenarios.


---

## Asynchronous Usage

The SDK supports asynchronous operations for non-blocking requests:

```python
import asyncio
from murf import AsyncMurf

# Initialize the async client
client = AsyncMurf(api_key="YOUR_API_KEY")

async def main():
    audio = await client.text_to_speech.generate(
        format="MP3",
        sample_rate=44100.0,
        text="Hello, world!",
        voice_id="en-US-natalie",
    )
    # Save the audio to a file
    with open("output_async.mp3", "wb") as f:
        f.write(audio)

# Run the async function
asyncio.run(main())
```

---

## Error Handling

Handle exceptions gracefully to ensure robust applications:

```python
from murf.core.api_error import ApiError

try:
    client.text_to_speech.generate(
        format="MP3",
        sample_rate=44100.0,
        text="Hello, world!",
        voice_id="en-US-natalie",
    )
except ApiError as e:
    print(f"Error: {e.status_code} - {e.body}")
```

---

## Advanced Configuration

### Retry Mechanism

Configure automatic retries for transient errors:

```python
client.text_to_speech.generate(
    format="MP3",
    sample_rate=44100.0,
    text="Hello, world!",
    voice_id="en-US-natalie",
    request_options={"max_retries": 3},
)
```

### Timeout Settings

Set client-wide and per-request timeouts:

```python
# Set a client-wide timeout
client = Murf(api_key="YOUR_API_KEY", timeout=30.0)

# Override timeout for a specific request
client.text_to_speech.generate(
    format="MP3",
    sample_rate=44100.0,
    text="Hello, world!",
    voice_id="en-US-natalie",
    request_options={"timeout_in_seconds": 10},
)
```

### Custom HTTP Client

Integrate a custom HTTP client for advanced use cases:

```python
import httpx
from murf import Murf

# Create a custom HTTPX client
custom_httpx_client = httpx.Client(
    proxies="http://my.proxy.server",
    transport=httpx.HTTPTransport(local_address="0.0.0.0"),
)

# Initialize the Murf client with the custom HTTPX client
client = Murf(api_key="YOUR_API_KEY", httpx_client=custom_httpx_client)
```

---

## Contributing

We welcome contributions to enhance the Murf Python SDK. Please note that this library is generated programmatically, so direct modifications may be overwritten. We suggest opening an issue first to discuss your ideas or improvements. Contributions to the documentation are especially appreciated! For any support queries email to support@murf.ai 

---

## License

Murf Python SDK is released under the [MIT License](LICENSE).

---
