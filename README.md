# Frequency-Division-Multiplexing-FDM-

---

### Aim:

To simulate Frequency Division Multiplexing (FDM) and Demultiplexing in Scilab by generating six message signals, modulating them onto distinct carrier frequencies using amplitude modulation, combining them into a composite FDM signal, and recovering each original signal through coherent demodulation and filtering to verify proper separation.

---

### Apparatus Required:

- Computer with SCILAB software installed

---

### Theory:

Frequency Division Multiplexing (FDM) is a technique in which multiple message signals are transmitted simultaneously over a single communication channel by assigning each signal a unique carrier frequency. Each message is modulated with its respective carrier so that their frequency bands do not overlap. These modulated signals are then combined to form a single multiplexed signal for transmission. At the receiver end, the signal is demultiplexed by using the same carrier frequencies for demodulation, followed by low-pass filtering to recover the original baseband signals. FDM is widely used in radio broadcasting, cable television, and satellite communication systems where efficient bandwidth utilization is essential.

---

### Algorithm:

1. Initialize the simulation environment by clearing variables, closing all figures, and defining the sampling frequency and time vector.
2. Generate six message signals of different frequencies by creating sine waves using the time vector.
3. Assign six different carrier frequencies that are sufficiently spaced apart to avoid overlapping during multiplexing.
4. Modulate each message signal using Amplitude Modulation by multiplying each message with its corresponding cosine carrier.
5. Add all modulated signals to form a single composite Frequency Division Multiplexed (FDM) signal.
6. Display the original message signals using subplots for visual reference.
7. Display the combined FDM signal which contains all six channels transmitted together.
8. Design a low-pass FIR filter using a window method to extract the baseband message after demodulation.
9. Demodulate each channel by multiplying the FDM signal with its corresponding carrier and passing the product through the low-pass filter.
10. Plot all recovered signals to verify that each demultiplexed output matches its corresponding original message.

---

### Program:

```sci
clc;clear;close;

fs = 1000;
t = linspace(0, 1, fs);

freqs = [5 10 15 20 25 30];

signals = zeros(6, length(t));
for i = 1:6
    signals(i,:) = sin(2*%pi*freqs(i)*t);
end

fdm_signal = sum(signals, "r");

order = 51;
cutoff = 8 / (fs/2);    
h = wfir("lp", order, cutoff, "hm", "sum");

demux_signals = zeros(6, length(t));

for i=1:6
    mixed = fdm_signal .* sin(2*%pi*freqs(i)*t);
    temp = filter(h, 1, mixed);
    demux_signals(i,:) = temp(1:length(t));
end

scf(1); clf;
for i = 1:6
    subplot(3,2,i);
    plot(t, signals(i,:));
    title("Original Signal f=" + string(freqs(i)));
end

scf(2); clf;
plot(t, fdm_signal);
title("FDM Signal");

scf(3); clf;
for i = 1:6
    subplot(3,2,i);
    plot(t, demux_signals(i,:));
    title("Recovered f=" + string(freqs(i)));
end
```

---

### Output Waveform:

<img width="610" height="460" alt="image" src="https://github.com/user-attachments/assets/5164b238-0f17-427d-80aa-cec3cb50ec32" />

<img width="610" height="460" alt="image" src="https://github.com/user-attachments/assets/407c1f0b-b832-4a76-9bbb-1811ea3213ba" />

<img width="610" height="460" alt="image" src="https://github.com/user-attachments/assets/341ea55b-12b2-47ab-b3b6-06939e5db665" />

---

### Tabulation:



---

### Result:

FDM and demultiplexing of six message signals were successfully implemented in Scilab. All signals were clearly multiplexed using different carriers and accurately recovered through demodulation and filtering, confirming correct system operation.
