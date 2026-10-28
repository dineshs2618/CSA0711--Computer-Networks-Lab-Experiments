clc;
clear;
close all;

% PSK modulation: BPSK and QPSK
bits = [1 0 1 1 0 0 1 0];
fc = 10;                 % Carrier frequency in Hz
Fs = 1000;               % Sampling frequency in Hz
Tb = 0.1;                % Bit duration in seconds
Ns = round(Fs*Tb);       % Samples per bit
tbit = (0:Ns-1)/Fs;

% ---------------- BPSK ----------------
bpsk = [];
for k = 1:length(bits)
    if bits(k) == 1
        phase = 0;
    else
        phase = pi;
    end
    bpsk = [bpsk cos(2*pi*fc*tbit + phase)];
end
tb = (0:length(bpsk)-1)/Fs;

% ---------------- QPSK ----------------
% Pair bits: 00, 01, 10, 11 map to 0, pi/2, pi, 3*pi/2.
% This is one valid phase mapping convention.
qpskBits = reshape(bits,2,[])';
phases = zeros(1,size(qpskBits,1));
for k = 1:size(qpskBits,1)
    b1 = qpskBits(k,1);
    b2 = qpskBits(k,2);
    if b1 == 0 && b2 == 0
        phases(k) = 0;
    elseif b1 == 0 && b2 == 1
        phases(k) = pi/2;
    elseif b1 == 1 && b2 == 0
        phases(k) = pi;
    else
        phases(k) = 3*pi/2;
    end
end

Tsym = 2*Tb;
Nsym = round(Fs*Tsym);
tsym = (0:Nsym-1)/Fs;
qpsk = [];
for k = 1:length(phases)
    qpsk = [qpsk cos(2*pi*fc*tsym + phases(k))];
end
tq = (0:length(qpsk)-1)/Fs;

figure('Color','w');
subplot(3,1,1);
stairs(0:length(bits),[bits bits(end)],'LineWidth',1.2);
ylim([-0.2 1.2]); grid on;
title('Input Bit Sequence'); xlabel('Bit Index'); ylabel('Bit');

subplot(3,1,2);
plot(tb,bpsk,'LineWidth',1.0); grid on;
title('BPSK Signal: phases 0 and pi'); xlabel('Time (s)'); ylabel('Amplitude');

subplot(3,1,3);
plot(tq,qpsk,'LineWidth',1.0); grid on;
title('QPSK Signal: four distinct phases'); xlabel('Time (s)'); ylabel('Amplitude');

disp('QPSK bit pairs and assigned phases (radians):');
disp([qpskBits phases']);
