# TestingEvaluationText-to-PASSModelGenerator

This repository contains the source code, prompts, reference models, and generated outputs for the Bachelor's Thesis: **Rigorous Testing and Evaluation of a Text-to-PASS Model Generator**.

It extends the original Text-to-Pass generator (see [original repository](https://github.com/I2PM/Text-to-PASS-Model-Generator)) with an optimized prompt configuration, and model selection.


 ## Repository Structure

 This repository has the following structure:  
```text
LLMs-For-Subject-Oriented-ProcessModeling/  
├── Outputs/                                # Outputs of the original master's thesis
│   ├── Thesis_Illustrations/                 # Full-size vector graphics
│   ├── CoT/                                  # CoT visualizations  
│   ├── OWL/                                  # OWL visualizations  
│   ├── OneShotPrompting/                     # OneShotPrompting visualizations  
│   └── ZeroShotPrompting/                    # ZeroShotPrompting visualizations
├── ReferenceModels/                        # Manually created reference PASS models used for the evaluation
│   ├── OWL                                   # Reference models in OWL format
│   └── VSDX                                  # Reference models as diagrams
├── src/                                    # Source code (all scripts)
│   ├── CoT/
│   ├── GUI/                                  # GUI notebooks
│   │   ├── GUI-Interactive/                    # Final Web-based human-in-the-loop interactive GUI notebooks
│   │   │   ├── Gemma/                      
│   │   │   ├── GPT/
│   │   │   ├── Llama/
│   │   │   └── Mistral-Small
│   │   ├── Llama/                            # Original Llama notebook (non-interactive)
│   │   └── Mistral-Small/                    # Original Mistral notebook (non-interactive)
│   ├── OWL/ 
│   ├── OneShotPrompting/
│   └── ZeroShotPrompting/ 
├── README.md                               # This file  
└── Requirements.txt                        # Python dependencies

```
### Final System Configuration
The optimized system configuration identified in this thesis consists of:
- **LLM**: gpt-oss-120b
- **Prompting Strategy**: One-shot prompting
- **Temperature**: 0.2

This configuration is implemented in the `GUI-Interactive/GPT/gpt-oss-Interactive-OneShot_.ipynb` notebook.

### Reference Models
Manually created reference PASS models all used test processes are available in the `ReferenceModels/` folder, both in OWL and VSDX format. These models served as ground truth for the structural evaluation conducted in this thesis.


### Model-Specific Folders  

- **Llama:** Contains code used for experiments with Llama model. Experiments are organized by prompting strategy: zero-shot, one-shot, and chain-of-thought.    

- **Mistral-Small:** Contains code used for experiments with Mistral-Small model. Experiments are organized by prompting strategy: zero-shot, one-shot, and chain-of-thought.   

> The variable `model` in each notebook determines which model is used in the notebook. You can change it to your preferred model (e.g., `"mistral-small"`).
 
### Installation

Clone the repository and install dependencies:

```bash
git clone https://github.com/shadiamanan/LLMs-For-Subject-Oriented-ProcessModeling.git  
cd LLMs-For-Subject-Oriented-ProcessModeling  
pip install -r Requirements.txt

```

## Configuration

Before running the notebooks, configure your API key and preferred model.

```python

from openai import OpenAI

api_key = "YOUR_API_KEY"
model = "Llama-3.3-70B"  # change to your preferred model
client = OpenAI(api_key=api_key, base_url=base_url)

```

### **Model Usage Notes**

**Mistral**: Best for linear simple scenarios.  
Responses may be truncated if the context window is exceeded.  

**Llama**: Recommended for complex scenarios requiring decision flows and longer context window.  

### File Paths
The notebooks reference local directories for saving diagrams or files (e.g., `E:\Thesis\PASS Diagrams\Diagram\llama`).    

To run the notebooks, you can either:    
1. Create a folder structure on your local machine where the outputs will be saved, **or**  
2. Update the path variables in the notebooks to match a directory of your choice.

### Running the GUI in Jupyter Notebook
The repository provides a **web-based, human-in-the-loop interactive GUI** for exploring different LLMs in process modeling.

### Steps to launch

Each GUI notebook has a **last cell** that launches the web-based interactive GUI.  

- The **top of this cell** contains the `model` variable, which determines which LLM will be used in the GUI:

```python
model = "mistral-small"  # You can change it to your preferred model  
```

Open the corresponding GUI notebook and run the **last cell** in the notebook. It ends with:  

```python  
app.show()

```  
the web-based interactive GUI will launch.

### Model Details for GUI

- **Llama folder**: contains code using Llama model. This GUI uses **one-shot complex scenario prompt**.
- **Mistral-Small folder**: contains code using Mistral-Small model. This GUI uses **one-shot simple scenario prompt**.

Prompts used differ between the two GUI versions.

> The variable `model` in each notebook determines which model is used in the GUI. You can change it to your preferred model (e.g., `"mistral-small"`). All GUI calls will use this variable.

### GUI Notebook Notes

- The final GUI notebooks in the **GUI-Interactive** folder use the **one-shot prompting strategy**, which produced the best overall results in experiments.

### Configuring for a Different LLM  

If you are **not using the Uni Münster LLM**, update the following variables:  

`base_url` variable in the notebook to match your LLM provider’s endpoint. For example:  

```python
base_url = "https://api.openai.com/v1"  # OpenAI endpoint
``` 

`model` variable in the notebook for using LLM of choice. For example:   

```python
model = "mistral-small"  # model used  
```

In GUI notebooks, the `model` and `base_url` variables are at the top of the last cell in the notebook. 
In other notebooks, update the variables in initialization cells for a specific prompt strategy. 


