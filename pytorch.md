Here’s a **comprehensive PyTorch cheatsheet** covering the essentials for building, training, and testing neural networks in PyTorch.

---

# **PyTorch Cheatsheet**

## **1. Basics**

### Import PyTorch
```python
import torch
import torch.nn as nn
import torch.optim as optim
import torch.nn.functional as F
from torch.utils.data import DataLoader, Dataset
```

### Tensor Basics
```python
# Create tensors
x = torch.tensor([1, 2, 3])
y = torch.zeros((2, 3))         # 2x3 zero tensor
z = torch.ones((2, 3))          # 2x3 tensor of ones
a = torch.randn((2, 2))         # Random tensor (Normal Distribution)

# Data types
x = torch.tensor([1.0, 2.0], dtype=torch.float32)
x = x.to(torch.int64)  # Change tensor data type

# GPU Support
device = torch.device('cuda' if torch.cuda.is_available() else 'cpu')
x = x.to(device)
```

### Tensor Operations
```python
# Arithmetic
a = torch.randn(2, 2)
b = torch.randn(2, 2)
c = a + b          # Addition
d = a - b          # Subtraction
e = a * b          # Element-wise multiplication
f = torch.matmul(a, b)  # Matrix multiplication

# Reshape
x = torch.randn(2, 6)
y = x.view(3, 4)   # Reshape into (3, 4)

# Slicing
x = torch.arange(10)  # Tensor: [0, 1, ..., 9]
print(x[:5])          # First 5 elements

# Gradients
x = torch.randn(2, 2, requires_grad=True)
y = x + 2
z = y * y * 3
z.mean().backward()  # Compute gradients
print(x.grad)
```

---

## **2. Building Neural Networks**

### Define a Model
```python
# Define a simple feedforward neural network
class Net(nn.Module):
    def __init__(self):
        super(Net, self).__init__()
        self.fc1 = nn.Linear(4, 3)  # Input: 4, Output: 3
        self.fc2 = nn.Linear(3, 1)  # Input: 3, Output: 1

    def forward(self, x):
        x = F.relu(self.fc1(x))  # Activation
        x = self.fc2(x)          # No activation for output layer
        return x

model = Net()
print(model)
```

### Loss Function and Optimizer
```python
# Loss Function
criterion = nn.MSELoss()  # Mean Squared Error Loss

# Optimizer
optimizer = optim.Adam(model.parameters(), lr=0.01)  # Adam optimizer
```

---

## **3. Training a Model**

### Training Loop
```python
# Dummy data
inputs = torch.randn(10, 4)  # 10 samples, 4 features
targets = torch.randn(10, 1)  # 10 samples, 1 target

# Training loop
epochs = 100
for epoch in range(epochs):
    # Forward pass
    outputs = model(inputs)
    loss = criterion(outputs, targets)

    # Backward pass and optimization
    optimizer.zero_grad()  # Clear previous gradients
    loss.backward()        # Backpropagation
    optimizer.step()       # Update weights

    if (epoch + 1) % 10 == 0:
        print(f"Epoch [{epoch+1}/{epochs}], Loss: {loss.item():.4f}")
```

---

## **4. Dataset and DataLoader**

### Custom Dataset
```python
class CustomDataset(Dataset):
    def __init__(self, data, labels):
        self.data = data
        self.labels = labels

    def __len__(self):
        return len(self.data)

    def __getitem__(self, idx):
        return self.data[idx], self.labels[idx]

# Example
data = torch.randn(100, 4)
labels = torch.randint(0, 2, (100, 1))
dataset = CustomDataset(data, labels)
```

### DataLoader
```python
# DataLoader for batching and shuffling
dataloader = DataLoader(dataset, batch_size=16, shuffle=True)

for batch_data, batch_labels in dataloader:
    print(batch_data.size(), batch_labels.size())
```

---

## **5. Save and Load Models**

### Save Model
```python
torch.save(model.state_dict(), 'model.pth')
```

### Load Model
```python
model = Net()
model.load_state_dict(torch.load('model.pth'))
model.eval()  # Set to evaluation mode
```

---

## **6. GPU Training**

### Move Model and Data to GPU
```python
model = model.to(device)
inputs = inputs.to(device)
targets = targets.to(device)

# Forward pass on GPU
outputs = model(inputs)
```

---

## **7. Pretrained Models (TorchVision)**

### Import Pretrained Models
```python
import torchvision.models as models

# Load a pretrained ResNet model
resnet18 = models.resnet18(pretrained=True)
resnet18.eval()

# Modify the final layer for custom tasks
resnet18.fc = nn.Linear(resnet18.fc.in_features, 10)  # Example: 10 output classes
```

---

## **8. Common Activation Functions**
```python
x = torch.randn(2, 2)

# ReLU
y = F.relu(x)

# Sigmoid
y = torch.sigmoid(x)

# Softmax
y = F.softmax(x, dim=1)

# Tanh
y = torch.tanh(x)
```

---

## **9. Gradient Management**

### No Gradient Computation (Inference Mode)
```python
with torch.no_grad():
    outputs = model(inputs)
```

### Detach Tensor from Computation Graph
```python
x = x.detach()
```

---

## **10. Debugging and Visualization**

### Check Gradients
```python
for param in model.parameters():
    print(param.grad)
```

### Tensor Shapes
```python
print(tensor.shape)
```

---

## **11. Tips and Tricks**

1. **Memory Management:** Use `torch.cuda.empty_cache()` to clear GPU memory.  
2. **Mixed Precision Training:** Use `torch.cuda.amp` for faster training.  
3. **Initialization:** Use `nn.init` for custom weight initialization:
   ```python
   nn.init.xavier_uniform_(model.fc1.weight)
   ```

---

This gives you an overview of the most common PyTorch functionalities.
