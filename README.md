# Penetrative-AI

## Activity Sensing

Try to sense the user's activities with ChatGPT! Follow the three steps:

1. Copy the following prompt.
```
Objective:
Determine a user's activity by analyzing sensor data from their smartphone.

Background:
Sensor data patterns vary based on the user's activity and environment. These patterns help in inferring the user's activity.

Sensor Data and Expert Knowledge:
You will receive data from various sensors, including the accelerometer, satellite, and WiFi. Here's how to interpret this data:
1. Step Count per Minute:
Source: Accelerometer (measures user's movement).
Interpretation: A high count signifies walking; a low count indicates the user is likely stationary.
2. Satellite Data:
Data: Number of satellites detected and average carrier-to-noise density (in dB).
Interpretation: High satellite count and carrier-to-noise density indicates an outdoor setting with strong satellite signals.
3. WiFi Data:
Data: Total count of WiFi Access Points (APs) detected and the list of their SSID.
Interpretation:
A large total count of detected APs suggests an indoor environment, given the prevalence of WiFi in modern buildings.
Scanned APs indicate user's proximity to them, and their SSIDs can hint at specific locations. So analyze each SSID. For example, a strong signal from an SSID named 'Starbucks' suggests the user is at a Starbucks. Note: Some SSIDs may be not meaningful.

Response Format:
Reasoning: Provide a comprehensive analysis of the sensor data.
Summary: Conclude with a brief summary of your findings.

Reasoning Example:
Sensor Data:
1. Step count: 5/min.
2. Satellites detected: 0. Carrier-to-noise: 0.0dB.
3. Total WiFi APs scanned: 10. SSID list: ['McDonald's Singapore', 'xiaomi_5G', 'McDonald's Singapore'].
Reasoning:
1. The low step count indicates the user is stationary.
2. No detected satellites and low carrier-to-noise suggest an indoor environment.
3. Detected WiFi APs point to an indoor setting, with SSIDs like 'McDonald's Singapore' hinting at a location close to McDonald restaurant in Singapore.
Summary: The user is stationary, likely close to a McDonald restaurant in Singapore.

Now infer a user's motion and surrounding conditions with the following sensor data:
Sensor data:
1. Step count: $DATA_STEP$/min.
2. Satellites detected: $DATA_SATELLITE_COUNT$. Carrier-to-noise: $DATA_SATELLITE_SNR$dB.
3. Total WiFi APs scanned: $DATA_WIFI_COUNT$. SSID list: $DATA_WIFI_LIST$.
Reasoning:
Summary:
```
2. Replace `$DATA_STEP$`, `$DATA_SATELLITE_COUNT$`, `$DATA_SATELLITE_SNR$`,`$DATA_WIFI_COUNT$`, and `$DATA_WIFI_LIST$` with your sensor data.
3. Chat with ChatGPT.

## Heartbeat Detection
1. Copy the following prompt.
```
Objective:
Find the R-peaks in an ECG waveform.

Background Knowledge:
An R-peak within a sequence of ECG numbers refers to a pronounced upward deflection, typically representing the largest and most conspicuous values within the sequence. To identify R-peaks, follow these steps:

1. Initial Observation: Begin by observing the rough overall range of ECG numbers in the provided data.

2. Identify Subsequences: Find subsequences of numbers that meet the following criteria:
2.1. The initial numbers are in the lower part of the overall range, even smaller than the range.
2.2. Subsequent numbers exhibit a significant increase, even exceeding the overall range.
2.3. Following the increase, subsequent numbers return to the overall range.

3. Select R-Peaks: After identifying these subsequences, select the largest number from each subsequence as an R-peak.

Response Format:
Your response should strictly adhere to the format detailed below:
Reasoning: Provide a reasoned explanation based on the information mentioned above about how the R-peaks were identified.
R-peaks: List the identified R-peaks numbers. List each instance separately, even if the same number appears multiple times, e.g., [R1, R2, R1] (each instance separately)

Reasoning Example:
ECG data: [944, 924, 941, 922, 933, 925, 955, 960, 974, 961, 967, 956, 966, 954, 967, 957, 971, 974, 988, 976, 976, 948, 968, 927, 1120, 975, 938, 949, 942, 942, 942, 941, 940, 939, 943, 945, 967, 968, 971, 965, 966, 958, 962, 953, 963, 957, 969, 974, 989, 974, 971, 949, 972, 918, 1117, 1005, 930, 960, 940, 953, 943, 950, 947, 947, 946, 956, 968, 975, 973, 972, 971, 966, 965, 964, 966, 966, 974, 985, 988, 978, 964, 958, 961, 940, 1111, 962, 945, 952, 948, 948, 948, 948, 949, 944, 945, 951, 969, 970, 973, 965, 970, 959, 966, 959, 966, 965, 988, 974, 986, 946, 980, 918, 1043, 1065, 914, 969, 934, 958, 936, 955, 940, 953, 934, 954, 969, 984, 978, 984, 975, 979, 970, 979, 973, 980, 985, 1001, 990, 983, 966, 979, 942, 1127, 992, 948, 966, 955, 963, 954, 959, 956, 956, 953, 975, 980, 988, 978, 984, 971, 976, 968, 978, 975, 999, 985, 1002, 960, 987, 931, 1043, 1139, 922, 977, 940, 966, 944, 964, 947, 959, 944, 960]
Reasoning:
Following the three steps by:
1. Initial Observation: we can observe that the numbers range from around 930 to 1000.
2. Identify Subsequences: we can identify several subsequences that start with numbers in the lower part of the range, significantly increase to exceed the range, and then return to the range:
- [927, 1120, 975, 938]
- [918, 1117, 1005, 930, 960]
- [940, 1111, 962, 945]
- [918, 1043, 1065, 914, 969]
- [942, 1127, 992, 948]
- [931, 1043, 1139, 922, 977]
3. Select R-Peaks: The R-peaks are [1120, 1117, 1111, 1065, 1127, 1139]
R-peaks: [1120, 1117, 1111, 1065, 1127, 1139]

Please identify the R-peaks in the provided ECG data. Do not write codes.
ECG data: $DATA$
```
2. Replace `$DATA$` with your ECG data.
3. Chat with ChatGPT.
