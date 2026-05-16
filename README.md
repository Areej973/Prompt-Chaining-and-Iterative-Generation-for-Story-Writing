# Prompt Chaining and Iterative Generation for Story Writing

This repository contains a Python-based automation pipeline designed to generate long-form, structured stories using Google's Gemini models via the official `google-genai` SDK. By leveraging a prompt-chaining strategy and an automated feedback loop, the system bypasses traditional output length limitations to craft well-paced, cohesive narratives.

## Features

- **Prompt Chaining:** Systematically breaks down the creative process into logical steps: premise generation, structural outlining, initial drafting, and contextual continuation.
- **Stateful Memory Management:** Feeds previous outputs (premise, outline, and accumulated draft) back into subsequent API requests to maintain narrative consistency and prevent repetitive plots.
- **Automated Continuation Loop:** Continuously expands the story until the model autonomously decides to conclude the narrative by emitting a specific termination token (`IAMDONE`).
- **Token Analytics:** Utilizes the API token counter to measure the exact size of the final generated text against model constraints.

## Prerequisites

- Python 3.10 or higher
- A Google Gemini API Key
- Google Colab (Recommended environment for execution)

## Installation

Install the required official Google GenAI SDK:

pip install google-genai

## Setup and Configuration

    API Key Configuration: If running in Google Colab, add your Gemini API key to the notebook Secrets tab with the key name GOOGLE_API_KEY.

    Model Selection: The pipeline defaults to gemini-2.5-flash-lite, which offers a balance of speed and efficiency for iterative generation. You can switch to other supported models (such as gemini-2.5-flash or gemini-2.5-pro) within the script.

## Core Pipeline Architecture
#### Phase 1: Initialization

The environment loads required dependencies, retrieves the API key securely via userdata, and initializes the unified genai.Client.
#### Phase 2: Premise and Outline Generation

    The model generates a central narrative idea (premise) based on an initial prompt.

    The premise is injected into a structural template to produce a chronological blueprint (outline) containing chapters or milestones.

#### Phase 3: The Iterative Loop

    The model writes the first section (starting_draft).

    A while loop begins execution. In each iteration, the complete history is passed to the continuation_prompt.

    The loop appends new content to the master draft and only terminates when the string IAMDONE is detected in the response.

#### Phase 4: Post-Processing and Analytics

    The control token IAMDONE is programmatically stripped from the text.

    The final narrative is formatted using pretty-print (pprint).

    The client.models.count_tokens method evaluates the total token footprint of the output.

## Usage

Run the cells sequentially in your notebook environment. The final output will display the complete, uninterrupted story followed by the total token count metric.

## License

This project is open-source and available under the MIT License.
