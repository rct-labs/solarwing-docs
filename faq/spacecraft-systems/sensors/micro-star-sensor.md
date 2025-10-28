# Micro Star Sensor (C-ST-MA-APS4-1) - Technical FAQ

## Overview

This document provides comprehensive technical answers about the Micro Star Sensor C-ST-MA-APS4-1, a high-precision attitude determination system designed for micro and nanosatellite platforms.

---

## What are the optical and imaging specifications?

The Micro Star Sensor utilizes an APS4 (Active Pixel Sensor 4) imaging system with the following detailed optical characteristics:

**Optical System:**
- Focal length: 25.4mm
- Aperture: f/2.8
- Field of view: 15° × 15°
- Spectral response: 400-700nm visible spectrum
- Stray light rejection: >10⁶:1
- Optical coatings: MgF₂ anti-reflective coating

**Imaging Sensor:**
- Detector type: CMOS APS4
- Pixel array: 1024 × 1024 pixels
- Pixel size: 5.5μm × 5.5μm
- Quantum efficiency: 65% peak at 550nm
- Read noise: <25e⁻ RMS
- Dark current: <0.5e⁻/pixel/sec at 25°C
- Full well capacity: 50,000e⁻

**Star Detection Performance:**
- Detection limit: Magnitude 6.5 (99.5% probability)
- Magnitude range: 0.0 to 6.5 Mv
- False detection rate: <0.1% per frame
- Processing time: <100ms for lost-in-space mode
- Update rate: 1Hz to 10Hz (configurable)

The optical system is optimized for space applications with radiation-hardened glass elements and a baffle system designed to reject Earth albedo and direct solar illumination up to 40° from the boresight.

---

## How does the attitude determination algorithm work?

The star sensor employs a sophisticated multi-stage algorithmic approach for accurate attitude determination:

**Lost-in-Space Mode:**
1. **Star Pattern Recognition**: Uses a geometric star triangle matching algorithm with a database of 48,000 reference stars (Hipparcos catalog)
2. **Initial Attitude Estimation**: Computes initial quaternion through singular value decomposition (SVD) of observed star vectors
3. **Verification**: Cross-references pattern matches with expected star magnitudes and positional tolerances

**Tracking Mode:**
1. **Star Field Correlation**: Tracks known star patterns using optical flow algorithms
2. **Predictive Tracking**: Utilizes Kalman filtering for attitude propagation between measurements
3. **Outlier Rejection**: Removes spurious detections through chi-squared statistical filtering

**Algorithm Specifications:**
- Catalog database: 48,000 stars down to magnitude 7.0
- Matching tolerance: ±0.1° angular separation
- Convergence time: <3 seconds from lost-in-space to tracking mode
- Memory requirements: 16MB for star catalog and algorithms
- Processing overhead: <15% CPU utilization

**Accuracy Factors:**
- Systematic error: <1.5″ (3σ) including optical distortions
- Random error: <0.5″ (3σ) from measurement noise
- Thermal stability: ±0.1″ accuracy variation across -25°C to +55°C
- Radiation degradation: <0.05″ accuracy loss after 5 years in LEO

The algorithm is implemented in radiation-hardened FPGAs with triple modular redundancy for critical computational paths, ensuring reliable operation throughout the mission lifetime.

---

## What are the electrical interfaces and power requirements?

The Micro Star Sensor provides comprehensive electrical interfaces optimized for spacecraft integration:

**Power Characteristics:**
- Supply voltage: +28V ±4V (spacecraft bus)
- Power consumption: 4.5W typical, 6.0W maximum
- Inrush current: <2A for <10ms during startup
- Power-on time: <2 seconds to operational mode

**Communication Interface:**
- Protocol: RS-422 (differential) standard
- Data rate: 115.2 kbps (configurable to 921.6 kbps)
- Connector: D-Sub 9-pin (MIL-DTL-38999 qualified)
- Signal levels: EIA-422-B compatible
- Cable impedance: 100Ω ±20% differential

**Data Output Format:**
- Primary data: Attitude quaternion (q0, q1, q2, q3)
- Angular velocity: 3-axis rate measurements
- Timestamp: GPS-coordinated time reference
- Health status: Temperature, voltage, current monitoring
- Star catalog match quality: Confidence metrics

**Electrical Specifications:**
- Operating voltage range: 22V to 32V DC
- Current draw: 160mA typical @ 28V
- Ground isolation: >10MΩ to chassis ground
- EMI/EMC compliance: MIL-STD-461E
- Surge protection: 40V transient tolerance
- Reverse polarity protection: Diode-protected input

**Environmental Tolerance:**
- Storage temperature: -20°C to +50°C
- Operating temperature: -25°C to +55°C
- Thermal cycling: Qualified for -40°C to +85°C
- Humidity: Non-condensing environment
- Vibration: 14.1g RMS random qualification level

The interface includes comprehensive fault detection and recovery mechanisms, with automatic restart capabilities and health monitoring telemetry for real-time system status assessment.

---

## What is the calibration procedure and accuracy verification?

The Micro Star Sensor undergoes rigorous calibration and verification procedures to ensure specified performance:

**Optical Calibration:**
- **Star Field Testing**: Laboratory verification using precision star simulator with magnitude accuracy of ±0.1 Mv
- **Geometric Calibration**: Grid plate measurements to determine focal length and principal point to ±0.01mm accuracy
- **Distortion Correction**: Radial and tangential distortion mapping with 10th-order polynomial correction
- **Flat Field Correction**: Pixel response non-uniformity correction to <1% variation

**Attitude Accuracy Verification:**
- **Static Testing**: Three-axis positioning table with 0.1″ angular resolution for ground-truth attitude reference
- **Dynamic Testing:**
  - Rate table testing up to 5°/s angular velocity
  - Slew maneuver testing for attitude determination latency
  - Vibration testing for optical stability verification
- **Environmental Testing:**
  - Thermal vacuum cycling (-40°C to +85°C) for optical focus stability
  - Radiation exposure testing for sensor degradation assessment

**Calibration Data Package:**
- Optical alignment matrices (intrinsic and extrinsic parameters)
- Temperature compensation coefficients for focus and alignment
- Star magnitude response curves across operating temperature range
- Error covariance matrices for attitude uncertainty quantification

**In-Orbit Calibration:**
- **Initial Calibration**: First 24 hours of operation for in-orbit parameter refinement
- **Periodic Recalibration**: Automatic star catalog updates based on long-term performance data
- **Health Monitoring**: Continuous assessment of attitude accuracy against predicted performance

**Performance Metrics:**
- Initial alignment accuracy: ±3″ (3σ) relative to spacecraft reference frame
- Long-term stability: ±0.5″ annual drift
- Calibration validity: 5 years without ground station intervention
- Verification confidence: 99.7% (3σ statistical confidence level)

The calibration process ensures that each unit meets the specified 3″ (3σ) accuracy requirement throughout the mission lifetime, with detailed documentation provided for integration verification and performance validation.