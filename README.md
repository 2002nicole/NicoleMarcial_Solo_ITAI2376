Nicole Marcial

ITAI 2376 - Deep Learning

SPRING 2026

Final Course Project AI Agent

# Cookie Recipe Adaptation Agent

A single AI agent that helps users adapt cookie recipes through ingredient substitutions, batch size changes, dietary adjustments, and texture guidance.

## Problem and Target User
Baking is sensitive to small ingredient and ratio changes, especially in cookies. Beginners often struggle when they need to halve a recipe, replace an ingredient, or adjust for dietary needs without ruining texture, spread, or structure.

This project solves that problem by building a cookie-focused AI agent that helps users adapt common cookie recipes in a more guided and practical way.

**Target user:** beginner or intermediate home bakers who want clearer help making recipe changes.

## Chosen Option
**Option A — Single AI Agent**

I stayed with the single-agent path from my Midterm blueprint. This problem is focused enough that one well-designed agent with retrieval and multiple tools is more appropriate than a multi-agent team.

## Architecture Overview
This project uses a single LangChain-based AI agent that reads a user’s cookie-related request, reasons about what kind of adaptation is needed, uses the appropriate tool(s), and returns a grounded response.

The system supports:
- cookie recipe retrieval
- ingredient scaling
- substitution guidance
- full recipe adaptation

The agent also uses a small cookie baking knowledge base and retrieval-augmented generation (RAG) to ground some of its baking guidance in external reference material instead of relying only on general language-model knowledge.

### Architecture Diagram


### How the Agent Works
1. The user gives a cookie-related request.
2. The agent interprets the request and decides what kind of action is needed.
3. The agent uses one or more custom tools:
   - recipe retrieval
   - ingredient scaling
   - substitution guidance
   - recipe adaptation
4. The agent reads the tool output and produces a final beginner-friendly response.
5. If the request is outside the project scope, the agent redirects or refuses gracefully.

## Frameworks and Tools Used

### Framework
- **LangChain** — used to define tools and build the single-agent workflow

### LLM Provider
- **OpenAI** — used as the language model provider for the agent

### Retrieval / Knowledge
- **SentenceTransformers embeddings**
- **FAISS vector store**
- small custom cookie baking knowledge base
- filtered cookie recipe dataset

### Custom Tools
- **Recipe Retrieval Tool** — retrieves relevant cookie recipe or baking guidance context
- **Ingredient Scaling Tool** — scales recipe ingredient amounts based on desired servings
- **Substitution Guidance Tool** — suggests ingredient replacements and explains likely effects
- **Recipe Adaptation Tool** — adapts a full cookie recipe for requests like egg-free or butter replacement

### Interface
- **Google Colab notebook** for development and execution
- **Gradio** as an optional user-facing interface

## Data Sources
This project uses a filtered cookie-focused dataset derived from Food.com recipes available through Kaggle, along with a small baking knowledge base created from summarized baking references.

Because some source datasets are large and/or third-party hosted, the full raw dataset is not redistributed in this repository. See the `data/` folder and notes below for how the project data was prepared.

### Main Sources
- Food.com recipe dataset from Kaggle
- cookie baking knowledge notes summarized from baking references such as King Arthur Baking

## Installation

### Python Version
This project was developed in **Python 3.11+** in Google Colab.

### Install Dependencies
```bash
pip install -r requirements.txt
```

### Environment Variables
Create a `.env` file based on `.env.example` and add your API key(s).

Example:
```env
OPENAI_API_KEY=your_key_here
```

## How to Run the Agent

### Notebook Version
Open **`agent.ipynb`** and run the notebook from top to bottom.

Recommended order:
- Sections 1–5: data prep, knowledge base, retrieval setup
- Section 6: custom tools
- Section 7: LangChain agent setup
- Section 8: real-world scenario testing
- Section 9: optional Gradio interface
- Section 10: final notes and limitations

### Optional Gradio Interface
If you want the notebook to launch the optional interface, run the Gradio section near the end of the notebook.

## Example Usage

### Example 1 — Butter substitution
**Input**
```text
What can I use instead of butter in cookies?
```

**Output Summary**
The agent suggests options such as coconut oil or plant-based butter and explains that spread, flavor, and texture may change.

### Example 2 — Egg-free recipe adaptation
**Input**
```text
Make this cookie recipe egg-free:

1 cup salted butter softened
1 cup granulated sugar
1 cup light brown sugar packed
2 teaspoons pure vanilla extract
2 large eggs
3 cups all-purpose flour
1 teaspoon baking soda
1/2 teaspoon baking powder
1 teaspoon sea salt
2 cups chocolate chips
```

**Output Summary**
The agent identifies the eggs, suggests replacements such as flax egg or applesauce, and explains likely effects on structure and texture.

### Example 3 — Batch scaling
**Input**
```text
Scale this cookie recipe from 24 servings to 12 servings.

Recipe ingredients:
1 cup butter | 1/2 cup brown sugar | 2 cups flour | 1 egg | 1 tsp vanilla
```

**Output Summary**
The agent scales the ingredient quantities proportionally and returns a smaller-batch ingredient list.

## Known Limitations
- The current version works best with **self-contained prompts**. It is more reliable when the recipe or full request is included in the same message.
- Follow-up questions without repeated context may be treated as a new request instead of a continuation of the prior one.
- The agent is intentionally limited to **cookie recipes only**.
- Substitution guidance is practical but not perfect. Real baking outcomes may still vary based on ingredient brand, dough temperature, measuring accuracy, and oven behavior.
- The baking knowledge base is intentionally small and focused, not a complete baking encyclopedia.

## Demo Video
[Insert demo link here]

## Repository Contents
- `agent.ipynb` — main notebook implementation
- `requirements.txt` — project dependencies
- `.env.example` — template for environment variables
- `.gitignore` — excluded files
- `docs/architecture.png` — architecture diagram
- `demo/` or external link — demo video
- `data/` — sample knowledge base / supporting project data
- `REFLECTION.md` — final reflection document

## Midterm-to-Final Continuity
This final project follows the core direction of my Midterm blueprint: a focused single AI agent for cookie recipe adaptation using a transformer-based language model, retrieval, and custom tools.

## References
- Food.com recipe datasets via Kaggle
- King Arthur Baking references used for summarized cookie baking guidance
