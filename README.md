# IIR-FILTER-DESIGN

# EXP 3 B: DESIGN OF LOW PASS CHEBYSHEV IIR FILTER USING BILINEAR TRANSFORMATION

# AIM: 

# To a design of low pass Chebyshev IIR filter using Bilinear Transformation.

# APPARATUS REQUIRED: 
PC installed with SCILAB. 

# PROGRAM: 
```
clc;
clear;
close;

// Input specifications
wp = input("Enter the pass band frequency (Radians) = ");
ws = input("Enter the stop band frequency (Radians) = ");
alphap = input("Enter the pass band attenuation (dB) = ");
alphas = input("Enter the stop band attenuation (dB) = ");
T = input("Enter the value of sampling time = ");

// Pre-warping using Bilinear Transformation
omegap = (2/T) * tan(wp/2);
disp(omegap, "omegap = ");

omegas = (2/T) * tan(ws/2);
disp(omegas, "omegas = ");

// Order of the Chebyshev Type-I filter
N = acosh(sqrt(((10^(0.1*alphas)) - 1) / ...
    ((10^(0.1*alphap)) - 1))) / acosh(omegas/omegap);

disp(N, "N = ");

N = ceil(N);
disp(N, "Round off value of N = ");

// Cut-off frequency
omegac = omegap / ...
    (((10^(0.1*alphap)) - 1)^(1/(2*N)));

disp(omegac, "omegac = ");

// Epsilon calculation
Epsilon = sqrt((10^(0.1*alphap)) - 1);
disp(Epsilon, "Epsilon = ");

// Find poles and gain of Chebyshev Type-I filter
[pols, gn] = zpch1(N, Epsilon, omegap);

disp(gn, "Gain = ");
disp(pols, "Poles = ");

// Analog Low Pass Chebyshev Filter Transfer Function
hs = poly(gn, "s", "coeff") / real(poly(pols, "s"));

disp(hs, "Analog Low Pass Chebyshev Filter Transfer Function = ");

// Define z variable
z = poly(0, "z");

// Bilinear Transformation
Hz = horner(hs, (2/T) * ((z - 1)/(z + 1)));

disp(Hz, "Digital LPF Transfer Function H(Z) = ");

// Frequency response
HW = frmag(Hz, 512);

// Frequency axis
w = 0:%pi/511:%pi;

// Plot frequency response
plot(w/%pi, abs(HW));

xlabel("Normalized Digital Frequency w");
ylabel("Magnitude");
title("Frequency Response of Chebyshev IIR LPF");
```

# OUTPUT: 
<img width="761" height="698" alt="WhatsApp Image 2026-09-01 at 14 23 50" src="https://github.com/user-attachments/assets/b2b3589f-4ceb-4084-9e88-9945204f02a4" />


# RESULT: 
Thus design of Chebyshev Low pass IIR filter waveforms were plotted and output was
verified.
