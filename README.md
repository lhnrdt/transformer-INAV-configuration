# INAV CLI Diff Configuration

This repository contains an INAV CLI diff for the **JHEMCU F745** flight controller used on the hybrid aerial-ground vehicle.

- **Firmware**: INAV 8.0.1
- **Target**: INAV/JHEMCUF745

> ⚠️ This diff starts with `defaults noreboot` and resets the configuration to INAV defaults before applying changes. Always back up your config.

## 1. Files

- `INAV-diff.txt` - Full CLI diff for this vehicle.

## 2. Prerequisites

- INAV Configurator
- JHEMCU F745 running INAV 8.0.1
- USB cable  
- Remove propellers before setup

## 3. Back Up Your Configuration

In INAV Configurator → CLI:

```
diff all
```

Save the output to a file.

## 4. How to Load the Diff

1. Open `INAV-diff.txt`.
2. Copy all contents (including `batch start` and `save`).
3. Open INAV Configurator → CLI.
4. Paste everything.
5. Press Enter. The FC will reboot.

## 5. Post Load Checks

- Verify gyro, accelerometer, mag, barometer.
- Check receiver channels (CRSF).
- Verify motor order with props removed.
- Confirm battery voltage readings.
- Inspect failsafe behavior.

## 6. Summary of Key Changes

Only the essential modifications:

### Sensor and board configuration
- Sets IMU to **ICM42605**, barometer to **SPL06**, magnetometer to **QMC5883**.
- Custom **board alignment**: 180 deg roll, 90 deg yaw.
- Hardware specific **sensor offsets** applied.

### Receiver and serial setup
- **CRSF** selected as receiver protocol.
- UARTs configured for GPS, CRSF, MSP, and ESC telemetry.

### Motor and mixer configuration
- Motor protocol: **DSHOT600**
- Custom quad mixer for the hybrid vehicle layout
- Motor stop disabled (motors idle when armed)

### Battery and power
- Configured for a **6S 9500 mAh** LiPo
- Calibrated voltage scale and current meter

### Filters and flight profiles
- Gyro LPF around **110 Hz**
- RPM filtering enabled

## 7. Safety Notes

- This config is tuned for a specific prototype.
- If hardware differs, recalibrate sensors and battery settings.
- Always verify motor directions before arming.
