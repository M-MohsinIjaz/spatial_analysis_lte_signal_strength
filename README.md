
# **Spatial Data Analysis: RSRP Signal Strength in the UK**

This project analyzes the spatial patterns and relationships of RSRP (Reference Signal Received Power) measurements in the UK. It explores signal strength patterns, spatial autocorrelation, and the impact of distance to cell towers, utilizing various spatial data science techniques.

## **Table of Contents**

* Overview  
* Project Goals  
* Data  
* Installation  
* Key Analysis Steps  
* Results  
* Conclusion  
* Future Work  
* Acknowledgments

## **Overview**

The study uses RSRP data collected via drive testing and LTE cell tower locations from the OpenCellID dataset. Advanced spatial analysis techniques, including clustering, visualization, and prediction using Kriging, are applied to understand the relationship between signal strength and its spatial distribution.

## **Project Goals**

1. Analyze spatial patterns of RSRP measurements.  
2. Investigate the correlation between cell tower distance and signal strength.  
3. Predict RSRP values using spatial techniques.

## **Data**

* **RSRP Measurement Data**: Signal strength values collected via drive testing.  
* **LTE Cell Tower Data**: Cell tower locations from OpenCellID.  
* **Region of Interest**: Focused on a subset of the UK where measurements were collected.

## **Installation**

To run this project, install the required Python libraries:

bash  
Copy code  
`pip install geopandas`  
`pip install haversine`  
`pip install pykrige`  
`pip install pysal==2.4.0`  
`pip install pandas==1.3.3`  
`pip install numpy==1.21.2`  
`pip install folium==0.12.1`

## **Key Analysis Steps**

1. **Data Loading and Preprocessing**:  
   * Load RSRP and cell tower datasets.  
   * Reduce redundant data points and create GeoDataFrames for spatial processing.  
2. **Visualization**:  
   * Map RSRP measurement locations and cluster signal strengths.  
   * Visualize patterns and cluster analysis on interactive maps.  
3. **Spatial Autocorrelation**:  
   * Calculate Moran's I to evaluate spatial clustering of RSRP values.  
4. **Distance Analysis**:  
   * Investigate the relationship between RSRP values and proximity to cell towers.  
   * Assess overlapping coverage areas using circular visualization.  
5. **Prediction**:  
   * Predict RSRP values using:  
     * Nearest neighbor interpolation.  
     * Kriging (Ordinary and Universal).

## **Results**

1. **Spatial Autocorrelation**:  
   * Moran's I score of 0.76 indicates strong spatial clustering of similar RSRP values.  
2. **Impact of Distance**:  
   * No direct relationship between signal strength and cell tower distance due to overlapping coverage areas.  
3. **Prediction Accuracy**:  
   * Kriging techniques effectively predict RSRP values, leveraging spatial autocorrelation.

## **Conclusion**

* **Key Findings**:  
  * RSRP values exhibit strong spatial clustering.  
  * Distance alone is not a sufficient predictor of signal strength.  
  * Overlapping cell tower coverage complicates the relationship between distance and RSRP values.  
* **Implications**:  
  * Results provide valuable insights for telecom operators to optimize coverage.

## **Future Work**

* Analyze the effect of environmental factors (e.g., terrain, building density) on RSRP.  
* Extend the analysis to 5G networks.  
* Refine prediction models using additional features and machine learning techniques.

## **Acknowledgments**

* RSRP data sourced from Ofcom.  
* Cell tower locations provided by OpenCellID.  
* Libraries used: `pandas`, `geopandas`, `pysal`, `pykrige`, `folium`.

# Additional Information

## Additional Libraries Used

The following additional libraries have been utilized in this project:

- **`haversine`**: Used to calculate the distance between two geographical locations.
- **`pykrige`**: Used to perform Ordinary Kriging for spatial interpolation.

The first two cells in the project notebook install these additional libraries along with other required libraries at their appropriate versions.

## Cell Tower Dataset: OpenCellID

To determine the areas where network coverage is available in the UK, the project utilizes a freely available dataset on cell tower locations from [OpenCellID](https://opencellid.org/).  
- **Access Requirements**: 
  - Signup is required to download the dataset.
  - A token number is issued for downloading.
  - There is a daily limit on the number of downloads.
- **Dataset Size**: The complete dataset is over 3GB. However, only a subset focused on the UK is used in this project.
- **Updates**: The dataset is regularly updated by the OpenCellID team.

### Brief Description of the OpenCellID Dataset

| **Parameter**        | **Description**                                                                                                                |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------|
| `radio`              | Type of radio network (e.g., GSM, UMTS, LTE, CDMA).                                                                           |
| `mcc`                | Mobile Country Code.                                                                                                          |
| `mnc`                | Mobile Network Code. In the original dataset, this is named `net`, but it has been renamed to `mnc` in the subset dataset.    |
| `area`               | Location Area Code (LAC) for GSM and UMTS networks, Tracking Area Code (TAC) for LTE networks, or Network ID for CDMA.         |
| `cell`               | Cell ID.                                                                                                                      |
| `unit`               | Scrambling Code for UMTS or Physical Cell ID for LTE networks. Empty for GSM/CDMA.                                            |
| `lon`                | Longitude (degrees between -180.0 and 180.0).                                                                                  |
| `lat`                | Latitude (degrees between -90.0 and 90.0).                                                                                     |
| `range`              | Estimated cell range in meters.                                                                                               |
| `samples`            | Number of measurements assigned to the cell tower.                                                                            |
| `changeable`         | Indicates whether the coordinates of the tower are exact (`0`) or approximate (`1`).                                          |
| `created`            | Date and time when the tower was first added to the OpenCellID database.                                                      |
| `updated`            | Date and time of the last update to the cell tower information.                                                               |
| `averageSignal`      | Average signal strength across all assigned measurements for the cell.                                                        |

> **Note**: The combination of `mcc` and `mnc` provides information about the network operator. For example, `mcc=410` and `mnc=04` represent the Zong network.

## Signal Strength Dataset: Ofcom

The Ofcom dataset is a collection of signal strength measurements across various locations in the UK. It is provided by the UK's communications regulatory authority, Ofcom.

### Description of the Ofcom Dataset

| **Parameter**      | **Description**                                                                                                     |
|---------------------|---------------------------------------------------------------------------------------------------------------------|
| `latitude`         | Latitude of the location where the signal strength measurement was recorded.                                        |
| `longitude`        | Longitude of the location where the signal strength measurement was recorded.                                       |
| `rsrp_top1_3uk`    | RSRP (Reference Signal Received Power) value for the strongest signal from the 3UK network operator, measured in dBm. |
| `rsrp_top1_ee`     | RSRP value for the strongest signal from the EE network operator, measured in dBm.                                 |
| `rsrp_top1_o2`     | RSRP value for the strongest signal from the O2 network operator, measured in dBm.                                 |
| `rsrp_top1_vf`     | RSRP value for the strongest signal from the Vodafone network operator, measured in dBm.                           |

### Notes
- **RSRP** (Reference Signal Received Power) is a measure of the power of the received signal in dBm (decibel-milliwatts).
- This dataset aids in analyzing the spatial distribution of signal strengths for various network operators in the UK.
