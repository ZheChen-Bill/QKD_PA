# Privacy Amplification Module

## Overview
Privacy amplification is a crucial step in **Quantum Key Distribution (QKD)**, designed to mitigate information leakage by transforming the reconciled key into a secure secret key. This module utilizes **Toeplitz matrix multiplication** combined with an **exclusive OR (XOR)** operation to achieve secure key generation efficiently.

Key features:
- Converts reconciled keys into secret keys using random matrices.
- Optimized for FPGA hardware to handle large matrix operations with high efficiency.

![圖片](https://github.com/user-attachments/assets/c0b65bad-9719-4f23-9693-0573bbb27463)

---

## Process Description

### Toeplitz Hashing
The privacy amplification process involves the following steps:
1. **Matrix Multiplication**: Multiplies the reconciled key ($n − m$ bits) with a random $m×(n − m)$ Toeplitz matrix.
2. **XOR Operation**: Combines the resulting product with the remaining $m$ bits of the reconciled key.

### Input and Output
- Input reconciled key size: **$n = 1048576$ bits (fixed)**.
- Output secret key size: **$m \approx 10^5$ bits (variable)**.
- Secret key length is approximately **10%** of the input size.

To manage the large size of the Toeplitz matrix, the computation is divided into smaller segments, allowing for efficient parallel processing on FPGA hardware.

---

## Implementation

### Architecture
The module architecture is designed to handle large-scale computations efficiently:
- **Segmented Multiplication**: Divides the secret key vector into smaller parts ($k$ bits per segment).
- **Parallel MAC Units**: Leverages 1024 MAC units for high-speed operations.
- **Hardware Optimization**: Implements matrix multiplication and XOR using FPGA-specific optimizations.

The flowchart of the privacy amplification process is shown below:  
![Privacy Amplification Workflow](figsrc/CH3_PA_FC.drawio.pdf)

---

## Specifications
| **Parameter**               | **Value**             | **Remark**       |
|-----------------------------|-----------------------|------------------|
| Input Key Size ($n$-bit)    | 1048576 $\approx10^6$ | Fixed            |
| Output Secret Key Size ($m$-bit) | $\approx10^5$       | Variable         |
| Toeplitz Hashing            | Matrix Multiplication + XOR |                |
| MAC Units                   | 1024                 | Parallelized     |
| Word Width ($w$)            | 64                   |                  |

---

## Block Diagrams
### Module Diagrams
- **Alice's Privacy Amplification Module**  
![圖片](https://github.com/user-attachments/assets/d2290713-2ad2-4d10-ad13-8a7d4c20dc9a)
  
- **Bob's Privacy Amplification Module**  
![圖片](https://github.com/user-attachments/assets/26533ba4-22cf-4d02-a989-e3c06b65f295)

### I/O Ports
- **Alice's Module I/O**  
![圖片](https://github.com/user-attachments/assets/7416651f-ed53-4015-bf09-9e0334fcf1ad)
  
- **Bob's Module I/O**  
![圖片](https://github.com/user-attachments/assets/df455884-c349-41e6-8bed-4a8553e3a3bb)

---

## Key Features
1. **Efficient Matrix Multiplication**: Handles large $m \times (n - m)$ Toeplitz matrices with FPGA-optimized hardware.
2. **Scalable and Flexible**: Supports variable output sizes while maintaining a fixed input size.
3. **Robust Design**: Ensures secure key generation by leveraging random matrices and XOR operations.
4. **Parallel Processing**: Utilizes 1024 MAC units for enhanced performance.

---

## Conclusion
The privacy amplification module efficiently reduces information leakage in QKD systems, transforming reconciled keys into secure secret keys. By leveraging FPGA-optimized designs and parallel processing, this implementation ensures high performance and scalability for practical quantum communication systems.

