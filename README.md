# Long-term-Monitoring-Data-for-Pipeline
guided wave data
# README

# 1. Long-Term Pipeline Monitoring Data

## 1.1 Data Source

### 0.1 Pipeline Description

Experimental Object: A complex pipeline in an outdoor environment with multiple types of defects. The pipeline consists of two straight pipe sections and a 90-degree right-angle elbow welded in between:

- Pipe 1: Welded by 4 straight pipes each 10 meters long;

- Pipe 2: 10 meters long, with an inner diameter of 150mm and a wall thickness of 6mm.

### 0.2 Defect Description

In the initial state, the experimental pipeline has 5 welds (W1-W5), 15 iron-cobalt alloy strips, and 15 defects (D1-D15). Among them, D1-D4 are crack defects, D5-D8 are groove defects, D9-D12 are three-hole defects, and D13-D15 are uniform thinning defects. The defect sizes are shown in Table 1. The on-site monitoring scene and the layout of monitoring nodes are shown in Figure 2 [1].

Table 1
|Defect No.|Defect Type|Defect Size (mm)|
|---|---|---|
|D1-D4|Crack Defect|55*1.5|
|D5-D8|Groove Defect|Φ55*1.5|
|D9-D12|Three-Hole Defect|Φ10|
|D13-D15|Uniform Thinning Defect|50|

The main research object is the three-hole defect D9. The distance between D9 and monitoring node 2 is about 1.5m. Each hole of D9 has a diameter of 10mm, a center distance of 12mm, a maximum depth of 3mm, and it is a non-through hole. As of March 5, 2026, D9 has been expanded seven times in total. The first expansion method was drilling a hole at the center of the three-hole defect with a maximum depth of 2.7mm; the second expansion method was grinding at the junction of the two right holes with a maximum depth of 3.1mm; the third expansion continued grinding at this position to a maximum depth of 3.5mm; the fourth expansion ground the two right holes and their junction to a maximum depth of 4.1mm. The fifth expansion continued grinding the junction of the two right holes to a maximum depth of 4.4mm. The sixth expansion continued grinding the junction of the two right holes to a maximum depth of 4.6mm. The seventh expansion continued grinding the junction of the two right holes to a maximum depth of 5mm. The real-scene images of the first 5 expansion processes of D9 are shown in the figure below.

Fig1.D9 Expansion Process

(Note: The original image content is retained as is)

|Defect Type|Expansion Time|Defect Size|
|---|---|---|
|Three-Hole Defect (Before Expansion)|2023.11.10|Each hole of the three-hole defect has a diameter of 10mm, a center distance of 12mm, and a maximum depth of 3mm;|
|Three-Hole Defect (1st Expansion)|2024.6.20|Drilling a hole at the center of the three-hole defect with a maximum depth of 2.7mm|
|Three-Hole Defect (2nd Expansion)|2024.10.18|Grinding at the junction of the two right holes with a maximum depth of 3.1mm|
|Three-Hole Defect (3rd Expansion)|2025.1.24|Grinding at the junction of the two right holes with a maximum depth of 3.5mm|
|Three-Hole Defect (4th Expansion)|2025.3.24|Grinding at the junction of the two right holes with a maximum depth of 4.1mm|
|Weld Defect (Before Expansion 1)|2024.10.21|Radial length 15mm, axial length 8mm, maximum depth 2.6mm|
|Weld Defect (Before Expansion 2)|2024.10.21|Radial length 23mm, axial length 10mm, maximum depth 3mm|
|Weld Defect (1st Expansion)|2025.8.6|Radial length 28mm, axial length 13mm, maximum depth 3.6mm|
|Weld Defect (2nd Expansion)|2026.2.24|Radial length 32mm, axial length 15mm, maximum depth 3.9mm|
### 0.3 Data Acquisition System

Two monitoring nodes are deployed on the pipeline. Monitoring Node 1 is deployed 2.3m away from the elbow weld, and Monitoring Node 2 is deployed 10.5m away, meaning the two nodes are 8.2m apart. The dual-node layout can cover a larger monitoring range and reduce monitoring blind areas. Both monitoring nodes are equipped with clamp-on MsT sensors to excite/receive T(0,1) mode guided waves. The experiment uses a self-excitation and self-reception mode, with an excitation frequency of 40kHz, an excitation signal of square wave, and a cycle number of 1. To suppress random noise, each collected signal is averaged 100 times. The sampling frequency is 1MHz, and the sampling interval is 4 hours. The two monitoring nodes operate independently without interfering with each other. The positions of the monitoring nodes and defects are shown in the figure below:

Figure 2 Schematic Diagram of Monitoring Nodes and Defect Positions

(Note: The original image content is retained as is)

## 1.2 Introduction to Data Packages

### 1. Data Files

The time monitoring range of Node 1 data is from October 22, 2024 to February 10, 2026. The time monitoring range of Node 2 data is from November 10, 2023 to March 23, 2025.

