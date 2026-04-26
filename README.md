# LSTM vs PatchTST: Energy Consumption Forecasting

A comprehensive comparison of LSTM and PatchTST (Patch Time Series Transformer) models for hourly energy consumption forecasting using the PJM Interconnection dataset.

## 📊 Project Overview

This project implements and compares two state-of-the-art time series forecasting models:
- **LSTM (Long Short-Term Memory)**: Classic recurrent architecture for sequence modeling
- **PatchTST**: Modern Transformer-based model using patch-based representation

The models are trained and evaluated on hourly energy consumption data from the PJM Interconnection, one of the largest wholesale electricity markets in North America.

## 🎯 Key Features

- **Complete Pipeline**: Data loading, preprocessing, model training, evaluation, and visualization
- **Fair Comparison**: Both models trained with similar hyperparameters for objective comparison
- **Comprehensive Metrics**: MAE, MSE, RMSE, MAPE evaluation across multiple horizons
- **Visualization**: Training curves, predictions, residuals, and model comparison plots
- **Production-Ready**: Model checkpointing, early stopping, and Google Drive integration

## 📁 Dataset

**Source**: [Hourly Energy Consumption - Kaggle](https://www.kaggle.com/datasets/robikscube/hourly-energy-consumption)

- **Time Period**: 1998-2018 (20 years of hourly data)
- **Features**: 12 regional energy consumption columns
- **Size**: ~178,000 hourly observations
- **Target**: PJM_Load (total energy consumption)

## 🛠️ Technologies Used

- **Deep Learning**: TensorFlow/Keras
- **Data Processing**: pandas, NumPy
- **Visualization**: Matplotlib, Seaborn
- **Environment**: Google Colab with GPU (T4)

## 🚀 Getting Started

### Prerequisites

```bash
pip install tensorflow pandas numpy matplotlib seaborn pyarrow fastparquet opendatasets
```

### Running the Notebook

1. **Open in Google Colab**: Upload `lstm_patchtst_comparison.ipynb` to Colab
2. **Enable GPU**: Runtime → Change runtime type → GPU (T4 recommended)
3. **Set Up Kaggle Credentials**: Enter your Kaggle username and API key when prompted
4. **Run All Cells**: The notebook will automatically:
   - Download the dataset
   - Preprocess the data
   - Train both models
   - Generate comparison visualizations
   - Save results to Google Drive

### Local Execution

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/lstm-vs-patchtst-energy-forecasting.git
cd lstm-vs-patchtst-energy-forecasting

# Install dependencies
pip install -r requirements.txt

# Download dataset from Kaggle manually or using API
# Run the notebook using Jupyter
jupyter notebook lstm_patchtst_comparison.ipynb
```

## 📈 Model Architecture

### LSTM Model
- **Input**: Lookback window of 168 hours (1 week)
- **Layers**: 
  - LSTM(128, return_sequences=True)
  - Dropout(0.2)
  - LSTM(64)
  - Dropout(0.2)
  - Dense(32, ReLU)
  - Dense(24) - Output for 24-hour forecast
- **Parameters**: ~160K

### PatchTST Model
- **Input**: Same 168-hour lookback window
- **Patch Length**: 16 hours
- **Architecture**:
  - Patch Embedding Layer
  - 4 Transformer Encoder blocks (64 units, 4 heads)
  - Multi-head Attention with dropout
  - Feed-forward network
  - Dense output projection
- **Parameters**: ~120K

## 📊 Results

The notebook generates comprehensive evaluation metrics and visualizations:

1. **Training History**: Loss and MAE curves for both models
2. **Predictions Plot**: Visual comparison of actual vs predicted values
3. **Residual Analysis**: Error distribution analysis
4. **Performance Metrics**: MAE, MSE, RMSE, MAPE comparison
5. **Inference Speed**: Prediction time benchmarking

### Sample Metrics Structure
```
LSTM:
  - MAE: [value] MW
  - RMSE: [value] MW
  - MAPE: [value]%
  - Inference Time: [value] ms

PatchTST:
  - MAE: [value] MW
  - RMSE: [value] MW
  - MAPE: [value]%
  - Inference Time: [value] ms
```

## 💾 Output Files

The notebook saves the following to Google Drive:

- `model_lstm.keras` - Trained LSTM model
- `model_patch_tst.keras` - Trained PatchTST model
- `best_lstm.weights.h5` - Best LSTM checkpoint
- `history.csv` - Training history
- `predictions.csv` - Test set predictions
- `model_comparison.png` - Comparison visualization
- `training_history_comparison.png` - Training curves

## 🔬 Experimental Setup

- **Train/Validation/Test Split**: 70% / 15% / 15%
- **Lookback Window**: 168 hours (1 week)
- **Forecast Horizon**: 24 hours (1 day)
- **Batch Size**: 32
- **Epochs**: 50 (with early stopping, patience=5)
- **Optimizer**: Adam
- **Loss Function**: Mean Squared Error (MSE)
- **Metrics**: MAE

## 📝 Key Findings

The notebook provides a detailed comparison including:
- Which model achieves better accuracy (lower MAE)
- Speed-accuracy tradeoff analysis
- Model complexity comparison
- Deployment recommendations based on use case

## 🤝 Contributing

Contributions are welcome! Areas for improvement:
- Hyperparameter tuning
- Additional baseline models (GRU, Transformer variants)
- Multi-step ahead forecasting evaluation
- Ensemble methods
- Feature engineering (weather, calendar effects)

## 📄 License

This project is open source and available under the MIT License.

## 👤 Author

**Sagar Mahadik**
- GitHub: [@Saggy7276](https://github.com/Saggy7276)
- LinkedIn: [Sagar Mahadik](https://www.linkedin.com/in/sagar-mahadik)

## 🙏 Acknowledgments

- Dataset provided by [Rob Mulla](https://www.kaggle.com/robikscube) on Kaggle
- PJM Interconnection for making energy data publicly available
- Original PatchTST paper: [A Time Series is Worth 64 Words](https://arxiv.org/abs/2211.14730)

## 📚 References

1. Hochreiter, S., & Schmidhuber, J. (1997). Long short-term memory. Neural computation.
2. Nie, Y., et al. (2022). A Time Series is Worth 64 Words: Long-term Forecasting with Transformers. ICLR 2023.
3. PJM Interconnection. (2024). Hourly Energy Consumption Dataset.

---

⭐ If you find this project useful, please consider giving it a star!
