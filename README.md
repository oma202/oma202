clc             %clear command windows
clear           %clear workspace   
close all
a=arduino();    %reads the arduino
% Number of data points to read
s=fopen('a');
numDataPoints = 100; % Adjust as needed

% Initialize variables
time = zeros(1, numDataPoints);
ecgData = zeros(1, numDataPoints);

% Read and plot data
figure;

for i = 1:numDataPoints
    % Read data from the serial port
    
    data = fscanf(a,'%f');
    
    % Extract and store time and ECG data
    time(i) = data(1);
    ecgData(i) = data(2);
    
    % Plot the real-time ECG data
    plot(time, ecgData, '-o');
    title('Real-time ECG Data');
    xlabel('Time');
    ylabel('ECG Voltage (V)');
    
    drawnow; % Update the plot
    
    % Pause for a short duration to control the plot update rate
    pause(0.1);
end
