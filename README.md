# EXP.NO.9-Simulation-Sampling-and-multiplexing-in-PCM
9.Simulation of PCM

# AIM

To simulate the Pulse Code Modulation (PCM) of two analog signals with different frequencies, and to demonstrate Time Division Multiplexing (TDM) by interleaving their PCM samples using Python.

# SOFTWARE REQUIRED

Python Software 

-> Numpy Library

-> Matplotlib Library

-> Scipy Library (for signal processing)

# ALGORITHMS

Algorithm: PCM Modulation and TDM Multiplexing of Two Signals
Step 1: Initialize Parameters
Set sampling_rate, duration, and quantization_levels.

Define the frequencies frequency1 and frequency2 for the two message signals.

Step 2: Generate Time Base
Create a time vector t using np.linspace() based on sampling rate and duration.

Step 3: Generate Analog Message Signals
Compute:

message_signal1 = sin(2π * frequency1 * t)

message_signal2 = sin(2π * frequency2 * t)

Step 4: Quantize Message Signals
For each signal:

Find the quantization step size:
step = (max(signal) - min(signal)) / quantization_levels

Quantize the signal:
quantized = round(signal / step) * step

Normalize and convert to integer PCM values:
pcm = ((quantized - min(quantized)) / step).astype(int)

Step 5: Perform Time Division Multiplexing (TDM)
Interleave the PCM samples of the two signals:

Create an empty array multiplexed_pcm of size 2 * pcm_signal1.size.

Assign:

multiplexed_pcm[0::2] = pcm_signal1

multiplexed_pcm[1::2] = pcm_signal2

Step 6: Generate Clock Signal
Create a high-frequency clock signal (e.g., 200 Hz) for timing reference:

clock_signal = sign(sin(2π * 200 * t))

Step 7: Plot the Results
Use matplotlib to generate subplots for:

Message Signal 1

Clock Signal for Signal 1

Quantized Signal 1

Message Signal 2

Clock Signal for Signal 2

Quantized Signal 2

Combined Quantized Signals

Final Multiplexed PCM Signal
# PROGRAM


import matplotlib.pyplot as plt

import numpy as np

#Parameters

sampling_rate = 5000

duration = 0.1

quantization_levels = 16

#Time base

t = np.linspace(0, duration, int(sampling_rate * duration), endpoint=False)

#Two message signals

frequency1 = 50

frequency2 = 120

message_signal1 = np.sin(2 * np.pi * frequency1 * t)

message_signal2 = np.sin(2 * np.pi * frequency2 * t)

#Quantization

def quantize(signal, levels):

    step = (max(signal) - min(signal)) / levels
    
    quantized = np.round(signal / step) * step
    
    pcm = ((quantized - min(quantized)) / step).astype(int)
    
    return quantized, pcm


quantized_signal1, pcm_signal1 = quantize(message_signal1, quantization_levels)

quantized_signal2, pcm_signal2 = quantize(message_signal2, quantization_levels)

#Multiplexing the PCM signals

#Interleaving samples from both signals


multiplexed_pcm = np.empty((pcm_signal1.size + pcm_signal2.size,), dtype=int)

multiplexed_pcm[0::2] = pcm_signal1

multiplexed_pcm[1::2] = pcm_signal2

#Time base for multiplexed stream (double samples)
t_mux = np.linspace(0, duration, multiplexed_pcm.size, endpoint=False)

#Clock signal for reference

clock_signal = np.sign(np.sin(2 * np.pi * 200 * t))

#Plotting

plt.figure(figsize=(14, 12))

plt.subplot(8, 1, 1)

plt.plot(t, message_signal1, label="Message Signal 1 (50Hz)", color='blue')

plt.title("Original Message Signal 1")

plt.xlabel("Time [s]")

plt.ylabel("Amplitude")

plt.grid(True)

plt.legend()


plt.subplot(8, 1, 2)

plt.plot(t, clock_signal, label="Clock Signal", color='green')

plt.title("Clock Signal")

plt.xlabel("Time [s]")

plt.ylabel("Amplitude")

plt.grid(True)


plt.subplot(8, 1, 3)

plt.step(t, quantized_signal1, label="Quantized Signal 1", color='red')

plt.title("Quantized Signals")

plt.xlabel("Time [s]")

plt.ylabel("Amplitude")

plt.grid(True)

plt.legend()


plt.subplot(8, 1, 4)

plt.plot(t, message_signal2, label="Message Signal 2 (120Hz)", color='orange', alpha=0.7)

plt.title("Original Message Signal 2")

plt.xlabel("Time [s]")

plt.ylabel("Amplitude")

plt.grid(True)

plt.legend()


plt.subplot(8, 1, 5)

plt.plot(t, clock_signal, label="Clock Signal", color='green')

plt.title("Clock Signal")

plt.xlabel("Time [s]")

plt.ylabel("Amplitude")

plt.grid(True)


plt.subplot(8, 1, 6)

plt.step(t, quantized_signal2, label="Quantized Signal 2", color='purple', alpha=0.7)

plt.title("Quantized Signals")

plt.xlabel("Time [s]")


plt.ylabel("Amplitude")

plt.grid(True)

plt.legend()



plt.subplot(8, 1, 7)

plt.step(t, quantized_signal1, label="Quantized Signal 1", color='red')

plt.step(t, quantized_signal2, label="Quantized Signal 2", color='purple', alpha=0.7)

plt.title("Quantized Signals")

plt.xlabel("Time [s]")

plt.ylabel("Amplitude")

plt.grid(True)

plt.legend()



plt.subplot(8, 1, 8)

plt.step(t_mux, multiplexed_pcm, label="Multiplexed PCM Signal", color='black')

plt.title("Multiplexed PCM Signal (Interleaved)")

plt.xlabel("Time [s]")

plt.ylabel("PCM Value")

plt.grid(True)

plt.legend()



plt.tight_layout()

plt.show()



# OUTPUT

![PCM OUTPUT](https://github.com/user-attachments/assets/77bae5ba-d55a-42e6-8f71-b704bc6ec0dc)


 
# RESULT / CONCLUSIONS

Two distinct analog signals (50Hz and 120Hz) are successfully generated and quantized.

Their PCM representations are calculated and visualized.

A time-division multiplexed PCM signal is constructed by interleaving PCM values from both signals.

The output plots demonstrate:

Clear quantization of both signals.

Proper interleaving of PCM values for transmission in a multiplexed form.

A visual representation of how TDM works with PCM for efficient digital signal transmission.
