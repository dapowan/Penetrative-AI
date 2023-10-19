# Heartbeat Detection

## Overview
1. [Example-1](#example-1).
2. [Example-2](#example-2).

## Example-1

### Sensor Data:
```
ECG data: [945 959 964 961 960 961 954 956 953 957 952 975 970 980 945 963 923 994 1059 915 960 931 953 935 953 938 945 930 953 960 976 966 973 963 972 961 972 961 974 970 995 982 995 953 986 921 1109 1028 931 977 947 970 955 967 957 965 953 972 977 986 976 983 971 975 966 972 964 973 968 991 981 992 955 976 937 985 1078 929 964 945 958 947 958 951 956 950 954 961 975 967 971 966 966 961 961 955 961 954 967 973 977 967 955 944 953 919 1076 959 929 943 935 938 934 939 934 934 923 932 948 955 950 953 948 948 944 947 941 947 943 953 960 965 953 946 936 939 905 1078 960 926 943 935 941 939 945 940 936 931 948 962 963 964 962 961 959 959 956 959 957 963 975 982 976 963 951 955 915 1129 986 935 954 944 953 949 955 950 952 950 963 973]
```
### Full Prompt
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
Reasoning: Provide a reasoned explanation based on the information mentioned above about how the S-peaks were identified.
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
ECG data: [945 959 964 961 960 961 954 956 953 957 952 975 970 980 945 963 923 994 1059 915 960 931 953 935 953 938 945 930 953 960 976 966 973 963 972 961 972 961 974 970 995 982 995 953 986 921 1109 1028 931 977 947 970 955 967 957 965 953 972 977 986 976 983 971 975 966 972 964 973 968 991 981 992 955 976 937 985 1078 929 964 945 958 947 958 951 956 950 954 961 975 967 971 966 966 961 961 955 961 954 967 973 977 967 955 944 953 919 1076 959 929 943 935 938 934 939 934 934 923 932 948 955 950 953 948 948 944 947 941 947 943 953 960 965 953 946 936 939 905 1078 960 926 943 935 941 939 945 940 936 931 948 962 963 964 962 961 959 959 956 959 957 963 975 982 976 963 951 955 915 1129 986 935 954 944 953 949 955 950 952 950 963 973]
```
### Response from ChatGPT-4
```
Reasoning:
To identify the R-peaks in the provided ECG data, let's follow the three steps:
1. Initial Observation: By examining the ECG data, we can see that the numbers predominantly range from around the low 900s to the high 900s, with occasional excursions above 1000.
2. Identify Subsequences: Based on the above-mentioned criteria, we can identify subsequences that begin with numbers in the lower part of the range, then show a significant increase, and subsequently return to the original range:
[923, 994, 1059, 915, 960]
[921, 1109, 1028, 931, 977]
[937, 985, 1078, 929, 964]
[919, 1076, 959, 929]
[905, 1078, 960, 926]
[915, 1129, 986, 935]
3. Select R-Peaks: From the subsequences identified above, the R-peaks can be picked out by selecting the largest number in each subsequence:
R-peaks: [1059, 1109, 1078, 1076, 1078, 1129]

Response:
R-peaks: [1059, 1109, 1078, 1076, 1078, 1129]
```
ChatGPT [chat link](https://chat.openai.com/share/c8559dc2-d821-42d3-acd0-9cdf4b4bfd1e).
