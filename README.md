# ☀️ Physics-Informed Neural Networks (PINN) for Photovoltaic Systems

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Machine Learning](https://img.shields.io/badge/Machine%20Learning-PINN-orange)
![Status](https://img.shields.io/badge/Status-Completed-success)

## 📖 Project Overview
This repository contains the code and methodology for predicting the **Performance Ratio (PR)** of industrial photovoltaic (PV) systems using a **Physics-Informed Multilayer Perceptron (PINN)**. 

Classical Deep Learning models act as statistical "black boxes" that optimize strictly mathematical errors, often leading to thermodynamically impossible predictions (e.g., predicting an energy output that implies a solar irradiance higher than physically possible under given weather conditions). This project solves this "physical blindness" by anchoring the laws of energy conservation directly into the neural network's gradient descent optimization process.

> **Note:** This research was developed as a collaboration between the *Gheorghe Asachi Technical University of Iasi* (Romania) and the *University of Oviedo* (Spain).

## ✨ Key Features & Innovations
* **Thermodynamic Double-Bound Loss Function:** A custom `ReLU`-based hybrid loss function that penalizes the network whenever its abstract PR prediction implies a daily solar irradiation ($H_{poa}$) outside the physical limits of $[3.8 - 4.2] \text{ kWh/m}^2\text{/day}$.
* **Advanced Feature Engineering:** Synthesizing 6 thermo-electrical stress indicators (e.g., Thermal Efficiency, Voltage/Current Stress Ratios, DC/AC overload) from 10 raw hardware and meteorological parameters.
* **Operational Space Balancing:** Using **SMOTE** oversampling to ensure uniform statistical distribution across 4 distinct operational states: *Optimal, Overclipping, Gray Zone, and Failure*, effectively removing nominal-operation bias.

## 📊 Dataset
The dataset was synthetically generated using iterative simulations in **NREL System Advisor Model (SAM)**, combined with meteorological boundary conditions from the **National Solar Radiation Database (NSRDB)**.
* **Input Features:** 16 combined features (10 raw physical variables + 6 calculated stress indicators).
* **Target Variable:** Performance Ratio (PR).
* **Total Samples (Balanced):** 5,180 (1,295 samples per operational class).

## 🧠 Neural Network Architecture & Hyperparameters
* **Topology:** Multilayer Perceptron (MLP) with 3 hidden layers: `(150, 100, 50)` neurons.
* **Activation Function:** `ReLU`
* **Optimizer:** `Adam`
* **L2 Penalty (Alpha):** `0.001`
* **Max Epochs:** `2000`
* **Physical Penalty Factor ($\lambda$):** `0.01` (dynamically balances the MSE and the thermodynamic compliance).

## 🏆 Results
By successfully eradicating out-of-bounds predictions and enforcing physical limits, the final Double-Bound PINN architecture achieved exceptional predictive accuracy:
* **$R^2$ Score:** `0.9883`
* **Mean Squared Error (MSE):** `0.000833`

This makes the model a highly robust and scalable tool for real-time fault detection and AI-based predictive maintenance in industrial PV control rooms.
