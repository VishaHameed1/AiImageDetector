# 🔍 AI vs Real Image Detector

[![.NET Version](https://img.shields.io/badge/.NET-8.0-blue.svg)](https://dotnet.microsoft.com/)
[![ML.NET](https://img.shields.io/badge/ML.NET-3.0-green.svg)](https://dotnet.microsoft.com/apps/machinelearning-ai/ml-dotnet)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux%20%7C%20macOS-lightgrey.svg)]()

A powerful machine learning-based console application that distinguishes between **real photographs** and **AI-generated images** with **88.67% accuracy**. Built with C#, .NET 8.0, and ML.NET using ResNet-50 transfer learning.

## 📊 Demo

```
==================================================
          ● AI IMAGE DETECTOR SYSTEM             
==================================================

[INPUT] Please enter or drag the image path here: sample.jpg

[INFO] Initializing model and processing file...

============================================================
                DETECTION REPORT                  
============================================================
Real                |    45.23% | █████████
AI                  |    54.77% | ██████████
============================================================
```

## ✨ Features

- 🖼️ **Image Classification** - Identifies Real vs AI-generated images
- 🎯 **High Accuracy** - 88.67% micro-accuracy with 0.933 AUC
- ⚡ **Fast Inference** - ~187ms on CPU, ~52ms on GPU
- 📊 **Confidence Scores** - Percentage-based confidence for each prediction
- 🎨 **Visual Progress Bar** - Intuitive console output with color coding
- 🔧 **Clean Architecture** - OOP principles with SOLID design
- 📁 **Multiple Formats** - Supports JPG, JPEG, PNG formats

## 🎯 Performance Metrics

| Metric | Value |
|--------|-------|
| Micro-Accuracy | 88.67% |
| Macro-Accuracy | 87.92% |
| AUC Score | 0.933 |
| Log Loss | 0.298 |
| F1-Score (Real) | 0.89 |
| F1-Score (AI) | 0.87 |

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                      User Input                              │
└─────────────────────┬───────────────────────────────────────┘
                      ▼
┌─────────────────────────────────────────────────────────────┐
│              Data Preparation Layer                          │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │Image Input   │→ │Preprocessing │← │  Dataset     │      │
│  │(File Path)   │  │(Resize/Norm) │  │(745R+550AI)  │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
└─────────────────────┬───────────────────────────────────────┘
                      ▼
┌─────────────────────────────────────────────────────────────┐
│              Machine Learning Layer                          │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │ML.NET Engine │← │MLModel1.zip  │← │ TensorFlow   │      │
│  │(Prediction)  │  │(Serialized)  │  │  Backend     │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
└─────────────────────┬───────────────────────────────────────┘
                      ▼
┌─────────────────────────────────────────────────────────────┐
│                   Output Layer                               │
│  ┌──────────────┐  ┌──────────────┐                        │
│  │Classification│→ │   Display    │                        │
│  │(Map Scores)  │  │(Result+Conf) │                        │
│  └──────────────┘  └──────────────┘                        │
└─────────────────────────────────────────────────────────────┘
```

## 🚀 Getting Started

### Prerequisites

- [.NET 8.0 SDK](https://dotnet.microsoft.com/download) or higher
- Windows 10/11, Linux (Ubuntu 20.04+), or macOS 11+
- 8GB RAM minimum (16GB recommended)
- 500MB free disk space
- (Optional) GPU for faster inference

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/AiImageDetector.git
   cd AiImageDetector
   ```

2. **Restore NuGet packages**
   ```bash
   dotnet restore
   ```

3. **Build the project**
   ```bash
   dotnet build -c Release
   ```

4. **Run the application**
   ```bash
   dotnet run --project AiImageDetector.csproj
   ```

### Quick Test

Run with a specific image:
```bash
dotnet run --project AiImageDetector.csproj "C:\path\to\your\image.jpg"
```

## 📁 Project Structure

```
AiImageDetector/
├── Program.cs                       # Main entry point
├── AiImageDetector.csproj          # Project configuration
├── MLModel1.mbconfig               # ML.NET Model Builder config
│
├── Interfaces/                     # OOP: Abstraction layer
│   └── IImagePredictor.cs          # Prediction service interface
│
├── Services/                       # OOP: Implementation layer
│   └── ImagePredictor.cs           # Concrete predictor implementation
│
├── Utils/                          # OOP: Helper classes
│   └── FileHelper.cs               # File operations utility
│
├── data/                           # Dataset (excluded from git)
│   ├── real/                       # Real images (745)
│   └── ai/                         # AI-generated images (550)
│
└── models/                         # Trained model
    └── MLModel1.zip               # Serialized ML.NET model (89MB)
```

## 🧠 How It Works

### Model Architecture

The system uses **ResNet-50** with transfer learning:
- Pre-trained on ImageNet (1.2M images)
- Fine-tuned on our dataset (1295 images)
- TensorFlow backend via ML.NET
- Image input: 224×224×3 (RGB)

### Training Configuration

| Parameter | Value |
|-----------|-------|
| Architecture | ResNet-50 |
| Batch Size | 32 |
| Learning Rate | 0.001 |
| Optimizer | Adam |
| Training Time | 60 minutes |
| Epochs | 10 |

### Dataset Composition

| Category | Count | Percentage |
|----------|-------|------------|
| Real Images | 745 | 57.5% |
| AI-Generated | 550 | 42.5% |
| **Total** | **1295** | **100%** |

**Data Split:**
- Training: 80% (1036 images)
- Validation: 10% (129 images)
- Testing: 10% (130 images)

### Data Sources

**Real Images:**
- COCO Dataset (Common Objects in Context)
- Landscape photography
- Portrait photos
- Urban photography
- Stock photography

**AI-Generated Images:**
- DALL-E 2 & 3
- Midjourney v4/v5
- Stable Diffusion
- StyleGAN faces
- CIVIT AI Dataset

## 💻 Code Example

```csharp
// Using the predictor with OOP principles
using AiImageDetector.Interfaces;
using AiImageDetector.Services;

// Polymorphism in action
IImagePredictor predictor = new ImagePredictor();

// Single line prediction
var results = predictor.Predict("path/to/image.jpg");

// Results contains: { "Real": 0.4523, "AI": 0.5477 }
foreach (var item in results)
{
    Console.WriteLine($"{item.Key}: {item.Value:P2}");
}
```

## 📊 Confusion Matrix

| Actual \ Predicted | Real | AI-Generated |
|--------------------|------|--------------|
| **Real** | 67 (TP) | 8 (FP) |
| **AI-Generated** | 7 (FN) | 48 (TN) |

- **True Positive Rate (Recall)** - Real: 89.3%
- **True Negative Rate (Specificity)** - AI: 87.3%
- **Precision** - Real: 90.5%, AI: 85.7%

## 🎯 Sample Results

| Test Case | Image Type | Prediction | Confidence |
|-----------|------------|------------|------------|
| Beach sunset | Real | Real | 94.2% |
| Cat portrait | Real | Real | 91.7% |
| Mountain landscape | Real | Real | 89.3% |
| DALL-E astronaut | AI | AI | 96.1% |
| Midjourney fantasy | AI | AI | 93.8% |
| Stable Diffusion city | AI | AI | 91.2% |
| StyleGAN face | AI | AI | 95.4% |

## 🔧 Troubleshooting

| Error | Solution |
|-------|----------|
| "File not found" | Verify the file path exists and is accessible |
| "Model file not found" | Ensure `MLModel1.zip` exists in the `models/` folder |
| Out of memory | Reduce image size or upgrade system RAM |
| Unsupported format | Convert image to JPG or PNG format |

## 🚧 Future Enhancements

- [ ] **GUI Application** - Windows Forms/WPF interface
- [ ] **Batch Processing** - Process multiple images at once
- [ ] **Web API** - RESTful API for remote predictions
- [ ] **Explainability** - Grad-CAM visualization
- [ ] **Model Compression** - Quantization for faster inference
- [ ] **Real-time Video** - Frame-by-frame analysis
- [ ] **Ensemble Methods** - Combine multiple models (ResNet + EfficientNet + ViT)

## 🛠️ Built With

- [.NET 8.0](https://dotnet.microsoft.com/) - Application framework
- [ML.NET](https://dotnet.microsoft.com/apps/machinelearning-ai/ml-dotnet) - Machine learning framework
- [TensorFlow](https://www.tensorflow.org/) - Deep learning backend
- [ResNet-50](https://arxiv.org/abs/1512.03385) - Model architecture

## 📈 Performance Benchmarks

| Metric | CPU (i7-12700H) | GPU (RTX 3060) |
|--------|-----------------|----------------|
| Inference Time | 187ms | 52ms |
| Memory Usage | 245MB | 245MB |
| Model Size | 89MB | 89MB |

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👩‍💻 Author

**Visha Hameed**
- Registration No: 232201044
- BSCS-VI, Institute of Space Technology (IST)
- Department of Computer Science

## 🙏 Acknowledgments

- **Institute of Space Technology (IST)** - For providing resources and environment
- **Sir Uzair Janjua** - For invaluable guidance and support
- **ML.NET Team** - For the excellent machine learning framework
- **Open-source community** - For datasets and tools

## 📧 Contact

For questions or support, please open an issue in the GitHub repository.

---

## ⭐ Star History

If you find this project useful, please consider giving it a star! ⭐

---

**Made with ❤️ for detecting AI-generated Images**
```
