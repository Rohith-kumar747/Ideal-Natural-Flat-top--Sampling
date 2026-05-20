# Exp 1 Ideal, Natural, & Flat-top -Sampling
# Aim
Write a simple Python program for the construction and reconstruction of ideal, natural, and flattop sampling.
# Tools required
Python IDE
# Program
# Ideal Sampling:
```PYTHON
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import resample

# Parameters
fs, f = 100, 5
t = np.arange(0, 1, 1/fs)

# Continuous signal
x = np.sin(2*np.pi*f*t)

# Impulse sampling
xs = x

# Reconstruction
xr = resample(xs, len(t))

# Plot
plt.figure(figsize=(10,8))
plt.suptitle("NAME : ROHITH KUMAR GD\nREG NO : 212224060220",
             fontsize=12, fontweight='bold')

plt.subplot(3,1,1)
plt.plot(t, x)
plt.title("Continuous Signal (fs = 100 Hz)")
plt.grid(True)

plt.subplot(3,1,2)
plt.stem(t, xs, basefmt=" ")
plt.title("Sampled Signal (Impulse Sampling)")
plt.grid(True)

plt.subplot(3,1,3)
plt.plot(t, xr, 'r--')
plt.title("Reconstructed Signal")
plt.grid(True)

plt.tight_layout(rect=[0,0,1,0.93])
plt.show() 
```
# Natural Sampling:
``` PYTHON
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, lfilter

# Parameters
fs, T, fm, fp = 1000, 1, 5, 50
t = np.arange(0, T, 1/fs)

# Message signal
m = np.sin(2*np.pi*fm*t)

# Pulse train
pw = fs // (2*fp)
p = np.zeros_like(t)
p[::fs//fp] = 1
p = np.convolve(p, np.ones(pw), mode='same')

# Natural sampling
nat = m * p

# Reconstruction (LPF)
b, a = butter(4, 10/(0.5*fs), 'low')
rec = lfilter(b, a, nat)

# Plot
plt.figure(figsize=(10,9))
plt.suptitle("NAME : ROHITH KUMAR GD\nREG NO : 212224060220",
             fontsize=12, fontweight='bold')

plt.subplot(4,1,1)
plt.plot(t, m)
plt.title("Message Signal")
plt.grid(True)

plt.subplot(4,1,2)
plt.plot(t, p)
plt.title("Pulse Train")
plt.grid(True)

plt.subplot(4,1,3)
plt.plot(t, nat)
plt.title("Natural Sampling")
plt.grid(True)

plt.subplot(4,1,4)
plt.plot(t, rec, color='g')
plt.title("Reconstructed Signal")
plt.grid(True)

plt.tight_layout(rect=[0,0,1,0.93])
plt.show()
```
# Flat-top -Sampling:
```PYTHON
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, lfilter

# Parameters
fs, T, fm, fp = 1000, 1, 5, 50
t = np.arange(0, T, 1/fs)

# Message signal
m = np.sin(2*np.pi*fm*t)

# Sampling
bd = fs // fp
idx = np.arange(0, len(t), bd)
flat = np.zeros_like(t)

for i in idx:
    flat[i:i+bd//2] = m[i]

 Low-pass filter (reconstruction)
b, a = butter(4, (2*fm)/(0.5*fs), 'low')
recon = lfilter(b, a, flat)

# Plot
plt.figure(figsize=(10,9))
plt.suptitle("NAME : ROHITH KUMAR GD\nREG NO : 212224060220",
             fontsize=12, fontweight='bold')

plt.subplot(4,1,1)
plt.plot(t, m)
plt.title("Message Signal")

plt.subplot(4,1,2)
plt.stem(t[idx], np.ones_like(idx), basefmt=" ")
plt.title("Sampling Instants")

plt.subplot(4,1,3)
plt.plot(t, flat)
plt.title("Flat-Top Sampled Signal")

plt.subplot(4,1,4)
plt.plot(t, recon, color='g')
plt.title("Reconstructed Signal")

plt.tight_layout(rect=[0,0,1,0.93])
plt.show()
```

# Output Waveform
# Ideal Sampling:
<img width="1229" height="972" alt="image" src="https://github.com/user-attachments/assets/fc2118a4-123e-48b0-af28-c740d785e97e" />

# Natural Sampling:
<img width="1220" height="1098" alt="image" src="https://github.com/user-attachments/assets/6071d4fa-13aa-49f4-874c-7ede6970b0c4" />


# Flat-top -Sampling:
<img width="1218" height="1106" alt="image" src="https://github.com/user-attachments/assets/a5cc6106-6d4b-4369-a599-b60dccf0bfe8" />


# Results


Thus, the construction and reconstruction of Ideal, Natural, and Flat-top sampling were successfully implemented using Python, and the corresponding waveforms were obtained.


