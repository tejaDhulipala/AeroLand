# AeroLand

**Paper:** [AeroLand: Benchmarking the Aviation Emergency Decision-Making Capabilities of LLMs](LINK_TO_PAPER)

## Run Instructions

Run the benchmark on a model:
```
python evaluation/llm_run.py --model openai/gpt-6-luna --runs 5
```

Any vision-capable model on [OpenRouter](https://openrouter.ai/models) can be used. Pass its model ID to `--model`.

Other useful options:
```
python evaluation/llm_run.py --limit 2 --dry-run   # print the prompts for the first 2 scenarios without calling the API
python evaluation/llm_run.py --help                # list all options
```

Results are saved to `evaluation/results/<model>_<runs>runs_<timestamp>/`:
- `summary.txt`: overall accuracy, accuracy by tag, and accuracy by scenario
- `responses.txt`: every model response for every scenario

## Setup Instructions

Clone the GitHub repo and cd into it:
```
git clone https://github.com/tejaDhulipala/Aviation-Emergencies-Benchmark.git
cd Aviation-Emergencies-Benchmark
```

Create a virtual environment (Python 3.10 or newer):
```
python -m venv venv
source venv/bin/activate        # on Windows: venv\Scripts\activate
```

Install dependencies:
```
pip install -r requirements.txt
```

Create a `.env` file in the repo root with your [OpenRouter API key](https://openrouter.ai/keys):
```
OPENROUTER-KEY=<your key>
```

## Creating Your Own Scenarios

The scenario builder is a graphical tool for making new scenarios. Start it from the repo root:
```
python -m scenario_builder.scenario_gui
```

The scenario builder uses Tkinter. It comes with most Python installs, but on some Linux systems you may need to install it separately (for example, `sudo apt install python3-tk`).

To create a scenario:
1. Enter a location and flight conditions, then click **Render / Refresh Map**.
2. Click on the map to place candidate landing sites and set their landing directions.
3. Right-click any point to see how much altitude the aircraft would lose gliding there.
4. Select the correct answer, add tags and an answer explanation, and export.

Exported scenarios are saved to the `dataset/` folder and are automatically included the next time you run the benchmark.

## Contributing

Contributions are welcome! Some ideas:
- New scenarios, especially for underrepresented categories like farm furrows, obstacles on approach, water landings, and night landings
- Reviews of existing scenarios and their answer explanations
- Results for models that have not been evaluated yet
- Bug fixes and improvements to the scenario builder or evaluation script

Feel free to open an issue or submit a pull request. If you are planning a larger change, please open an issue first so we can discuss it.
