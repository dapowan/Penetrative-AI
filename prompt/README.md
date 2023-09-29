# Penetrative-AI
Try to sense the user's activities and identify human heartbeats with ChatGPT! ChatGPT-4 is recommended.
## Activity Sensing

Follow the three steps:

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
2. Replace `$DATA_STEP$`, `$DATA_SATELLITE_COUNT$`, `$DATA_SATELLITE_SNR$`,`$DATA_WIFI_COUNT$`, and `$DATA_WIFI_LIST$` with your sensor data. Here are some examples you may try:
```
Sensor data:
1. Step count: 115.0/min.
2. Satellites detected: 2. Carrier-to-noise: 17.9dB.
3. Total WiFi APs scanned: 21. SSID list: ['SINGTEL-UU9A(5G)', 'eduroam', 'NTUSECURE', 'NTUGUEST', 'NTUGUEST', 'OCBCAPPS', 'OCBC Free WiFi Zone', 'SINGTEL-D7B6', 'YilinLikesTea', 'eduroam', 'NTUGUEST', 'NTUSECURE', 'NTUSECURE', 'Redmi Note 9', 'Phoenix', 'OCBC Free WiFi Zone', 'eduroam', 'HAP_F04482485', 'OCBCAPPS', 'PAIKSBIBIM NTU_EXT', 'MNMP'].
```
```
Sensor data:
1. Step count: 109.0/min.
2. Satellites detected: 0. Carrier-to-noise: 0.0dB.
3. Total WiFi APs scanned: 8. SSID list: ["Claudio's Galaxy S23", 'mkphone1', 'GlobalWiFi_0RORFC', 'Wireless@SGx', 'Galaxy S9f3b7', 'Wireless@SGx', 'GlobalWiFi_0QU8XG', 'Wireless@SGx'].
```
4. Chat with ChatGPT.

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
2. Replace `$DATA$` with your ECG data. Here are some examples you may try:
```
[945 959 964 961 960 961 954 956 953 957 952 975 970 980 945 963 923 994 1059 915 960 931 953 935 953 938 945 930 953 960 976 966 973 963 972 961 972 961 974 970 995 982 995 953 986 921 1109 1028 931 977 947 970 955 967 957 965 953 972 977 986 976 983 971 975 966 972 964 973 968 991 981 992 955 976 937 985 1078 929 964 945 958 947 958 951 956 950 954 961 975 967 971 966 966 961 961 955 961 954 967 973 977 967 955 944 953 919 1076 959 929 943 935 938 934 939 934 934 923 932 948 955 950 953 948 948 944 947 941 947 943 953 960 965 953 946 936 939 905 1078 960 926 943 935 941 939 945 940 936 931 948 962 963 964 962 961 959 959 956 959 957 963 975 982 976 963 951 955 915 1129 986 935 954 944 953 949 955 950 952 950 963 973]
```
The ground-truth R-peaks are `[1059, 1109, 1078, 1076, 1078, 1129]`
```
[975 952 976 960 985 984 1023 1019 1026 991 997 980 990 979 994 983 994 983 994 980 999 983 998 985 1010 1005 1017 974 1002 946 1180 1108 968 978 962 971 964 971 976 994 1016 1033 1022 993 980 973 979 977 985 981 982 979 984 977 983 976 985 978 994 997 1019 982 995 950 1068 1192 979 985 957 976 958 974 967 989 1001 1032 1029 1017 989 992 983 989 983 994 987 995 986 995 986 994 985 999 992 1020 1018 1025 987 1015 962 1151 1141 976 1005 976 994 978 990 983 1006 1013 1042 1041 1035 1008 1005 994 998 992 999 993 997 986 993 983 989 983 990 985 1006 1003 993 966 978 950 1186 1065 950 956 940 948 939 944 945 959 973 995 1005 994 966 955 946 947 947 950 951 950 949 948 946 945 945 942 943 943 952 962 968 942 944 920 973 1169 967 933 915 926 914 923 916 931]
```
The ground-truth R-peaks are `[1180, 1192, 1151, 1186, 1169]`

4. Chat with ChatGPT.
