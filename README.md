# 🚜 GNSS-CAN Farm Tractor Operations Dataset

A multivariate time series dataset collected from a **New Holland T7.165 S** farm tractor equipped with **GNSS** and **CAN-Bus** sensors.  

The dataset supports research in **precision agriculture** by enabling:  
- **Operational state classification & clustering**  
- **Time-series anomaly detection**  
- **Predictive maintenance research**  

It also includes **synthetic anomalies** generated through a multi-agent workflow powered by **Large Language Models (LLMs)**, designed to simulate realistic fault conditions.  

---

## 📍 Dataset Overview

- **Collection site**: Lucio Toniolo experimental farm, University of Padova (`45°20'42.5"N, 11°57'15.1"E`)
- **Tractor model**: New Holland T7.165 S  
- **Sensors**:  
  - **GNSS** (u-blox NEO-M8U): 2.5 m CEP  
  - **CAN-Bus**: engine speed, hydraulic pressure, ground speed, and other signals  
- **Sampling frequency**: 1 Hz  
- **Labeling**: Manual, based on real observations  
- **Operational states**: `Working`, `Turning`, `Moving`, `Idle`  

---

## 📊 Dataset Structure & Format

The dataset consists of **two work sessions** (train/test split). Each row corresponds to one timestamped observation with synchronized GNSS and CAN-Bus signals.  

| Split           | Observations | Purpose                                               |
|-----------------|--------------|-------------------------------------------------------|
| Work-session 1  | 17,447       | Training of terrain- and activity-specific models      |
| Work-session 2  | 11,795       | Anomaly injection and model evaluation                 |

**CSV columns include:**  
- `timestamp`  
- `latitude`, `longitude`  
- `engine_speed`, `hydraulic_pressure`, `ground_speed`  
- `...` (other CAN-Bus signals)  
- `operational_state` (categorical label)  

---

## 🧪 Anomaly Injection Workflow

Synthetic anomalies were generated through a **multi-agent pipeline of LLMs**. Each agent contributes to designing, validating, and applying anomalies to the dataset, resulting in realistic augmented data for benchmarking.  

The workflow proceeds as follows:  

- **LLM Selection**: Several models (GPT-4o, Llama 3.1 70B, Gemini 2.0, Mistral Large 2) propose operational ranges for tractor variables, which are compared to real-world ranges. The most accurate model is chosen.  
- **Anomaly Case Generation**: The selected LLM proposes anomaly scenarios, which are then formalized into explicit anomaly rules.  
- **Validation**: Another LLM verifies that the anomaly rules are realistic and consistent.  
- **Python Code Generation**: Validated rules are translated into Python code.  
- **Anomalous Dataset Creation**: The generated rules are applied to produce augmented datasets with injected anomalies.  

All **prompts used in this workflow** are available in the [`prompts`](./prompts) folder.  

---

## 🧑‍🔬 Citation

If you use this dataset, please cite:  

> Lindia, L., Cantini, R., Bettucci, F., Sartori, L., & Trunfio, P. (2025). _"Predictive maintenance in agricultural machinery: Spatiotemporal anomaly detection with LLM-generated test faults"_ [Manuscript submitted for publication]. _Computers in Industry._

---

## 📬 Contact

For questions or collaborations:  

- **Paolo Lindia** – [paolo.lindia@dimes.unical.it](mailto:paolo.lindia@dimes.unical.it)  
- **Francesco Bettucci** – [francesco.bettucci@phd.unipd.it](mailto:francesco.bettucci@phd.unipd.it)  

---

## 📝 License

Released under [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/).  
You may use, share, and adapt the data for **non-commercial purposes**, with proper attribution.  
