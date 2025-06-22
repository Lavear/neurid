This trained LSTM (Long Short-Term Memory) model is a core component of the AI-powered system designed to detect electricity theft, prevent transformer overload, and identify grid faults. It uses historical and real-time sensor data to predict anomalies and assist with automatic decisions like alerting authorities and switching loads between transformers.

⸻

1. Electricity Theft Detection

The model is trained to recognize normal electrical usage patterns using sequences of current and voltage data.

By comparing real-time sensor inputs from ESP32 nodes placed at different points along the feeder line, the model detects inconsistencies. If the upstream transformer node reports more current than the downstream node—beyond the expected load—it indicates possible theft or unregistered consumption between the two points.

This mechanism allows detection of intermediate tapping without requiring manual patrols or inspections.

⸻

2. Load Balancing

As a transformer becomes overloaded—either due to legal consumption growth or hidden theft—the load pattern changes gradually. The LSTM model is trained to detect these time-based deviations. Upon predicting overload, it prompts the system to switch the feeder line to a backup transformer using a smart relay.

This proactive rerouting prevents transformer failure and maintains power continuity.

⸻

3. Transformer Fault Detection

Irregular current or voltage fluctuations and sudden drops may signal transformer stress. The LSTM model captures such anomalies and predicts faults in advance. Its sequence-based learning allows early identification of gradual degradation—well before complete failure occurs.

When a fault is flagged, the system can:
	•	Send alerts to the monitoring dashboard
	•	Disconnect the faulty transformer via relay
	•	Maintain load flow using the alternate transformer

⸻

4. Why LSTM Is Ideal for This Project

Electricity usage patterns evolve over time. Rule-based systems often miss slow or complex trends. LSTM models, however:
	•	Learn from time-sequenced behavior
	•	Are resilient to noise and fluctuations
	•	Work efficiently on devices like Raspberry Pi 5 in real-time scenarios

⸻

5. Model Format and Integration
	•	The model is saved in .h5 format and trained on input sequences of shape (10, 3) — representing 10 time steps of voltage, current, and optional temperature.
	•	It runs on a Raspberry Pi 5, receiving sensor data from ESP32 nodes over WebSockets.
	•	On detecting anomalies, the system:
	•	Logs the event to Firebase or ThingsBoard
	•	Commands relays to reroute power where necessary

⸻

This model upgrades the system from basic monitoring to intelligent, autonomous control, turning it into a complete predictive smart grid prototype capable of real-time action against theft, overload, and transformer faults.
