# PSK
# Aim
Write a simple Python program for the modulation and demodulation of PSK and QPSK.
# Tools required
1.Personal Computer
2.Google Colab
# Program
## PSK
```
import numpy as np
import matplotlib.pyplot as plt

# ---------------- PARAMETERS ----------------
fs = 1000          # sampling frequency
Tb = 1             # bit duration
fc = 5             # carrier frequency
data = [1,0,1,1,0,1]

t = np.arange(0, Tb, 1/fs)

# ---------------- MESSAGE ----------------
message = np.repeat(data, len(t))
time = np.arange(len(message)) / fs

# ---------------- CARRIER ----------------
carrier = np.sin(2*np.pi*fc*time)

# ---------------- PSK MODULATION ----------------
# 1 -> +1 , 0 -> -1
polar_data = 2*message - 1
psk = polar_data * carrier

# ---------------- DEMODULATION ----------------
demod = psk * carrier
reconstructed = (demod > 0).astype(int)

# ---------------- PLOTS ----------------
plt.figure(figsize=(12,8))

plt.subplot(4,1,1)
plt.plot(time, message)
plt.title("Message Signal")
plt.ylim(-0.5,1.5)
plt.grid()

plt.subplot(4,1,2)
plt.plot(time, carrier)
plt.title("Carrier Signal")
plt.grid()

plt.subplot(4,1,3)
plt.plot(time, psk)
plt.title("PSK Modulated Signal")
plt.grid()

plt.subplot(4,1,4)
plt.plot(time, reconstructed)
plt.title("Demodulated Signal")
plt.ylim(-0.5,1.5)
plt.grid()

plt.tight_layout()
plt.show()
```
## QPSK
```
import numpy as np
import matplotlib.pyplot as plt

# -------- PARAMETERS --------
fs, Tb, fc = 1000, 1, 5
data = [1,0, 0,1, 1,1, 0,0]   # even bits

t = np.arange(0, Tb, 1/fs)

# -------- MESSAGE --------
I = np.repeat(data[0::2], len(t))
Q = np.repeat(data[1::2], len(t))
time = np.arange(len(I))/fs

# -------- CARRIERS --------
c1 = np.cos(2*np.pi*fc*time)
c2 = np.sin(2*np.pi*fc*time)

# -------- QPSK MODULATION --------
qpsk = (2*I-1)*c1 + (2*Q-1)*c2

# -------- DEMODULATION --------
I_rec = (qpsk*c1 > 0).astype(int)
Q_rec = (qpsk*c2 > 0).astype(int)

reconstructed = np.ravel(np.column_stack((I_rec, Q_rec)))

# -------- PLOTS --------
plt.figure(figsize=(12,8))

plt.subplot(4,1,1)
plt.plot(time, I)
plt.title("Message Signal")
plt.ylim(-0.5,1.5); plt.grid()

plt.subplot(4,1,2)
plt.plot(time, c1)
plt.title("Carrier Signal")
plt.grid()

plt.subplot(4,1,3)
plt.plot(time, qpsk)
plt.title("QPSK Modulated Signal")
plt.grid()

plt.subplot(4,1,4)
plt.plot(time, reconstructed[:len(time)])
plt.title("Demodulated Signal")
plt.ylim(-0.5,1.5); plt.grid()

plt.tight_layout()
plt.show()
```
# Output Waveform
## PSK
![WhatsApp Image 2026-02-23 at 3 15 04 PM](https://github.com/user-attachments/assets/eae23202-c5c7-43f2-9e61-01b7f7cc3f9e)

## QPSK
![WhatsApp Image 2026-02-23 at 3 28 30 PM](https://github.com/user-attachments/assets/b6ef868a-b006-4b60-9a4d-f6bb87b14697)

# Results
Thus PSK and QPSK were performed and the waveform is verified using Google Colab.
