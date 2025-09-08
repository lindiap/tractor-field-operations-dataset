# GNSS-CAN-FarmTractor-Operations-Dataset

This repository contains a multivariate time series dataset collected from a New Holland T7.165 S farm tractor equipped with GNSS and CAN-Bus sensors. The dataset is designed for training and evaluating machine learning models for operational state classification and anomaly detection in precision agriculture.

---

## 📍 Dataset Overview

- **Collection site**: Lucio Toniolo experimental farm, University of Padova  
  Coordinates: `45°20'42.5"N`, `11°57'15.1"E`
- **Tractor model**: New Holland T7.165 S
- **Sensors**:
  - **GNSS** (u-blox NEO-M8U): 2.5m CEP, 1Hz sampling
  - **CAN-Bus**: engine speed, hydraulic pressure, ground speed, and other operational parameters
- **Sampling frequency**: 1 Hz
- **Labeling**: Manual labeling based on CAN-Bus signal interpretation
- **Operational states**:
  - `Working`
  - `Turning`
  - `Moving`
  - `Idle`

---

## 📊 Dataset Structure

The dataset consists of two separate work sessions, split for training and testing:

| Split             | Observations | Description                                         |
|-------------------|--------------|-----------------------------------------------------|
| Work-session 1    | 17,447       | Used to train terrain- and activity-specific models |
| Work-session 2    | 11,795       | Used for anomaly injection and model evaluation     |

Each row in the dataset represents a timestamped reading with synchronized GNSS and CAN-Bus sensor values, along with an associated operational label.

---

## ☢️ Anomaly Generation

The anomaly generation process is based on a multi-agent workflow that leverages different Large Language Models (LLMs). All **prompts used** are available in the `prompts` folder of this repository.  

The workflow is structured as follows:  

1. **LLM Selection**  
   - Several models (GPT-4o, Llama 3.1 70B, Gemini 2.0, and Mistral Large 2) are asked to generate operational ranges for selected variables extracted from the tractor’s **CAN-Bus**.  
   - The generated ranges are compared with the real operational ranges, and the LLM that produces the most similar values is selected.  

2. **Anomaly Scenario Generation**  
   - Once the best-performing model is chosen, it is prompted to propose **anomaly cases or scenarios**.  
   - These scenarios are then passed to another prompt that asks the LLM to translate them into **formal anomaly rules**.  

3. **Anomaly Validation**  
   - Another LLM agent evaluates whether the generated anomaly rules are realistic and valid.  

4. **Python Code Generation**  
   - If an anomaly is validated, an LLM generates the corresponding **Python code** to apply the rules to the dataset.  

5. **Anomalous Dataset Creation**  
   - The validated anomalies are applied to the original dataset, producing an **anomalous dataset** for each generat

---

## 🧪 Applications

This dataset can be used also for:
- Operational state classification and clustering
- Time series anomaly detection
- Predictive maintenance research 

---

## 📁 Files and Format

The dataset is provided in CSV format and includes the following columns (indicative):

- `timestamp`
- `latitude`
- `longitude`
- `engine_speed`
- `hydraulic_pressure`
- `ground_speed`
- `...` (other CAN-Bus signals)
- `operational_state` (categorical label)

---

## 🧑‍🔬 Citation

If you use this dataset in your research, please cite:

> Lindia, L., Cantini, R., Bettucci, F., Sartori, L., & Trunfio, P. (2025). _"Predictive maintenance in agricultural machinery: Spatiotemporal anomaly detection with LLM-generated test faults"_ [Manuscript submitted for publication]. _Engineering Applications of Artificial Intelligence._

---

## 📬 Contact

For questions or collaborations, please contact:  
**Paolo Lindia** – [paolo.lindia@dimes.unical.it](mailto:paolo.lindia@dimes.unical.it)
**Francesco Bettucci** – [francesco.bettucci@phd.unipd.it](mailto:francesco.bettucci@phd.unipd.it)

---

## 📝 License

This dataset is released under the [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/) license.  
You are free to use, share, and adapt the data for **non-commercial** purposes, provided proper attribution.

---
