clc;
clear;
close all;

% PCM encoding and decoding demonstration
fm = 5;                 % Message frequency in Hz
Fs = 100;               % Sampling frequency in Hz
A = 1;                  % Message amplitude
t = 0:1/5000:1;         % Fine time vector
tm = 0:1/Fs:1;          % Sampling instants

m = A*sin(2*pi*fm*t);   % Original message
ms = A*sin(2*pi*fm*tm); % Sampled message

nBits = 3;              % Number of bits per sample
L = 2^nBits;            % Number of quantization levels
xmin = -A;
xmax = A;
delta = (xmax-xmin)/L;

% Uniform quantization: map samples to level indices 0 ... L-1
index = floor((ms-xmin)/delta);
index(index < 0) = 0;
index(index > L-1) = L-1;
mq = xmin + (index + 0.5)*delta;  % Quantized sample values

% Encode each index as an nBits-wide binary word
codeWords = dec2bin(index, nBits);
disp('PCM code words (one row per sample):');
disp(codeWords);

% Decode code words back to integer indices and quantized values
decodedIndex = bin2dec(codeWords);
decoded = xmin + (decodedIndex + 0.5)*delta;

% Reconstruct the signal for visualization
mr = interp1(tm, decoded, t, 'linear', 'extrap');

figure('Color','w');
subplot(4,1,1);
plot(t,m,'LineWidth',1.2); grid on;
title('Original Message Signal'); xlabel('Time (s)'); ylabel('Amplitude');

subplot(4,1,2);
stem(tm,ms,'filled'); grid on;
title('Sampled Signal'); xlabel('Time (s)'); ylabel('Amplitude');

subplot(4,1,3);
stairs(tm,mq,'LineWidth',1.1); hold on;
stem(tm,mq,'filled'); grid on;
title(['Quantized Signal: ',num2str(nBits),' bits, ',num2str(L),' levels']);
xlabel('Time (s)'); ylabel('Amplitude');

subplot(4,1,4);
plot(t,m,'b','LineWidth',1.1); hold on;
plot(t,mr,'r--','LineWidth',1.1); grid on;
title('Original and PCM Reconstructed Signal');
xlabel('Time (s)'); ylabel('Amplitude');
legend('Original','Reconstructed','Location','best');

quantizationError = ms - decoded;
fprintf('Mean squared quantization error = %.6f\\n', mean(quantizationError.^2));
