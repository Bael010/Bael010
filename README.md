- 👋 Hi, I’m @Bael010
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

% Load the text file containing the three-axis acceleration data
data = load('DLPF0calib.txt');
% Extract the z-axis data from the loaded file and limit to 512 points
z_axis_data = data(:, 3); % Assuming the z-axis is the third column
% Sampling rate
sampling_rate = 1024; % Hz
% Define the filter specifications
order = 4; % Filter order
cutoff_freq = 500; % Hz
% Normalize cutoff frequency
normalized_cutoff = cutoff_freq / (sampling_rate/2);
% Design the filter
[b, a] = butter(order, normalized_cutoff, 'low');
% Apply the filter to the time-domain signal
filtered_signal = filter(b, a, z_axis_data);
% Time axis
time_axis = (0:length(z_axis_data)-1) * (1 / sampling_rate);
% Plot the time-domain signal in a separate figure window
figure;
plot(time_axis, z_axis_data);
xlabel('Time (s)');
ylabel('Acceleration (m/s²)');
title('Time-Domain Signal');
% Perform FFT on the filtered signal
fft_signal = fft(filtered_signal);
% Generate frequency axis with normalized scale
frequency_axis = (0:length(fft_signal)-1) * (sampling_rate / 
length(fft_signal));
frequency_axis = frequency_axis(1:length(fft_signal)/2); % Limit to 
positive frequencies
% Plot the frequency spectrum in a separate figure window
figure;
plot(frequency_axis, abs(fft_signal(1:length(fft_signal)/2)) * 2 / 
length(fft_signal)); % Scale by 2/N to account for one-sided spectrum
xlabel('Frequency (Hz)');
ylabel('Acceleration Magnitude (m/s²)');
title('Frequency Spectrum');
xlim([0, 512]);
<!---
Bael010/Bael010 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
