# AI vs Real Image Detector 🛡️

### Overview
This is a **C# Console Application** developed for my 5th-semester project at the **Institute of Space Technology (IST)**. The system uses Machine Learning to classify images into two categories: **Authentic (Real)** or **AI-Generated**.

### Key Features
* **High Accuracy:** Achieved a Micro-Accuracy of **88.67%** during training.
* **Real-time Prediction:** Fast inference using a pre-trained ML.NET model.
* **Modern Tech Stack:** Built using **.NET 8.0** and **ML.NET Model Builder**.
* **Pattern Recognition:** Analyzes complex image features and Logarithmic Loss to ensure reliable classification.

### Technical Specifications
* **Language:** C#
* **Framework:** .NET 8.0
* **Machine Learning Library:** ML.NET (TensorFlow integration for deep learning)
* **Dataset:** 1200+ images (745 Real, 550 AI-Generated)
* **Accuracy:** 0.8867 (Micro-Accuracy)

### How to Use
1. Clone the repository (excluding large binary files handled by .gitignore).
2. Ensure **.NET 10.0 Runtime** is installed on your system.
3. Run the application in Visual Studio.
4. Provide a local file path of an image (e.g., `C:\Images\test.jpg`).
5. The system will output the classification result and the **Confidence Score**.

### Project Structure
- `AiImageDetector/`: Main project files and Program.cs.
- `MLModel1.mbconfig`: The ML.NET model configuration used for training.
- `.gitignore`: Configured to ignore heavy `bin/`, `obj/`, and dataset folders for a clean repository.

---
**Developed by:** Visha Hameed  
**Institution:** Institute of Space Technology (IST)
