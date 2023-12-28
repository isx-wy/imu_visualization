Code to convert accelerometer IMU data to a visualized output.

Accelerometer IMU Data
Inertial measurement unit (IMU) data contains 9 different data traces that are exported as 1 csv file where each row
corresponds to 1 sample of the signal. The exported csv file is organized in 11 columns with the following headers:
• IMU Time (s)
• Acc x
• Acc y
• Acc z
• Ori yaw
• Ori pitch
• Ori roll
• Mag Time (s)
• Mag x
• Mag y
• Mag z
Columns 2 through 7 (Acc x to Ori roll) represent accelerometer (Acc) and orientation (Ori, i.e., attitude) data that is
sampled at 50 Hz. The timestamps for these data are in the first column (IMU Time (s)).
The last 3 columns represent magnetometer data that is sampled at 2.5 Hz. The timestamps for these last 3 columns
are in column 8 (Mag Time (s)).
Orientation data is derived from accelerometer data.
The units for these data are:
• Acc: g
• Ori: radians
• Mag: gauss * 16384

Based on the following pseudocode:
csv_data = read_csv('imu.csv', columns = [0:3])
raw_acceleration = csv_data[1:3]
time = csv_data[0]
BA = sqrt(raw_acceleration[0]^2 + raw_acceleration[1]^2 + raw_acceleration[2]^2 )
filtered_BA = filtfilt_butterworth(BA, crit_freq = 5, type = 'highpass' )
thresh = otsu(filtered_BA)
movements = filtered_BA > thresh
