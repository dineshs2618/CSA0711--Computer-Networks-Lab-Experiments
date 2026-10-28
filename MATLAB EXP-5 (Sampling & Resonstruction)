clc;
clear;
close all;

% Signal Sampling and Reconstruction for Different Signals
f0 = 2;                    % Fundamental frequency in Hz
t = 0:0.001:1;             % Fine time vector for reference signals
Fs_high = 20;              % Higher sampling frequency in Hz
Fs_low = 3;                 % Low sampling frequency (undersampling)
Ts_high = 1/Fs_high;
Ts_low = 1/Fs_low;

% Generate different signals
x_sine = sin(2*pi*f0*t);
x_square = square(2*pi*f0*t);
x_triangle = sawtooth(2*pi*f0*t, 0.5);

signals = {x_sine, x_square, x_triangle};
signalNames = {'Sinusoidal Signal', 'Square Signal', 'Triangular Signal'};

% Sampling instants
th = 0:Ts_high:1;
tl = 0:Ts_low:1;

figure('Name','Signal Sampling and Reconstruction','Color','w');

for k = 1:3
    x = signals{k};

    % Sample the signal at the higher sampling frequency
    xh = interp1(t, x, th, 'nearest');
    % Sample the signal at the lower sampling frequency
    xl = interp1(t, x, tl, 'nearest');

    % Sinc interpolation reconstruction
    xrh = zeros(size(t));
    for n = 1:length(th)
        xrh = xrh + xh(n)*sinc(Fs_high*(t-th(n)));
    end

    xrl = zeros(size(t));
    for n = 1:length(tl)
        xrl = xrl + xl(n)*sinc(Fs_low*(t-tl(n)));
    end

    % Column 1: original signal
    subplot(3,3,(k-1)*3+1);
    plot(t,x,'LineWidth',1.2);
    grid on;
    title([signalNames{k} ' - Original']);
    xlabel('Time (s)');
    ylabel('Amplitude');

    % Column 2: higher-rate samples and reconstruction
    subplot(3,3,(k-1)*3+2);
    plot(t,xrh,'b','LineWidth',1.1); hold on;
    stem(th,xh,'r','filled');
    grid on;
    title(['Sampled and Reconstructed, Fs = ' num2str(Fs_high) ' Hz']);
    xlabel('Time (s)');
    ylabel('Amplitude');
    legend('Reconstruction','Samples','Location','best');

    % Column 3: low-rate samples and reconstruction
    subplot(3,3,(k-1)*3+3);
    plot(t,xrl,'b','LineWidth',1.1); hold on;
    stem(tl,xl,'r','filled');
    grid on;
    title(['Undersampled, Fs = ' num2str(Fs_low) ' Hz']);
    xlabel('Time (s)');
    ylabel('Amplitude');
    legend('Reconstruction','Samples','Location','best');
end

sgtitle('Analysis of Sampling and Reconstruction for Different Signals');
