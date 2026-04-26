# Setup Instructions

## Quick Start Guide

### 1. Clone the Repository
```bash
git clone https://github.com/YOUR_USERNAME/lstm-vs-patchtst-energy-forecasting.git
cd lstm-vs-patchtst-energy-forecasting
```

### 2. Set Up Environment

#### Option A: Google Colab (Recommended)
1. Upload `lstm_patchtst_comparison.ipynb` to Google Colab
2. Runtime → Change runtime type → Hardware accelerator → GPU (T4)
3. Run all cells - dependencies will be installed automatically

#### Option B: Local Setup
```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### 3. Configure Kaggle API

To download the dataset, you need Kaggle credentials:

1. **Get Kaggle API Token**:
   - Go to https://www.kaggle.com/
   - Click on your profile picture → Account
   - Scroll to "API" section → Click "Create New API Token"
   - This downloads `kaggle.json`

2. **Setup (Local)**:
   ```bash
   # Linux/macOS
   mkdir -p ~/.kaggle
   mv kaggle.json ~/.kaggle/
   chmod 600 ~/.kaggle/kaggle.json
   
   # Windows
   mkdir %USERPROFILE%\.kaggle
   move kaggle.json %USERPROFILE%\.kaggle\kaggle.json
   ```

3. **Setup (Colab)**:
   - The notebook will prompt you for username and API key
   - Get these from your `kaggle.json` file

### 4. Run the Notebook

#### Google Colab:
1. Open `lstm_patchtst_comparison.ipynb` in Colab
2. Run all cells (Runtime → Run all)
3. Enter Kaggle credentials when prompted
4. Results will be saved to Google Drive

#### Local Jupyter:
```bash
jupyter notebook lstm_patchtst_comparison.ipynb
```

## Expected Runtime

- **Data Download**: 1-2 minutes
- **Data Preprocessing**: 2-3 minutes
- **LSTM Training**: 15-20 minutes (on GPU)
- **PatchTST Training**: 20-25 minutes (on GPU)
- **Evaluation & Visualization**: 2-3 minutes

**Total**: ~40-50 minutes on Google Colab T4 GPU

## Hardware Requirements

### Minimum (CPU):
- RAM: 8GB
- Storage: 2GB
- Runtime: ~4-6 hours

### Recommended (GPU):
- GPU: NVIDIA T4 or better (4GB+ VRAM)
- RAM: 12GB+
- Storage: 5GB
- Runtime: ~40-50 minutes

## Troubleshooting

### Common Issues

1. **Kaggle Download Fails**
   ```
   Error: 401 Unauthorized
   ```
   **Solution**: Check your Kaggle credentials are correct

2. **Out of Memory Error**
   ```
   ResourceExhaustedError: OOM when allocating tensor
   ```
   **Solution**: Reduce batch size in the notebook (line ~500, change `batch_size=32` to `batch_size=16`)

3. **GPU Not Detected**
   ```bash
   # Check GPU availability
   import tensorflow as tf
   print(tf.config.list_physical_devices('GPU'))
   ```
   **Solution**: In Colab, verify GPU is enabled (Runtime → Change runtime type → GPU)

4. **Import Errors**
   ```
   ModuleNotFoundError: No module named 'xyz'
   ```
   **Solution**: Reinstall requirements:
   ```bash
   pip install -r requirements.txt --upgrade
   ```

### Dataset Issues

If automatic download fails, manually download:
1. Go to https://www.kaggle.com/datasets/robikscube/hourly-energy-consumption
2. Download ZIP file
3. Extract to `data/hourly-energy-consumption/` in the notebook directory
4. Comment out the `opendatasets` download cell

## Directory Structure

After running the notebook, your directory will look like:
```
lstm-vs-patchtst-energy-forecasting/
├── lstm_patchtst_comparison.ipynb  # Main notebook
├── README.md                        # Project documentation
├── requirements.txt                 # Dependencies
├── .gitignore                       # Git ignore rules
├── SETUP.md                         # This file
├── data/                            # Downloaded dataset (ignored by git)
│   └── hourly-energy-consumption/
│       └── *.paruqet files
└── outputs/                         # Generated files (optional)
    ├── model_lstm.keras
    ├── model_patch_tst.keras
    ├── predictions.csv
    └── *.png
```

## Next Steps

1. **Experiment with Hyperparameters**: Modify batch size, learning rate, model architecture
2. **Try Different Forecasting Horizons**: Change from 24-hour to 48-hour or weekly forecasts
3. **Add More Models**: Implement GRU, Temporal Fusion Transformer, N-BEATS
4. **Feature Engineering**: Add calendar features (day of week, holidays), weather data
5. **Ensemble Methods**: Combine LSTM and PatchTST predictions

## Getting Help

- **GitHub Issues**: Open an issue on the repository
- **Email**: Contact the author for questions
- **Documentation**: Check TensorFlow and Keras documentation for model-specific questions

## Citation

If you use this code in your research, please cite:
```
@misc{mahadik2026lstm-patchtst,
  author = {Mahadik, Sagar},
  title = {LSTM vs PatchTST: Energy Consumption Forecasting},
  year = {2026},
  publisher = {GitHub},
  url = {https://github.com/Saggy7276/lstm-vs-patchtst-energy-forecasting}
}
```
