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

fs = 58400;
t = 0:1/fs:0.03;

m1 = 6.8*sin(2*%pi*534*t);
m2 = 6.9*sin(2*%pi*544*t);
m3 = 7.0*sin(2*%pi*554*t);
m4 = 7.1*sin(2*%pi*564*t);
m5 = 7.2*sin(2*%pi*574*t);
m6 = 7.3*sin(2*%pi*584*t);

fc = [5340 5440 5540 5640 5740 5840];

c1 = 13.6*cos(2*%pi*fc(1)*t);
c2 = 13.8*cos(2*%pi*fc(2)*t);
c3 = 14*cos(2*%pi*fc(3)*t);
c4 = 14.2*cos(2*%pi*fc(4)*t);
c5 = 14.4*cos(2*%pi*fc(5)*t);
c6 = 14.6*cos(2*%pi*fc(6)*t);

s1 = m1 .* c1;
s2 = m2 .* c2;
s3 = m3 .* c3;
s4 = m4 .* c4;
s5 = m5 .* c5;
s6 = m6 .* c6;

s = s1 + s2 + s3 + s4 + s5 + s6;

d1 = 2 * s .* c1;
d2 = 2 * s .* c2;
d3 = 2 * s .* c3;
d4 = 2 * s .* c4;
d5 = 2 * s .* c5;
d6 = 2 * s .* c6;

cutoff = 585;  

function y = fft_lowpass(x, cutoff, fs)
    N = length(x);
    X = fft(x);
    f = (0:N-1)*(fs/N);
    mask = (f <= cutoff);

    Y = X .* mask;
    y = real(ifft(Y));
endfunction

r1 = fft_lowpass(d1, cutoff, fs);
r2 = fft_lowpass(d2, cutoff, fs);
r3 = fft_lowpass(d3, cutoff, fs);
r4 = fft_lowpass(d4, cutoff, fs);
r5 = fft_lowpass(d5, cutoff, fs);
r6 = fft_lowpass(d6, cutoff, fs);

scf(1); clf;

subplot(6,2,1);  plot(t, m1);
subplot(6,2,3);  plot(t, m2);
subplot(6,2,5);  plot(t, m3);
subplot(6,2,7); plot(t, m4);
subplot(6,2,9); plot(t, m5);
subplot(6,2,11); plot(t, m6);

subplot(6,2,2);  plot(t, r1);
subplot(6,2,4);  plot(t, r2);
subplot(6,2,6);  plot(t, r3);
subplot(6,2,8); plot(t, r4);
subplot(6,2,10); plot(t, r5);
subplot(6,2,12); plot(t, r6);

scf(2); clf;
subplot(1,1,1);  plot(t, s);title("FDM Signal");
```

---

### Output Waveform:

<img width="1536" height="800" alt="image" src="https://github.com/user-attachments/assets/acc02c22-577d-4b7a-9271-95afa807af2e" />

<img width="1536" height="800" alt="image" src="https://github.com/user-attachments/assets/669ea06f-5e52-47db-aa1e-a981ae352fb5" />

---

### Tabulation:

<img width="911" height="1280" alt="image" src="https://github.com/user-attachments/assets/1fd99d0d-40a4-4e83-a948-d72cb51e424d" />

<img width="924" height="1280" alt="image" src="https://github.com/user-attachments/assets/f67ad249-a797-4294-8ace-2d4d9a4f997e" />

---

### Result:

FDM and demultiplexing of six message signals were successfully implemented in Scilab. All signals were clearly multiplexed using different carriers and accurately recovered through demodulation and filtering, confirming correct system operation.