The file structure of the dataset is shown in Table 3. Among them, Data Package_Node 2 contains data before and after five defect expansions of the three-hole defect D9 (txt files in the directory), which are stored in 6 folders respectively. Similarly, Data Package_Node 1 contains data before and after three defect expansions of the weld defect (txt files in the directory), which are stored in 3 folders respectively.

|Dataset Root Directory|File Type|Subdirectory Folders|Number of Data (pieces)|
|---|---|---|---|
|Data Package_Node 2|Folder|Before Defect Expansion_Node 2|1188|
|||1st Defect Expansion_Node 2|1190|
|||2nd Defect Expansion_Node 2|613|
|||3rd Defect Expansion_Node 2|565|
|||4th Defect Expansion_Node 2|265|
|Data Package_Node 1|Folder|1st Defect Expansion_Node 1|1310|
|||2nd Defect Expansion_Node 1|927|
### 2. File Naming Rules

The original data files are in txt format, and the file name indicates the time when the data was collected.

For example: 20241022131200.txt indicates that the data was collected at 13:12:00 on October 22, 2024.

### 3. Data Field Description

Each txt document contains two sets of array data, both of which are character-type data. The first "data" mainly stores guided wave signals, and the second "otherData" mainly stores equipment information, stored in high and low 8-bit format. The detailed description is as follows:

- (1) Guided Wave Signals: Stored in the "data" array, stored in [xxx]/[yyy] format in the original data, which needs to be split and extracted (it is recommended to use the regexp() function in regular expressions to remove the '[]' and split the long string of numbers by ','), and then converted from character-type data to numerical-type data;

- (2) Temperature: The 14th and 15th bits of the otherData array (i.e., the two numbers after '1,1,1,') represent temperature information. Temperature changes will cause phase drift and amplitude fluctuation of the guided wave signal;

Figure 3 Example of Temperature Data

(Note: The original image content is retained as is)

- (3) Power: Stored in the 6th and 7th bits of the otherData array, used to evaluate the long-term operation stability of the monitoring system;

Temperature and power can be converted by (high bit * 256 + low bit)/100[^footnote1]. Taking the temperature in Figure 3 as an example: (11, 240) is processed to get: (11 * 256 + 240) / 100 = 30.56℃

## 1.3 Data Processing Suggestions (Taking MATLAB as an Example)

1. First, read all .txt monitoring files in the specified folder, and complete splitting and character format conversion;

2. Splice the high 8-bit (odd-bit data) and low 8-bit (even-bit) data stored in the file into 16-bit guided wave signals. The processing of temperature and power is the same;

3. Separate temperature and power parameters from the data and store them as two mat files respectively;

4. Intercept the guided wave signal data with temperature ≤ 45℃ and store it as one mat file;

5. Load the 3 mat files, adopt 8th-order Butterworth filtering of "low-pass first and then high-pass", with a low-pass cutoff frequency of 55kHz and a high-pass cutoff frequency of 35kHz (the purpose is to filter out high-frequency noise and low-frequency interference), and extract the effective frequency band of T(0,1) mode guided waves;

6. Convert the original digital signal into physical units (mV);

7. Intercept the first 30,000 sampling points (i.e., the defect signal area in the near field (0-3m) of the pipeline) and draw a waveform diagram.

|% Draw time-domain signal diagram<br>x1=1:30000;%30000 indicates the number of points to draw, the maximum is 30020<br>x1=x1/1e6*3192/2;%3192 is the guided wave velocity<br>y1=data_e(1,:);%First set of signals<br>y2=data_e(2,:);%Second set of signals|
|---|
|Figure 4 Example of MATLAB Signal Conversion|
Figure 5 Time-Domain Signal Analysis of Monitoring Node 2 (0-3m, 26℃)

(Note: The original image content is retained as is)

The distance between D9 and monitoring node 2 is about 1.5m. Based on this position information, the 0-3m signal of monitoring node 2 is selected for analysis. When the temperature is 26℃, the typical time-domain signal analysis is shown in Figure 5. Within this range, excitation crosstalk, W3, iron-cobalt alloy strips, secondary reflection of W3, and echo signals of D9 can be clearly observed, and the signal quality is good.

Then select the 0-3m signal of monitoring node 1 for analysis. From Figure 6, excitation crosstalk, D5, iron-cobalt alloy strips, D6, W1 and W2 echo signals can be observed; from the figure, W4, iron-cobalt alloy strips, W2 and W1 echo signals can be observed, and the signal quality is good.

Figure 6 Time-Domain Signal Analysis of Monitoring Node 1

(Note: The original image content is retained as is)

# References:

[1]Gao, Xiang, et al. "Long-term monitoring experiment and data analysis of complex pipeline based on magnetostrictive guided wave cloud monitoring system." Measurement 254 (2025): 117897.

[^footnote1]: High and Low 8-Bit Splicing: When the hardware collects data, if the value exceeds 8 bits (0-255), it will be split into high 8 bits and low 8 bits for storage, which need to be restored by high 8 bits * 256 + low 8 bits.
