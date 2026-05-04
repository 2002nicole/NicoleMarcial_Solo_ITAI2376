# Cookie Recipe Adaptation Agent

A single AI agent that helps users adapt cookie recipes through ingredient substitutions, batch size changes, dietary adjustments, and texture guidance.

## Solo Project - Nicole Marcial

ITAI 2376 - Deep Learning

SPRING 2026

Final Course Project AI Agent


## Problem and Target User
Baking is sensitive to small ingredient and ratio changes, especially in cookies. Beginners often struggle when they need to halve a recipe, replace an ingredient, or adjust for dietary needs without ruining texture, spread, or structure.

This project solves that problem by building a cookie-focused AI agent that helps users adapt common cookie recipes in a more guided and practical way.

**Target user:** beginner or intermediate home bakers who want clearer help making recipe changes based on their needs.

## Chosen Option
**Option A — Single AI Agent**

I stayed with the single-agent path from my Midterm blueprint. This problem is focused enough that one well-designed agent with retrieval and multiple tools is more appropriate than a multi-agent team.

## Architecture Overview
This project uses a single LangChain-based AI agent designed specifically for cookie recipe adaptation. The agent takes cookied-related user request, reassons about what kind of help is needed, chooses the most appropiate custom tool, reads the tool ouput, and returns a beginner-friendly respone.

The system has three main layers:

1. It uses a filtered cookie recipe dataset together with a small cookie baking knowledge base. These text sources are converted into LangChain documents, split into chunks, embedded with the Hugging Face sentence-transformer model, and stored in a local Chroma vector database. This creates the retrieval-augmented generation (RAG) so the agent can pull in recipe and baking context instead of relying only on general model knoweldge.
2. The project definess custom tools for the main cookie-adaptation tasks. The recipe retrieval tools pulls relevant recipe and baking guidance from the retriever. The ingredient scaling tool rescales ingredient quantities when the user changes batch size. The subsitution guidance tool suggests cookie-friendly replacements and explains likely effects on texture, spead, flavor, structure, or moisture. The recipe adaptaion tool adapts a full cookie recipe based on requests.
3. The LangChain agent uses OpenAI's reasoning engine. The agent inteprets the user's request, decides whhich tool should be used, observes the returned result, and then produces the final answer. The project is intentionally limited to cookie recipes only so the agent stays focused and more reliable for the final build.


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

### Embeddings and Retrieval
- **Hugging Face Embeddings** — used for local text embeddings
- **Embedding model:** `sentence-transformers/all-MiniLM-L6-v2`
- **Chroma** — used as the local vector store for recipe and baking knowledge retrieval
- **LangChain Retriever** — used to retrieve the most relevant recipe and knowledge-base chunks for the agent


### Custom Tools
- **Recipe Retrieval Tool** — retrieves relevant cookie recipe or baking guidance context
- **Ingredient Scaling Tool** — scales recipe ingredient amounts based on desired servings
- **Substitution Guidance Tool** — suggests ingredient replacements and explains likely effects
- **Recipe Adaptation Tool** — adapts a full cookie recipe for requests like egg-free or butter replacement

### Interface
- **Google Colab notebook** for development and execution
- **Gradio** as an optional user-facing interface

## Data Sources

This project uses a filtered cookie-focused recipe dataset and a small summarized baking knowledge base.

### Recipe Dataset
- Food.com recipe dataset from Kaggle
- Used to retrieve cookie recipe examples and ingredient patterns
- The raw full dataset is not fully redistributed in this repository. To reproduce the dataset setup, download it from the original Kaggle source(s):

  - [Food.com Recipes with Ingredients and Tags (Kaggle)](https://www.kaggle.com/datasets/realalexanderwei/food-com-recipes-with-ingredients-and-tags)

### Baking Knowledge References
The cookie baking knowledge base in this project was manually summarized from baking references and paraphrased into short project notes.

Main references:
- [King Arthur Baking — Cookie chemistry](https://www.kingarthurbaking.com/blog/2016/03/14/cookie-chemistry-2)
- [King Arthur Baking — No eggs? Here's your guide for substituting eggs](https://www.kingarthurbaking.com/blog/2021/01/21/guide-for-substituting-eggs-best-egg-replacers)
- [King Arthur Baking — Chilling cookie dough: Does it make a difference?](https://www.kingarthurbaking.com/blog/2015/05/17/chilling-cookie-dough)
- [King Arthur Baking — Why are my cookies spreading?](https://www.kingarthurbaking.com/blog/2023/12/19/why-are-my-cookies-spreading)

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
[]

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

## Deep Learning Connection
This projects applies several deep learning concepts from ITAI 2376. The agent uses as transformer-based language model because the task is entirely text based and must understand user requests, interpet recipe text, and generate updated cookie guidance. This connects expecially to Module 05 where transformers and attention are used to model language context.

The project also uses embeddings and RAG (retrieval-augmented generation). Recipes and baking knowledge are converted into embeddings, stored in a vector database, and retrieved when the agent needs relevant context. This connects to Module 10, which explains how embeddings and RAG help agents ground their answers in external knowledge instead of relying only on model memory.

Finally, the project reflects the course's agent design modules because it combines an LLM w/ retrieval, custom tools, and a tool using reasoning workflow. The agent interprets the request, chooses a tool, reads the result, and then produces a final respose. That matches the single-agent design approach discussed in Module 09 and 10.

