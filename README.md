# OptimizingWearableSR

This pipeline outlines the process for determining the optimal sampling rate from a wearable biosensor. 

**Downsampling_Procedure.Rmd** is an R file that follows the pre-processing steps to remove artefact from the Empatica E4 BVP signal using the E4 IBI values and produce new IBI values for a decimated signal. 

Pre-processing to remove the Empatica E4 BVP signal uses the E4 IBI values. Pre-processing also includes reducing high-frequency components with a standard lowpass filter (IIR, Chebyshev order 8). The BVP signal is then decimated via rate reduction by an integer factor into 64Hz, 32Hz, 21Hz, 16Hz, 12.8Hz, 10.7Hz, 9.1Hz, 8Hz, 7.1Hz, and 6.4Hz.A Kolmogorev-Zurbenko low pass linear filter (https://onlinelibrary.wiley.com/doi/full/10.1002/wics.1419) is used for outlier removal in order to mitigate any additional artifact not removed in the pre-processing. 
To extract new IBI values for the decimated signal(s), local minima are detected using a rolling minimum detector and IBI values were calculated as the difference between these local minima values, as described by Empatica: https://support.empatica.com/hc/en-us/articles/201912319-How-is-IBI-csv-obtained-. Finally, outlier capping at 1.5xIQR was performed on each decimated signal. 

**PythonCodeforHRV.ipynb** is a Python notebook that calculates HRV metrics from RR intervals (ECG) or IBI (PPG). See more here: https://github.com/Big-Ideas-Lab/DBDP
