# Flood-Detection-Algorithm-using-GEE
# Flood Detection and Population Impact Assessment Using SAR Imagery

A comprehensive approach for detecting flooded regions and estimating affected populations using Sentinel-1 SAR and Sentinel-2 optical satellite imagery, implemented on Google Earth Engine (GEE).

## Overview

This project addresses the challenge of flood detection in areas with high cloud cover, where traditional optical-based machine learning techniques fail to accurately identify flooded pixels. By leveraging Synthetic Aperture Radar (SAR) technology from Sentinel-1, this approach can penetrate clouds and detect flood inundation in previously invisible areas.

## Key Features

### Flood Detection
- **SAR-based approach**: Uses Sentinel-1 SAR data to overcome cloud cover limitations
- **Advanced noise filtering**: Implements speckle noise reduction techniques
- **Permanent water masking**: Two-step process using Hansen dataset and user-defined thresholds
- **Otsu thresholding**: Automated threshold determination for flood/non-flood pixel classification
- **Tile-based optimization**: Enhanced accuracy through segmented analysis using Ashman coefficient

### Population Impact Assessment
- **HRSL integration**: Uses High-Resolution Settlement Layer (~30m resolution) for population estimation
- **Affected population calculation**: Multiplies flood maps with population density data
- **Sub-regional analysis**: Provides granular affected population statistics

## Methodology

### 1. Flood Inundation Mapping
```
Input: Sentinel-1 SAR Images
  ↓
Speckle Noise Filtering
  ↓
Permanent Water Masking (Hansen Dataset + Threshold)
  ↓
Otsu Threshold Algorithm
  ↓
Output: Binary Flood Map (30m resolution)
```

### 2. Enhanced Tile-Based Approach
- Divide image into tiles
- Calculate Ashman coefficient for histogram separability
- Remove non-separable tiles (uniform features)
- Apply Otsu algorithm only to bimodal histogram tiles

### 3. Population Impact Assessment
```
Flood Map × HRSL Population Data = Affected Population Estimate
```

## Platform and Dependencies

- **Platform**: Google Earth Engine (GEE)
- **Primary Data Sources**:
  - Sentinel-1 SAR imagery
  - Sentinel-2 optical imagery (complementary)
  - Hansen Global Forest Change dataset
  - High-Resolution Settlement Layer (HRSL)

## Limitations and Considerations

### Technical Limitations
- **Urban area challenges**: Double-bounce scattering in urban environments can violate scattering assumptions
- **Rural area optimization**: Threshold-based algorithms perform better in rural settings
- **Gaussian distribution requirement**: Otsu algorithm effectiveness depends on Gaussian histogram distribution

### Population Estimation Limitations
- **Overestimation risks**:
  - Incomplete permanent water masking
  - Population displacement due to early warning systems
- **Resolution constraints**: Limited by 30m resolution of processed imagery

## Accuracy Improvements

### Recommended Enhancements
1. **Height Above Nearest Drainage (HAND)**: Use 10m threshold for non-flooded area masking
2. **Tile-based processing**: Implement Ashman coefficient-based tile selection
3. **Visual validation**: Compare results with RGB imagery for accuracy assessment
4. **Benchmark comparison**: Validate against ground truth or reference datasets

## Use Cases

- **Emergency Response**: Rapid flood extent mapping for disaster management
- **Population Assessment**: Estimate affected populations for resource allocation
- **Insurance Applications**: Flood damage assessment and claims processing
- **Research**: Climate change impact studies and flood pattern analysis

## Performance Characteristics

- **Temporal Resolution**: Near real-time processing capability
- **Spatial Resolution**: 30m after denoising
- **Coverage**: Global (limited by Sentinel-1 coverage)
- **Weather Independence**: Functions in cloudy conditions

## Implementation Notes

### For Rural Areas
- Standard Otsu thresholding typically sufficient
- Higher accuracy expected due to clearer water/land boundaries

### For Urban Areas
- Tile-based approach recommended
- Additional validation against optical imagery suggested
- Consider HAND mapping for improved accuracy

### For Mixed Environments
- Hybrid approach combining multiple validation methods
- Careful permanent water masking essential

## Future Improvements

1. **Machine Learning Integration**: Combine with ML techniques for enhanced accuracy
2. **Multi-sensor Fusion**: Better integration of SAR and optical data
3. **Real-time Processing**: Optimize for faster emergency response
4. **Validation Framework**: Develop comprehensive accuracy assessment protocols

## References

The methodology is based on established research in SAR-based flood detection, including works by:
- Landuyt et al. (2019) - SAR flood mapping assessment
- Hansen et al. (2013) - Global forest cover change
- Otsu (1979) - Threshold selection methods
- Chini et al. (2017) - Hierarchical SAR thresholding
- Schlaffer et al. (2015) - Multi-temporal SAR analysis

## Getting Started

1. Set up Google Earth Engine account and access
2. Import required datasets (Sentinel-1, HRSL, Hansen)
3. Implement speckle filtering and permanent water masking
4. Apply Otsu or tile-based thresholding algorithm
5. Multiply flood map with HRSL for population estimation
6. Validate results against available ground truth or optical imagery

## Contributing

When contributing to this project, please consider:
- Testing in both rural and urban environments
- Validating against multiple flood events
- Documenting performance metrics and limitations
- Sharing benchmark datasets for algorithm validation

---

*This project provides a foundation for SAR-based flood detection and can be adapted for various geographic regions and flood scenarios. The methodology balances automation with accuracy, making it suitable for both research and operational applications.*
