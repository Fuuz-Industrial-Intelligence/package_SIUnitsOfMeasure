# SIUnits

SI (International System of Units) measurement units for the Fuuz Industrial Operations Platform. Includes metric units across 13 measurement categories plus 4 shared categories (Amount, Currency, Time, Frequency).

[![Fuuz Platform](https://img.shields.io/badge/Fuuz-Platform-blue)](https://fuuz.com)
![Version](https://img.shields.io/badge/version-1.0.0-green)
![Spec](https://img.shields.io/badge/spec-2.0.0-lightgrey)

## Overview

| | Count |
|---|---|
| **UnitTypes** | 17 (4 shared + 13 si) |
| **Units** | 110 |
| **Conversions** | 686 |
| **Package Version** | 1.0.0 |
| **Platform Version** | 2026.2.1.782 |

## Installation

### Prerequisites

- Fuuz Platform environment with package import access
- No existing Unit, UnitType, or UnitConversion records with conflicting IDs

> **Important:** If you have platform-seeded unit records (IDs prefixed with `seed`), delete them before importing. See [Cleanup](#cleanup-seeded-records) below.

### Import

1. Download `SIUnits@1.0.0.fuuz` from the [Releases](../../releases) page
2. Navigate to **Settings → Packages** in your Fuuz environment
3. Click **Import Package** and select the `.fuuz` file
4. Verify import completed without errors

> **Note:** Only install **one** unit package per environment. Do not install both `SIUnits` and `AllUnits` — they share unit IDs and will conflict.

## UnitType Naming Convention

UnitTypes use a **system suffix** to distinguish measurement systems, enabling screen-level filtering:

| Suffix | System | Example | Label |
|--------|--------|---------|-------|
| `SI` | International System (Metric) | `LengthSI` | Length (SI) |
| `IMP` | Imperial / US Customary | `LengthIMP` | Length (Imperial) |
| *(none)* | Shared (no system distinction) | `Time` | Time |

### Shared UnitTypes (no suffix)

These categories are identical across measurement systems:

| UnitType ID | Label | Rationale |
|-------------|-------|-----------|
| `Amount` | Amount | Counting — no measurement system |
| `Currency` | Currency | Financial — no measurement system |
| `Time` | Time | Identical in both SI and Imperial |
| `Frequency` | Frequency | Hz is universally used — no Imperial alternative |

### Screen Filtering

Use the UnitType ID suffix to filter unit dropdowns by measurement system:

```jsonata
/* Show only SI units in a select input */
unitTypeId.$contains("SI")

/* Show only Imperial units */
unitTypeId.$contains("IMP")

/* Show all units for a category (both systems) */
unitTypeId.$startsWith("Length")
```

## ID & Code Rename Reference

The Fuuz platform enforces **case-insensitive uniqueness** on both `id` and `code` fields. Several standard unit abbreviations collide when compared case-insensitively (e.g., `mN` millinewtons vs `MN` meganewtons). These have been renamed to ensure clean imports.

### Unit ID Renames

| Original ID | New ID | Unit | Reason |
|-------------|--------|------|--------|
| `MHz` | `megaHz` | Megahertz | Case collision with mHz (Millihertz) |
| `MJ` | `megaJ` | Megajoules | Case collision with mJ (Millijoules) |
| `MN` | `megaN` | Meganewtons | Case collision with mN (Millinewtons) |
| `MW` | `megaW` | Megawatts | Case collision with mW (Milliwatts) |
| `Nm` | `ntm` | Newton-meters | Case collision with nm (Nanometers) |
| `kN` | `kiloN` | Kilonewtons | Case collision with kn (Knots) |
| `mHz` | `milliHz` | Millihertz | Case collision with MHz (Megahertz) |
| `mJ` | `milliJ` | Millijoules | Case collision with MJ (Megajoules) |
| `mN` | `milliN` | Millinewtons | Case collision with MN (Meganewtons) |
| `mW` | `milliW` | Milliwatts | Case collision with MW (Megawatts) |
| `nm` | `nanom` | Nanometers | Case collision with Nm (Newton-meters) |

### Unit Code Renames

| Original Code | New Code | Unit | Reason |
|---------------|----------|------|--------|
| `MHz` | `MegaHz` | Megahertz | Case collision with mHz |
| `MJ` | `MegaJ` | Megajoules | Case collision with mJ |
| `MN` | `MegaN` | Meganewtons | Case collision with mN |
| `MW` | `MegaW` | Megawatts | Case collision with mW |

> **Convention:** Milli- prefixes keep their standard abbreviation (`mN`, `mJ`, `mW`, `mHz`). Mega- variants get the longer form (`MegaN`, `MegaJ`, `MegaW`, `MegaHz`) since they are less commonly used in day-to-day manufacturing.

## Package Contents

### UnitTypes

| ID | Label | Units |
|----|-------|-------|
| `Amount` | Amount | 4 |
| `AreaSI` | Area (SI) | 7 |
| `Currency` | Currency | 9 |
| `DensitySI` | Density (SI) | 4 |
| `EnergySI` | Energy (SI) | 10 |
| `FlowRateSI` | Flow Rate (SI) | 8 |
| `ForceSI` | Force (SI) | 4 |
| `Frequency` | Frequency | 6 |
| `LengthSI` | Length (SI) | 9 |
| `PowerSI` | Power (SI) | 5 |
| `PressureSI` | Pressure (SI) | 8 |
| `SpeedSI` | Speed (SI) | 2 |
| `TemperatureSI` | Temperature (SI) | 2 |
| `Time` | Time | 10 |
| `TorqueSI` | Torque (SI) | 2 |
| `VolumeSI` | Volume (SI) | 12 |
| `WeightSI` | Weight (SI) | 8 |

### Units by Category

### Amount (`Amount`)

| ID | Code | Name |
|------|------|------|
| `ea` | `ea` | Each |
| `pc` | `pc` | Pieces |
| `dz` | `dz` | Dozen |
| `gro` | `gro` | Gross |

### Area (SI) (`AreaSI`)

| ID | Code | Name |
|------|------|------|
| `mm2` | `mm²` | Square Millimeters |
| `cm2` | `cm²` | Square Centimeters |
| `dm2` | `dm²` | Square Decimeters |
| `m2` | `m²` | Square Meters |
| `dam2` | `dam²` | Square Decameters |
| `hm2` | `ha` | Hectares |
| `km2` | `km²` | Square Kilometers |

### Currency (`Currency`)

| ID | Code | Name |
|------|------|------|
| `USD` | `USD` | US Dollar |
| `EUR` | `EUR` | Euro |
| `GBP` | `GBP` | British Pound Sterling |
| `JPY` | `JPY` | Japanese Yen |
| `CAD` | `CAD` | Canadian Dollar |
| `AUD` | `AUD` | Australian Dollar |
| `CHF` | `CHF` | Swiss Franc |
| `CNY` | `CNY` | Chinese Yuan |
| `MXN` | `MXN` | Mexican Peso |

### Density (SI) (`DensitySI`)

| ID | Code | Name |
|------|------|------|
| `kgm3` | `kg/m³` | Kilograms per Cubic Meter |
| `gcm3` | `g/cm³` | Grams per Cubic Centimeter |
| `gmL` | `g/mL` | Grams per Milliliter |
| `kgL` | `kg/L` | Kilograms per Liter |

### Energy (SI) (`EnergySI`)

| ID | Code | Name |
|------|------|------|
| `milliJ` | `mJ` | Millijoules |
| `J` | `J` | Joules |
| `kJ` | `kJ` | Kilojoules |
| `megaJ` | `MegaJ` | Megajoules |
| `GJ` | `GJ` | Gigajoules |
| `Wh` | `Wh` | Watt-hours |
| `kWh` | `kWh` | Kilowatt-hours |
| `MWh` | `MWh` | Megawatt-hours |
| `cal` | `cal` | Calories |
| `kcal` | `kcal` | Kilocalories |

### Flow Rate (SI) (`FlowRateSI`)

| ID | Code | Name |
|------|------|------|
| `mLmin` | `mL/min` | Milliliters per Minute |
| `mLh` | `mL/h` | Milliliters per Hour |
| `Lmin` | `L/min` | Liters per Minute |
| `Lh` | `L/h` | Liters per Hour |
| `Ls` | `L/s` | Liters per Second |
| `m3h` | `m³/h` | Cubic Meters per Hour |
| `m3min` | `m³/min` | Cubic Meters per Minute |
| `m3s` | `m³/s` | Cubic Meters per Second |

### Force (SI) (`ForceSI`)

| ID | Code | Name |
|------|------|------|
| `milliN` | `mN` | Millinewtons |
| `N` | `N` | Newtons |
| `kiloN` | `kN` | Kilonewtons |
| `megaN` | `MegaN` | Meganewtons |

### Frequency (`Frequency`)

| ID | Code | Name |
|------|------|------|
| `milliHz` | `mHz` | Millihertz |
| `Hz` | `Hz` | Hertz |
| `kHz` | `kHz` | Kilohertz |
| `megaHz` | `MegaHz` | Megahertz |
| `GHz` | `GHz` | Gigahertz |
| `THz` | `THz` | Terahertz |

### Length (SI) (`LengthSI`)

| ID | Code | Name |
|------|------|------|
| `nanom` | `nm` | Nanometers |
| `um` | `µm` | Micrometers |
| `mm` | `mm` | Millimeters |
| `cm` | `cm` | Centimeters |
| `dm` | `dm` | Decimeters |
| `m` | `m` | Meters |
| `dam` | `dam` | Decameters |
| `hm` | `hm` | Hectometers |
| `km` | `km` | Kilometers |

### Power (SI) (`PowerSI`)

| ID | Code | Name |
|------|------|------|
| `milliW` | `mW` | Milliwatts |
| `W` | `W` | Watts |
| `kW` | `kW` | Kilowatts |
| `megaW` | `MegaW` | Megawatts |
| `GW` | `GW` | Gigawatts |

### Pressure (SI) (`PressureSI`)

| ID | Code | Name |
|------|------|------|
| `Pa` | `Pa` | Pascals |
| `hPa` | `hPa` | Hectopascals |
| `kPa` | `kPa` | Kilopascals |
| `MPa` | `MPa` | Megapascals |
| `GPa` | `GPa` | Gigapascals |
| `bar` | `bar` | Bar |
| `mbar` | `mbar` | Millibar |
| `atm` | `atm` | Atmospheres |

### Speed (SI) (`SpeedSI`)

| ID | Code | Name |
|------|------|------|
| `mps` | `m/s` | Meters per Second |
| `kmph` | `km/h` | Kilometers per Hour |

### Temperature (SI) (`TemperatureSI`)

| ID | Code | Name |
|------|------|------|
| `C` | `°C` | Celsius |
| `K` | `K` | Kelvin |

### Time (`Time`)

| ID | Code | Name |
|------|------|------|
| `ns` | `ns` | Nanoseconds |
| `us` | `µs` | Microseconds |
| `ms` | `ms` | Milliseconds |
| `s` | `s` | Seconds |
| `min` | `min` | Minutes |
| `h` | `h` | Hours |
| `d` | `d` | Days |
| `wk` | `wk` | Weeks |
| `mo` | `mo` | Months |
| `yr` | `yr` | Years |

### Torque (SI) (`TorqueSI`)

| ID | Code | Name |
|------|------|------|
| `ntm` | `N·m` | Newton-meters |
| `kNm` | `kN·m` | Kilonewton-meters |

### Volume (SI) (`VolumeSI`)

| ID | Code | Name |
|------|------|------|
| `uL` | `µL` | Microliters |
| `mL` | `mL` | Milliliters |
| `cL` | `cL` | Centiliters |
| `dL` | `dL` | Deciliters |
| `L` | `L` | Liters |
| `daL` | `daL` | Decaliters |
| `hL` | `hL` | Hectoliters |
| `kL` | `kL` | Kiloliters |
| `mm3` | `mm³` | Cubic Millimeters |
| `cm3` | `cm³` | Cubic Centimeters |
| `dm3` | `dm³` | Cubic Decimeters |
| `m3` | `m³` | Cubic Meters |

### Weight (SI) (`WeightSI`)

| ID | Code | Name |
|------|------|------|
| `ug` | `µg` | Micrograms |
| `mg` | `mg` | Milligrams |
| `cg` | `cg` | Centigrams |
| `g` | `g` | Grams |
| `dag` | `dag` | Decagrams |
| `hg` | `hg` | Hectograms |
| `kg` | `kg` | Kilograms |
| `mt` | `t` | Metric Ton |

## Conversion Factors

Total conversions: **686**

<details>
<summary>Click to expand full conversion table</summary>


### Amount

| Source | Target | Factor |
|--------|--------|--------|
| `dz` (Dozen) | `ea` (Each) | 12 |
| `dz` (Dozen) | `gro` (Gross) | 0.08333333333 |
| `dz` (Dozen) | `pc` (Pieces) | 12 |
| `ea` (Each) | `dz` (Dozen) | 0.08333333333 |
| `ea` (Each) | `gro` (Gross) | 0.006944444444 |
| `ea` (Each) | `pc` (Pieces) | 1 |
| `gro` (Gross) | `dz` (Dozen) | 12 |
| `gro` (Gross) | `ea` (Each) | 144 |
| `gro` (Gross) | `pc` (Pieces) | 144 |
| `pc` (Pieces) | `dz` (Dozen) | 0.08333333333 |
| `pc` (Pieces) | `ea` (Each) | 1 |
| `pc` (Pieces) | `gro` (Gross) | 0.006944444444 |

### AreaSI

| Source | Target | Factor |
|--------|--------|--------|
| `cm2` (Square Centimeters) | `dam2` (Square Decameters) | 1e-06 |
| `cm2` (Square Centimeters) | `dm2` (Square Decimeters) | 0.01 |
| `cm2` (Square Centimeters) | `hm2` (Hectares) | 1e-08 |
| `cm2` (Square Centimeters) | `km2` (Square Kilometers) | 1e-10 |
| `cm2` (Square Centimeters) | `m2` (Square Meters) | 0.0001 |
| `cm2` (Square Centimeters) | `mm2` (Square Millimeters) | 100 |
| `dam2` (Square Decameters) | `cm2` (Square Centimeters) | 1000000 |
| `dam2` (Square Decameters) | `dm2` (Square Decimeters) | 10000 |
| `dam2` (Square Decameters) | `hm2` (Hectares) | 0.01 |
| `dam2` (Square Decameters) | `km2` (Square Kilometers) | 0.0001 |
| `dam2` (Square Decameters) | `m2` (Square Meters) | 100 |
| `dam2` (Square Decameters) | `mm2` (Square Millimeters) | 100000000 |
| `dm2` (Square Decimeters) | `cm2` (Square Centimeters) | 100 |
| `dm2` (Square Decimeters) | `dam2` (Square Decameters) | 0.0001 |
| `dm2` (Square Decimeters) | `hm2` (Hectares) | 1e-06 |
| `dm2` (Square Decimeters) | `km2` (Square Kilometers) | 1e-08 |
| `dm2` (Square Decimeters) | `m2` (Square Meters) | 0.01 |
| `dm2` (Square Decimeters) | `mm2` (Square Millimeters) | 10000 |
| `hm2` (Hectares) | `cm2` (Square Centimeters) | 100000000 |
| `hm2` (Hectares) | `dam2` (Square Decameters) | 100 |
| `hm2` (Hectares) | `dm2` (Square Decimeters) | 1000000 |
| `hm2` (Hectares) | `km2` (Square Kilometers) | 0.01 |
| `hm2` (Hectares) | `m2` (Square Meters) | 10000 |
| `hm2` (Hectares) | `mm2` (Square Millimeters) | 10000000000 |
| `km2` (Square Kilometers) | `cm2` (Square Centimeters) | 10000000000 |
| `km2` (Square Kilometers) | `dam2` (Square Decameters) | 10000 |
| `km2` (Square Kilometers) | `dm2` (Square Decimeters) | 100000000 |
| `km2` (Square Kilometers) | `hm2` (Hectares) | 100 |
| `km2` (Square Kilometers) | `m2` (Square Meters) | 1000000 |
| `km2` (Square Kilometers) | `mm2` (Square Millimeters) | 1000000000000 |
| `m2` (Square Meters) | `cm2` (Square Centimeters) | 10000 |
| `m2` (Square Meters) | `dam2` (Square Decameters) | 0.01 |
| `m2` (Square Meters) | `dm2` (Square Decimeters) | 100 |
| `m2` (Square Meters) | `hm2` (Hectares) | 0.0001 |
| `m2` (Square Meters) | `km2` (Square Kilometers) | 1e-06 |
| `m2` (Square Meters) | `mm2` (Square Millimeters) | 1000000 |
| `mm2` (Square Millimeters) | `cm2` (Square Centimeters) | 0.01 |
| `mm2` (Square Millimeters) | `dam2` (Square Decameters) | 1e-08 |
| `mm2` (Square Millimeters) | `dm2` (Square Decimeters) | 0.0001 |
| `mm2` (Square Millimeters) | `hm2` (Hectares) | 1e-10 |
| `mm2` (Square Millimeters) | `km2` (Square Kilometers) | 1e-12 |
| `mm2` (Square Millimeters) | `m2` (Square Meters) | 1e-06 |

### DensitySI

| Source | Target | Factor |
|--------|--------|--------|
| `gcm3` (Grams per Cubic Centimeter) | `gmL` (Grams per Milliliter) | 1 |
| `gcm3` (Grams per Cubic Centimeter) | `kgL` (Kilograms per Liter) | 1 |
| `gcm3` (Grams per Cubic Centimeter) | `kgm3` (Kilograms per Cubic Meter) | 1000 |
| `gmL` (Grams per Milliliter) | `gcm3` (Grams per Cubic Centimeter) | 1 |
| `gmL` (Grams per Milliliter) | `kgL` (Kilograms per Liter) | 1 |
| `gmL` (Grams per Milliliter) | `kgm3` (Kilograms per Cubic Meter) | 1000 |
| `kgL` (Kilograms per Liter) | `gcm3` (Grams per Cubic Centimeter) | 1 |
| `kgL` (Kilograms per Liter) | `gmL` (Grams per Milliliter) | 1 |
| `kgL` (Kilograms per Liter) | `kgm3` (Kilograms per Cubic Meter) | 1000 |
| `kgm3` (Kilograms per Cubic Meter) | `gcm3` (Grams per Cubic Centimeter) | 0.001 |
| `kgm3` (Kilograms per Cubic Meter) | `gmL` (Grams per Milliliter) | 0.001 |
| `kgm3` (Kilograms per Cubic Meter) | `kgL` (Kilograms per Liter) | 0.001 |

### EnergySI

| Source | Target | Factor |
|--------|--------|--------|
| `GJ` (Gigajoules) | `J` (Joules) | 1000000000 |
| `GJ` (Gigajoules) | `MWh` (Megawatt-hours) | 0.2777777778 |
| `GJ` (Gigajoules) | `Wh` (Watt-hours) | 277777.7778 |
| `GJ` (Gigajoules) | `cal` (Calories) | 239005736.1 |
| `GJ` (Gigajoules) | `kJ` (Kilojoules) | 1000000 |
| `GJ` (Gigajoules) | `kWh` (Kilowatt-hours) | 277.7777778 |
| `GJ` (Gigajoules) | `kcal` (Kilocalories) | 239005.7361 |
| `GJ` (Gigajoules) | `megaJ` (Megajoules) | 1000 |
| `GJ` (Gigajoules) | `milliJ` (Millijoules) | 1000000000000 |
| `J` (Joules) | `GJ` (Gigajoules) | 1e-09 |
| `J` (Joules) | `MWh` (Megawatt-hours) | 2.777777778e-10 |
| `J` (Joules) | `Wh` (Watt-hours) | 0.0002777777778 |
| `J` (Joules) | `cal` (Calories) | 0.2390057361 |
| `J` (Joules) | `kJ` (Kilojoules) | 0.001 |
| `J` (Joules) | `kWh` (Kilowatt-hours) | 2.777777778e-07 |
| `J` (Joules) | `kcal` (Kilocalories) | 0.0002390057361 |
| `J` (Joules) | `megaJ` (Megajoules) | 1e-06 |
| `J` (Joules) | `milliJ` (Millijoules) | 1000 |
| `MWh` (Megawatt-hours) | `GJ` (Gigajoules) | 3.6 |
| `MWh` (Megawatt-hours) | `J` (Joules) | 3600000000 |
| `MWh` (Megawatt-hours) | `Wh` (Watt-hours) | 1000000 |
| `MWh` (Megawatt-hours) | `cal` (Calories) | 860420650.1 |
| `MWh` (Megawatt-hours) | `kJ` (Kilojoules) | 3600000 |
| `MWh` (Megawatt-hours) | `kWh` (Kilowatt-hours) | 1000 |
| `MWh` (Megawatt-hours) | `kcal` (Kilocalories) | 860420.6501 |
| `MWh` (Megawatt-hours) | `megaJ` (Megajoules) | 3600 |
| `MWh` (Megawatt-hours) | `milliJ` (Millijoules) | 3600000000000 |
| `Wh` (Watt-hours) | `GJ` (Gigajoules) | 3.6e-06 |
| `Wh` (Watt-hours) | `J` (Joules) | 3600 |
| `Wh` (Watt-hours) | `MWh` (Megawatt-hours) | 1e-06 |
| `Wh` (Watt-hours) | `cal` (Calories) | 860.4206501 |
| `Wh` (Watt-hours) | `kJ` (Kilojoules) | 3.6 |
| `Wh` (Watt-hours) | `kWh` (Kilowatt-hours) | 0.001 |
| `Wh` (Watt-hours) | `kcal` (Kilocalories) | 0.8604206501 |
| `Wh` (Watt-hours) | `megaJ` (Megajoules) | 0.0036 |
| `Wh` (Watt-hours) | `milliJ` (Millijoules) | 3600000 |
| `cal` (Calories) | `GJ` (Gigajoules) | 4.184e-09 |
| `cal` (Calories) | `J` (Joules) | 4.184 |
| `cal` (Calories) | `MWh` (Megawatt-hours) | 1.162222222e-09 |
| `cal` (Calories) | `Wh` (Watt-hours) | 0.001162222222 |
| `cal` (Calories) | `kJ` (Kilojoules) | 0.004184 |
| `cal` (Calories) | `kWh` (Kilowatt-hours) | 1.162222222e-06 |
| `cal` (Calories) | `kcal` (Kilocalories) | 0.001 |
| `cal` (Calories) | `megaJ` (Megajoules) | 4.184e-06 |
| `cal` (Calories) | `milliJ` (Millijoules) | 4184 |
| `kJ` (Kilojoules) | `GJ` (Gigajoules) | 1e-06 |
| `kJ` (Kilojoules) | `J` (Joules) | 1000 |
| `kJ` (Kilojoules) | `MWh` (Megawatt-hours) | 2.777777778e-07 |
| `kJ` (Kilojoules) | `Wh` (Watt-hours) | 0.2777777778 |
| `kJ` (Kilojoules) | `cal` (Calories) | 239.0057361 |
| `kJ` (Kilojoules) | `kWh` (Kilowatt-hours) | 0.0002777777778 |
| `kJ` (Kilojoules) | `kcal` (Kilocalories) | 0.2390057361 |
| `kJ` (Kilojoules) | `megaJ` (Megajoules) | 0.001 |
| `kJ` (Kilojoules) | `milliJ` (Millijoules) | 1000000 |
| `kWh` (Kilowatt-hours) | `GJ` (Gigajoules) | 0.0036 |
| `kWh` (Kilowatt-hours) | `J` (Joules) | 3600000 |
| `kWh` (Kilowatt-hours) | `MWh` (Megawatt-hours) | 0.001 |
| `kWh` (Kilowatt-hours) | `Wh` (Watt-hours) | 1000 |
| `kWh` (Kilowatt-hours) | `cal` (Calories) | 860420.6501 |
| `kWh` (Kilowatt-hours) | `kJ` (Kilojoules) | 3600 |
| `kWh` (Kilowatt-hours) | `kcal` (Kilocalories) | 860.4206501 |
| `kWh` (Kilowatt-hours) | `megaJ` (Megajoules) | 3.6 |
| `kWh` (Kilowatt-hours) | `milliJ` (Millijoules) | 3600000000 |
| `kcal` (Kilocalories) | `GJ` (Gigajoules) | 4.184e-06 |
| `kcal` (Kilocalories) | `J` (Joules) | 4184 |
| `kcal` (Kilocalories) | `MWh` (Megawatt-hours) | 1.162222222e-06 |
| `kcal` (Kilocalories) | `Wh` (Watt-hours) | 1.162222222 |
| `kcal` (Kilocalories) | `cal` (Calories) | 1000 |
| `kcal` (Kilocalories) | `kJ` (Kilojoules) | 4.184 |
| `kcal` (Kilocalories) | `kWh` (Kilowatt-hours) | 0.001162222222 |
| `kcal` (Kilocalories) | `megaJ` (Megajoules) | 0.004184 |
| `kcal` (Kilocalories) | `milliJ` (Millijoules) | 4184000 |
| `megaJ` (Megajoules) | `GJ` (Gigajoules) | 0.001 |
| `megaJ` (Megajoules) | `J` (Joules) | 1000000 |
| `megaJ` (Megajoules) | `MWh` (Megawatt-hours) | 0.0002777777778 |
| `megaJ` (Megajoules) | `Wh` (Watt-hours) | 277.7777778 |
| `megaJ` (Megajoules) | `cal` (Calories) | 239005.7361 |
| `megaJ` (Megajoules) | `kJ` (Kilojoules) | 1000 |
| `megaJ` (Megajoules) | `kWh` (Kilowatt-hours) | 0.2777777778 |
| `megaJ` (Megajoules) | `kcal` (Kilocalories) | 239.0057361 |
| `megaJ` (Megajoules) | `milliJ` (Millijoules) | 1000000000 |
| `milliJ` (Millijoules) | `GJ` (Gigajoules) | 1e-12 |
| `milliJ` (Millijoules) | `J` (Joules) | 0.001 |
| `milliJ` (Millijoules) | `MWh` (Megawatt-hours) | 2.7777778e-13 |
| `milliJ` (Millijoules) | `Wh` (Watt-hours) | 2.777777778e-07 |
| `milliJ` (Millijoules) | `cal` (Calories) | 0.0002390057361 |
| `milliJ` (Millijoules) | `kJ` (Kilojoules) | 1e-06 |
| `milliJ` (Millijoules) | `kWh` (Kilowatt-hours) | 2.777777778e-10 |
| `milliJ` (Millijoules) | `kcal` (Kilocalories) | 2.390057361e-07 |
| `milliJ` (Millijoules) | `megaJ` (Megajoules) | 1e-09 |

### FlowRateSI

| Source | Target | Factor |
|--------|--------|--------|
| `Lh` (Liters per Hour) | `Lmin` (Liters per Minute) | 0.01666666667 |
| `Lh` (Liters per Hour) | `Ls` (Liters per Second) | 0.0002777777778 |
| `Lh` (Liters per Hour) | `m3h` (Cubic Meters per Hour) | 0.001 |
| `Lh` (Liters per Hour) | `m3min` (Cubic Meters per Minute) | 1.666666667e-05 |
| `Lh` (Liters per Hour) | `m3s` (Cubic Meters per Second) | 2.777777778e-07 |
| `Lh` (Liters per Hour) | `mLh` (Milliliters per Hour) | 1000 |
| `Lh` (Liters per Hour) | `mLmin` (Milliliters per Minute) | 16.66666667 |
| `Lmin` (Liters per Minute) | `Lh` (Liters per Hour) | 60 |
| `Lmin` (Liters per Minute) | `Ls` (Liters per Second) | 0.01666666667 |
| `Lmin` (Liters per Minute) | `m3h` (Cubic Meters per Hour) | 0.06 |
| `Lmin` (Liters per Minute) | `m3min` (Cubic Meters per Minute) | 0.001 |
| `Lmin` (Liters per Minute) | `m3s` (Cubic Meters per Second) | 1.666666667e-05 |
| `Lmin` (Liters per Minute) | `mLh` (Milliliters per Hour) | 60000 |
| `Lmin` (Liters per Minute) | `mLmin` (Milliliters per Minute) | 1000 |
| `Ls` (Liters per Second) | `Lh` (Liters per Hour) | 3600 |
| `Ls` (Liters per Second) | `Lmin` (Liters per Minute) | 60 |
| `Ls` (Liters per Second) | `m3h` (Cubic Meters per Hour) | 3.6 |
| `Ls` (Liters per Second) | `m3min` (Cubic Meters per Minute) | 0.06 |
| `Ls` (Liters per Second) | `m3s` (Cubic Meters per Second) | 0.001 |
| `Ls` (Liters per Second) | `mLh` (Milliliters per Hour) | 3600000 |
| `Ls` (Liters per Second) | `mLmin` (Milliliters per Minute) | 60000 |
| `m3h` (Cubic Meters per Hour) | `Lh` (Liters per Hour) | 1000 |
| `m3h` (Cubic Meters per Hour) | `Lmin` (Liters per Minute) | 16.66666667 |
| `m3h` (Cubic Meters per Hour) | `Ls` (Liters per Second) | 0.2777777778 |
| `m3h` (Cubic Meters per Hour) | `m3min` (Cubic Meters per Minute) | 0.01666666667 |
| `m3h` (Cubic Meters per Hour) | `m3s` (Cubic Meters per Second) | 0.0002777777778 |
| `m3h` (Cubic Meters per Hour) | `mLh` (Milliliters per Hour) | 1000000 |
| `m3h` (Cubic Meters per Hour) | `mLmin` (Milliliters per Minute) | 16666.66667 |
| `m3min` (Cubic Meters per Minute) | `Lh` (Liters per Hour) | 60000 |
| `m3min` (Cubic Meters per Minute) | `Lmin` (Liters per Minute) | 1000 |
| `m3min` (Cubic Meters per Minute) | `Ls` (Liters per Second) | 16.66666667 |
| `m3min` (Cubic Meters per Minute) | `m3h` (Cubic Meters per Hour) | 60 |
| `m3min` (Cubic Meters per Minute) | `m3s` (Cubic Meters per Second) | 0.01666666667 |
| `m3min` (Cubic Meters per Minute) | `mLh` (Milliliters per Hour) | 60000000 |
| `m3min` (Cubic Meters per Minute) | `mLmin` (Milliliters per Minute) | 1000000 |
| `m3s` (Cubic Meters per Second) | `Lh` (Liters per Hour) | 3600000 |
| `m3s` (Cubic Meters per Second) | `Lmin` (Liters per Minute) | 60000 |
| `m3s` (Cubic Meters per Second) | `Ls` (Liters per Second) | 1000 |
| `m3s` (Cubic Meters per Second) | `m3h` (Cubic Meters per Hour) | 3600 |
| `m3s` (Cubic Meters per Second) | `m3min` (Cubic Meters per Minute) | 60 |
| `m3s` (Cubic Meters per Second) | `mLh` (Milliliters per Hour) | 3600000000 |
| `m3s` (Cubic Meters per Second) | `mLmin` (Milliliters per Minute) | 60000000 |
| `mLh` (Milliliters per Hour) | `Lh` (Liters per Hour) | 0.001 |
| `mLh` (Milliliters per Hour) | `Lmin` (Liters per Minute) | 1.666666667e-05 |
| `mLh` (Milliliters per Hour) | `Ls` (Liters per Second) | 2.777777778e-07 |
| `mLh` (Milliliters per Hour) | `m3h` (Cubic Meters per Hour) | 1e-06 |
| `mLh` (Milliliters per Hour) | `m3min` (Cubic Meters per Minute) | 1.666666667e-08 |
| `mLh` (Milliliters per Hour) | `m3s` (Cubic Meters per Second) | 2.777777778e-10 |
| `mLh` (Milliliters per Hour) | `mLmin` (Milliliters per Minute) | 0.01666666667 |
| `mLmin` (Milliliters per Minute) | `Lh` (Liters per Hour) | 0.06 |
| `mLmin` (Milliliters per Minute) | `Lmin` (Liters per Minute) | 0.001 |
| `mLmin` (Milliliters per Minute) | `Ls` (Liters per Second) | 1.666666667e-05 |
| `mLmin` (Milliliters per Minute) | `m3h` (Cubic Meters per Hour) | 6e-05 |
| `mLmin` (Milliliters per Minute) | `m3min` (Cubic Meters per Minute) | 1e-06 |
| `mLmin` (Milliliters per Minute) | `m3s` (Cubic Meters per Second) | 1.666666667e-08 |
| `mLmin` (Milliliters per Minute) | `mLh` (Milliliters per Hour) | 60 |

### ForceSI

| Source | Target | Factor |
|--------|--------|--------|
| `N` (Newtons) | `kiloN` (Kilonewtons) | 0.001 |
| `N` (Newtons) | `megaN` (Meganewtons) | 1e-06 |
| `N` (Newtons) | `milliN` (Millinewtons) | 1000 |
| `kiloN` (Kilonewtons) | `N` (Newtons) | 1000 |
| `kiloN` (Kilonewtons) | `megaN` (Meganewtons) | 0.001 |
| `kiloN` (Kilonewtons) | `milliN` (Millinewtons) | 1000000 |
| `megaN` (Meganewtons) | `N` (Newtons) | 1000000 |
| `megaN` (Meganewtons) | `kiloN` (Kilonewtons) | 1000 |
| `megaN` (Meganewtons) | `milliN` (Millinewtons) | 1000000000 |
| `milliN` (Millinewtons) | `N` (Newtons) | 0.001 |
| `milliN` (Millinewtons) | `kiloN` (Kilonewtons) | 1e-06 |
| `milliN` (Millinewtons) | `megaN` (Meganewtons) | 1e-09 |

### Frequency

| Source | Target | Factor |
|--------|--------|--------|
| `GHz` (Gigahertz) | `Hz` (Hertz) | 1000000000 |
| `GHz` (Gigahertz) | `THz` (Terahertz) | 0.001 |
| `GHz` (Gigahertz) | `kHz` (Kilohertz) | 1000000 |
| `GHz` (Gigahertz) | `megaHz` (Megahertz) | 1000 |
| `GHz` (Gigahertz) | `milliHz` (Millihertz) | 1000000000000 |
| `Hz` (Hertz) | `GHz` (Gigahertz) | 1e-09 |
| `Hz` (Hertz) | `THz` (Terahertz) | 1e-12 |
| `Hz` (Hertz) | `kHz` (Kilohertz) | 0.001 |
| `Hz` (Hertz) | `megaHz` (Megahertz) | 1e-06 |
| `Hz` (Hertz) | `milliHz` (Millihertz) | 1000 |
| `THz` (Terahertz) | `GHz` (Gigahertz) | 1000 |
| `THz` (Terahertz) | `Hz` (Hertz) | 1000000000000 |
| `THz` (Terahertz) | `kHz` (Kilohertz) | 1000000000 |
| `THz` (Terahertz) | `megaHz` (Megahertz) | 1000000 |
| `THz` (Terahertz) | `milliHz` (Millihertz) | 1000000000000000.0 |
| `kHz` (Kilohertz) | `GHz` (Gigahertz) | 1e-06 |
| `kHz` (Kilohertz) | `Hz` (Hertz) | 1000 |
| `kHz` (Kilohertz) | `THz` (Terahertz) | 1e-09 |
| `kHz` (Kilohertz) | `megaHz` (Megahertz) | 0.001 |
| `kHz` (Kilohertz) | `milliHz` (Millihertz) | 1000000 |
| `megaHz` (Megahertz) | `GHz` (Gigahertz) | 0.001 |
| `megaHz` (Megahertz) | `Hz` (Hertz) | 1000000 |
| `megaHz` (Megahertz) | `THz` (Terahertz) | 1e-06 |
| `megaHz` (Megahertz) | `kHz` (Kilohertz) | 1000 |
| `megaHz` (Megahertz) | `milliHz` (Millihertz) | 1000000000 |
| `milliHz` (Millihertz) | `GHz` (Gigahertz) | 1e-12 |
| `milliHz` (Millihertz) | `Hz` (Hertz) | 0.001 |
| `milliHz` (Millihertz) | `THz` (Terahertz) | 1e-15 |
| `milliHz` (Millihertz) | `kHz` (Kilohertz) | 1e-06 |
| `milliHz` (Millihertz) | `megaHz` (Megahertz) | 1e-09 |

### LengthSI

| Source | Target | Factor |
|--------|--------|--------|
| `cm` (Centimeters) | `dam` (Decameters) | 0.001 |
| `cm` (Centimeters) | `dm` (Decimeters) | 0.1 |
| `cm` (Centimeters) | `hm` (Hectometers) | 0.0001 |
| `cm` (Centimeters) | `km` (Kilometers) | 9.99999257e-06 |
| `cm` (Centimeters) | `m` (Meters) | 0.01 |
| `cm` (Centimeters) | `mm` (Millimeters) | 10 |
| `cm` (Centimeters) | `nanom` (Nanometers) | 10000000 |
| `cm` (Centimeters) | `um` (Micrometers) | 10000 |
| `dam` (Decameters) | `cm` (Centimeters) | 1000 |
| `dam` (Decameters) | `dm` (Decimeters) | 100 |
| `dam` (Decameters) | `hm` (Hectometers) | 0.1 |
| `dam` (Decameters) | `km` (Kilometers) | 0.01 |
| `dam` (Decameters) | `m` (Meters) | 10 |
| `dam` (Decameters) | `mm` (Millimeters) | 10000 |
| `dam` (Decameters) | `nanom` (Nanometers) | 10000000000 |
| `dam` (Decameters) | `um` (Micrometers) | 10000000 |
| `dm` (Decimeters) | `cm` (Centimeters) | 10 |
| `dm` (Decimeters) | `dam` (Decameters) | 0.01 |
| `dm` (Decimeters) | `hm` (Hectometers) | 0.001 |
| `dm` (Decimeters) | `km` (Kilometers) | 0.0001 |
| `dm` (Decimeters) | `m` (Meters) | 0.1 |
| `dm` (Decimeters) | `mm` (Millimeters) | 100 |
| `dm` (Decimeters) | `nanom` (Nanometers) | 100000000 |
| `dm` (Decimeters) | `um` (Micrometers) | 100000 |
| `hm` (Hectometers) | `cm` (Centimeters) | 10000 |
| `hm` (Hectometers) | `dam` (Decameters) | 10 |
| `hm` (Hectometers) | `dm` (Decimeters) | 1000 |
| `hm` (Hectometers) | `km` (Kilometers) | 0.1 |
| `hm` (Hectometers) | `m` (Meters) | 100 |
| `hm` (Hectometers) | `mm` (Millimeters) | 100000 |
| `hm` (Hectometers) | `nanom` (Nanometers) | 100000000000 |
| `hm` (Hectometers) | `um` (Micrometers) | 100000000 |
| `km` (Kilometers) | `cm` (Centimeters) | 100000.0743 |
| `km` (Kilometers) | `dam` (Decameters) | 100 |
| `km` (Kilometers) | `dm` (Decimeters) | 10000 |
| `km` (Kilometers) | `hm` (Hectometers) | 10 |
| `km` (Kilometers) | `m` (Meters) | 1000 |
| `km` (Kilometers) | `mm` (Millimeters) | 1000000.743 |
| `km` (Kilometers) | `nanom` (Nanometers) | 1000000742981 |
| `km` (Kilometers) | `um` (Micrometers) | 1000000743 |
| `m` (Meters) | `cm` (Centimeters) | 100 |
| `m` (Meters) | `dam` (Decameters) | 0.1 |
| `m` (Meters) | `dm` (Decimeters) | 10 |
| `m` (Meters) | `hm` (Hectometers) | 0.01 |
| `m` (Meters) | `km` (Kilometers) | 0.001 |
| `m` (Meters) | `mm` (Millimeters) | 1000 |
| `m` (Meters) | `nanom` (Nanometers) | 1000000000 |
| `m` (Meters) | `um` (Micrometers) | 1000000 |
| `mm` (Millimeters) | `cm` (Centimeters) | 0.1 |
| `mm` (Millimeters) | `dam` (Decameters) | 0.0001 |
| `mm` (Millimeters) | `dm` (Decimeters) | 0.01 |
| `mm` (Millimeters) | `hm` (Hectometers) | 1e-05 |
| `mm` (Millimeters) | `km` (Kilometers) | 9.99999257e-07 |
| `mm` (Millimeters) | `m` (Meters) | 0.001 |
| `mm` (Millimeters) | `nanom` (Nanometers) | 1000000 |
| `mm` (Millimeters) | `um` (Micrometers) | 1000 |
| `nanom` (Nanometers) | `cm` (Centimeters) | 1e-07 |
| `nanom` (Nanometers) | `dam` (Decameters) | 1e-10 |
| `nanom` (Nanometers) | `dm` (Decimeters) | 1e-08 |
| `nanom` (Nanometers) | `hm` (Hectometers) | 1e-11 |
| `nanom` (Nanometers) | `km` (Kilometers) | 9.9999926e-13 |
| `nanom` (Nanometers) | `m` (Meters) | 1e-09 |
| `nanom` (Nanometers) | `mm` (Millimeters) | 1e-06 |
| `nanom` (Nanometers) | `um` (Micrometers) | 0.001 |
| `um` (Micrometers) | `cm` (Centimeters) | 0.0001 |
| `um` (Micrometers) | `dam` (Decameters) | 1e-07 |
| `um` (Micrometers) | `dm` (Decimeters) | 1e-05 |
| `um` (Micrometers) | `hm` (Hectometers) | 1e-08 |
| `um` (Micrometers) | `km` (Kilometers) | 9.99999257e-10 |
| `um` (Micrometers) | `m` (Meters) | 1e-06 |
| `um` (Micrometers) | `mm` (Millimeters) | 0.001 |
| `um` (Micrometers) | `nanom` (Nanometers) | 1000 |

### PowerSI

| Source | Target | Factor |
|--------|--------|--------|
| `GW` (Gigawatts) | `W` (Watts) | 1000000000 |
| `GW` (Gigawatts) | `kW` (Kilowatts) | 1000000 |
| `GW` (Gigawatts) | `megaW` (Megawatts) | 1000 |
| `GW` (Gigawatts) | `milliW` (Milliwatts) | 1000000000000 |
| `W` (Watts) | `GW` (Gigawatts) | 1e-09 |
| `W` (Watts) | `kW` (Kilowatts) | 0.001 |
| `W` (Watts) | `megaW` (Megawatts) | 1e-06 |
| `W` (Watts) | `milliW` (Milliwatts) | 1000 |
| `kW` (Kilowatts) | `GW` (Gigawatts) | 1e-06 |
| `kW` (Kilowatts) | `W` (Watts) | 1000 |
| `kW` (Kilowatts) | `megaW` (Megawatts) | 0.001 |
| `kW` (Kilowatts) | `milliW` (Milliwatts) | 1000000 |
| `megaW` (Megawatts) | `GW` (Gigawatts) | 0.001 |
| `megaW` (Megawatts) | `W` (Watts) | 1000000 |
| `megaW` (Megawatts) | `kW` (Kilowatts) | 1000 |
| `megaW` (Megawatts) | `milliW` (Milliwatts) | 1000000000 |
| `milliW` (Milliwatts) | `GW` (Gigawatts) | 1e-12 |
| `milliW` (Milliwatts) | `W` (Watts) | 0.001 |
| `milliW` (Milliwatts) | `kW` (Kilowatts) | 1e-06 |
| `milliW` (Milliwatts) | `megaW` (Megawatts) | 1e-09 |

### PressureSI

| Source | Target | Factor |
|--------|--------|--------|
| `GPa` (Gigapascals) | `MPa` (Megapascals) | 1000 |
| `GPa` (Gigapascals) | `Pa` (Pascals) | 1000000000 |
| `GPa` (Gigapascals) | `atm` (Atmospheres) | 9869.194392 |
| `GPa` (Gigapascals) | `bar` (Bar) | 10000 |
| `GPa` (Gigapascals) | `hPa` (Hectopascals) | 10000000 |
| `GPa` (Gigapascals) | `kPa` (Kilopascals) | 1000000 |
| `GPa` (Gigapascals) | `mbar` (Millibar) | 10000000 |
| `MPa` (Megapascals) | `GPa` (Gigapascals) | 0.001 |
| `MPa` (Megapascals) | `Pa` (Pascals) | 1000000 |
| `MPa` (Megapascals) | `atm` (Atmospheres) | 9.869194392 |
| `MPa` (Megapascals) | `bar` (Bar) | 10 |
| `MPa` (Megapascals) | `hPa` (Hectopascals) | 10000 |
| `MPa` (Megapascals) | `kPa` (Kilopascals) | 1000 |
| `MPa` (Megapascals) | `mbar` (Millibar) | 10000 |
| `Pa` (Pascals) | `GPa` (Gigapascals) | 1e-09 |
| `Pa` (Pascals) | `MPa` (Megapascals) | 1e-06 |
| `Pa` (Pascals) | `atm` (Atmospheres) | 9.869232667e-06 |
| `Pa` (Pascals) | `bar` (Bar) | 1e-05 |
| `Pa` (Pascals) | `hPa` (Hectopascals) | 0.01 |
| `Pa` (Pascals) | `kPa` (Kilopascals) | 0.001 |
| `Pa` (Pascals) | `mbar` (Millibar) | 0.01 |
| `atm` (Atmospheres) | `GPa` (Gigapascals) | 0.000101325393 |
| `atm` (Atmospheres) | `MPa` (Megapascals) | 0.101325393 |
| `atm` (Atmospheres) | `Pa` (Pascals) | 101325 |
| `atm` (Atmospheres) | `bar` (Bar) | 1.01325 |
| `atm` (Atmospheres) | `hPa` (Hectopascals) | 1013.25 |
| `atm` (Atmospheres) | `kPa` (Kilopascals) | 101.325393 |
| `atm` (Atmospheres) | `mbar` (Millibar) | 1013.25 |
| `bar` (Bar) | `GPa` (Gigapascals) | 0.0001 |
| `bar` (Bar) | `MPa` (Megapascals) | 0.1 |
| `bar` (Bar) | `Pa` (Pascals) | 100000 |
| `bar` (Bar) | `atm` (Atmospheres) | 0.9869232667 |
| `bar` (Bar) | `hPa` (Hectopascals) | 1000 |
| `bar` (Bar) | `kPa` (Kilopascals) | 100 |
| `bar` (Bar) | `mbar` (Millibar) | 1000 |
| `hPa` (Hectopascals) | `GPa` (Gigapascals) | 1e-07 |
| `hPa` (Hectopascals) | `MPa` (Megapascals) | 0.0001 |
| `hPa` (Hectopascals) | `Pa` (Pascals) | 100 |
| `hPa` (Hectopascals) | `atm` (Atmospheres) | 0.0009869232667 |
| `hPa` (Hectopascals) | `bar` (Bar) | 0.001 |
| `hPa` (Hectopascals) | `kPa` (Kilopascals) | 0.1 |
| `hPa` (Hectopascals) | `mbar` (Millibar) | 1 |
| `kPa` (Kilopascals) | `GPa` (Gigapascals) | 1e-06 |
| `kPa` (Kilopascals) | `MPa` (Megapascals) | 0.001 |
| `kPa` (Kilopascals) | `Pa` (Pascals) | 1000 |
| `kPa` (Kilopascals) | `atm` (Atmospheres) | 0.009869194392 |
| `kPa` (Kilopascals) | `bar` (Bar) | 0.01 |
| `kPa` (Kilopascals) | `hPa` (Hectopascals) | 10 |
| `kPa` (Kilopascals) | `mbar` (Millibar) | 10 |
| `mbar` (Millibar) | `GPa` (Gigapascals) | 1e-07 |
| `mbar` (Millibar) | `MPa` (Megapascals) | 0.0001 |
| `mbar` (Millibar) | `Pa` (Pascals) | 100 |
| `mbar` (Millibar) | `atm` (Atmospheres) | 0.0009869232667 |
| `mbar` (Millibar) | `bar` (Bar) | 0.001 |
| `mbar` (Millibar) | `hPa` (Hectopascals) | 1 |
| `mbar` (Millibar) | `kPa` (Kilopascals) | 0.1 |

### SpeedSI

| Source | Target | Factor |
|--------|--------|--------|
| `kmph` (Kilometers per Hour) | `mps` (Meters per Second) | 0.277778 |
| `mps` (Meters per Second) | `kmph` (Kilometers per Hour) | 3.59999712 |

### TemperatureSI

| Source | Target | Factor |
|--------|--------|--------|
| `C` (Celsius) | `K` (Kelvin) | 1 |
| `K` (Kelvin) | `C` (Celsius) | 1 |

### Time

| Source | Target | Factor |
|--------|--------|--------|
| `d` (Days) | `h` (Hours) | 24 |
| `d` (Days) | `min` (Minutes) | 1440 |
| `d` (Days) | `mo` (Months) | 0.03285420945 |
| `d` (Days) | `ms` (Milliseconds) | 86400000 |
| `d` (Days) | `ns` (Nanoseconds) | 86400000000000 |
| `d` (Days) | `s` (Seconds) | 86400 |
| `d` (Days) | `us` (Microseconds) | 86400000000 |
| `d` (Days) | `wk` (Weeks) | 0.1428571429 |
| `d` (Days) | `yr` (Years) | 0.002737850787 |
| `h` (Hours) | `d` (Days) | 0.04166666667 |
| `h` (Hours) | `min` (Minutes) | 60 |
| `h` (Hours) | `mo` (Months) | 0.001368925394 |
| `h` (Hours) | `ms` (Milliseconds) | 3600000 |
| `h` (Hours) | `ns` (Nanoseconds) | 3600000000000 |
| `h` (Hours) | `s` (Seconds) | 3600 |
| `h` (Hours) | `us` (Microseconds) | 3600000000 |
| `h` (Hours) | `wk` (Weeks) | 0.005952380952 |
| `h` (Hours) | `yr` (Years) | 0.0001140771161 |
| `min` (Minutes) | `d` (Days) | 0.0006944444444 |
| `min` (Minutes) | `h` (Hours) | 0.01666666667 |
| `min` (Minutes) | `mo` (Months) | 2.281542323e-05 |
| `min` (Minutes) | `ms` (Milliseconds) | 60000 |
| `min` (Minutes) | `ns` (Nanoseconds) | 60000000000 |
| `min` (Minutes) | `s` (Seconds) | 60 |
| `min` (Minutes) | `us` (Microseconds) | 60000000 |
| `min` (Minutes) | `wk` (Weeks) | 9.920634921e-05 |
| `min` (Minutes) | `yr` (Years) | 1.901285269e-06 |
| `mo` (Months) | `d` (Days) | 30.4375 |
| `mo` (Months) | `h` (Hours) | 730.5 |
| `mo` (Months) | `min` (Minutes) | 43830 |
| `mo` (Months) | `ms` (Milliseconds) | 2629800000 |
| `mo` (Months) | `ns` (Nanoseconds) | 2629800000000000.0 |
| `mo` (Months) | `s` (Seconds) | 2629800 |
| `mo` (Months) | `us` (Microseconds) | 2629800000000 |
| `mo` (Months) | `wk` (Weeks) | 4.348214286 |
| `mo` (Months) | `yr` (Years) | 0.08333333333 |
| `ms` (Milliseconds) | `d` (Days) | 1.157407407e-08 |
| `ms` (Milliseconds) | `h` (Hours) | 2.777777778e-07 |
| `ms` (Milliseconds) | `min` (Minutes) | 1.666666667e-05 |
| `ms` (Milliseconds) | `mo` (Months) | 3.802570538e-10 |
| `ms` (Milliseconds) | `ns` (Nanoseconds) | 1000000 |
| `ms` (Milliseconds) | `s` (Seconds) | 0.001 |
| `ms` (Milliseconds) | `us` (Microseconds) | 1000 |
| `ms` (Milliseconds) | `wk` (Weeks) | 1.653439153e-09 |
| `ms` (Milliseconds) | `yr` (Years) | 3.168808781e-11 |
| `ns` (Nanoseconds) | `d` (Days) | 1.157407e-14 |
| `ns` (Nanoseconds) | `h` (Hours) | 2.7777778e-13 |
| `ns` (Nanoseconds) | `min` (Minutes) | 1.666666667e-11 |
| `ns` (Nanoseconds) | `mo` (Months) | 3.8026e-16 |
| `ns` (Nanoseconds) | `ms` (Milliseconds) | 1e-06 |
| `ns` (Nanoseconds) | `s` (Seconds) | 1e-09 |
| `ns` (Nanoseconds) | `us` (Microseconds) | 0.001 |
| `ns` (Nanoseconds) | `wk` (Weeks) | 1.65344e-15 |
| `ns` (Nanoseconds) | `yr` (Years) | 3.169e-17 |
| `s` (Seconds) | `d` (Days) | 1.157407407e-05 |
| `s` (Seconds) | `h` (Hours) | 0.0002777777778 |
| `s` (Seconds) | `min` (Minutes) | 0.01666666667 |
| `s` (Seconds) | `mo` (Months) | 3.802570538e-07 |
| `s` (Seconds) | `ms` (Milliseconds) | 1000 |
| `s` (Seconds) | `ns` (Nanoseconds) | 1000000000 |
| `s` (Seconds) | `us` (Microseconds) | 1000000 |
| `s` (Seconds) | `wk` (Weeks) | 1.653439153e-06 |
| `s` (Seconds) | `yr` (Years) | 3.168808781e-08 |
| `us` (Microseconds) | `d` (Days) | 1.157407407e-11 |
| `us` (Microseconds) | `h` (Hours) | 2.777777778e-10 |
| `us` (Microseconds) | `min` (Minutes) | 1.666666667e-08 |
| `us` (Microseconds) | `mo` (Months) | 3.8025705e-13 |
| `us` (Microseconds) | `ms` (Milliseconds) | 0.001 |
| `us` (Microseconds) | `ns` (Nanoseconds) | 1000 |
| `us` (Microseconds) | `s` (Seconds) | 1e-06 |
| `us` (Microseconds) | `wk` (Weeks) | 1.65343915e-12 |
| `us` (Microseconds) | `yr` (Years) | 3.168809e-14 |
| `wk` (Weeks) | `d` (Days) | 7 |
| `wk` (Weeks) | `h` (Hours) | 168 |
| `wk` (Weeks) | `min` (Minutes) | 10080 |
| `wk` (Weeks) | `mo` (Months) | 0.2299794661 |
| `wk` (Weeks) | `ms` (Milliseconds) | 604800000 |
| `wk` (Weeks) | `ns` (Nanoseconds) | 604800000000000 |
| `wk` (Weeks) | `s` (Seconds) | 604800 |
| `wk` (Weeks) | `us` (Microseconds) | 604800000000 |
| `wk` (Weeks) | `yr` (Years) | 0.01916495551 |
| `yr` (Years) | `d` (Days) | 365.25 |
| `yr` (Years) | `h` (Hours) | 8766 |
| `yr` (Years) | `min` (Minutes) | 525960 |
| `yr` (Years) | `mo` (Months) | 12 |
| `yr` (Years) | `ms` (Milliseconds) | 31557600000 |
| `yr` (Years) | `ns` (Nanoseconds) | 31557600000000000 |
| `yr` (Years) | `s` (Seconds) | 31557600 |
| `yr` (Years) | `us` (Microseconds) | 31557600000000 |
| `yr` (Years) | `wk` (Weeks) | 52.17857143 |

### TorqueSI

| Source | Target | Factor |
|--------|--------|--------|
| `kNm` (Kilonewton-meters) | `ntm` (Newton-meters) | 1000 |
| `ntm` (Newton-meters) | `kNm` (Kilonewton-meters) | 0.001 |

### VolumeSI

| Source | Target | Factor |
|--------|--------|--------|
| `L` (Liters) | `cL` (Centiliters) | 100 |
| `L` (Liters) | `cm3` (Cubic Centimeters) | 1000 |
| `L` (Liters) | `dL` (Deciliters) | 10 |
| `L` (Liters) | `daL` (Decaliters) | 0.1 |
| `L` (Liters) | `dm3` (Cubic Decimeters) | 1 |
| `L` (Liters) | `hL` (Hectoliters) | 0.01 |
| `L` (Liters) | `kL` (Kiloliters) | 0.001 |
| `L` (Liters) | `m3` (Cubic Meters) | 0.001 |
| `L` (Liters) | `mL` (Milliliters) | 1000 |
| `L` (Liters) | `mm3` (Cubic Millimeters) | 1000000 |
| `L` (Liters) | `uL` (Microliters) | 1000000 |
| `cL` (Centiliters) | `L` (Liters) | 0.01 |
| `cL` (Centiliters) | `cm3` (Cubic Centimeters) | 10 |
| `cL` (Centiliters) | `dL` (Deciliters) | 0.1 |
| `cL` (Centiliters) | `daL` (Decaliters) | 0.001 |
| `cL` (Centiliters) | `dm3` (Cubic Decimeters) | 0.01 |
| `cL` (Centiliters) | `hL` (Hectoliters) | 0.0001 |
| `cL` (Centiliters) | `kL` (Kiloliters) | 1e-05 |
| `cL` (Centiliters) | `m3` (Cubic Meters) | 1e-05 |
| `cL` (Centiliters) | `mL` (Milliliters) | 10 |
| `cL` (Centiliters) | `mm3` (Cubic Millimeters) | 10000 |
| `cL` (Centiliters) | `uL` (Microliters) | 10000 |
| `cm3` (Cubic Centimeters) | `L` (Liters) | 0.001 |
| `cm3` (Cubic Centimeters) | `cL` (Centiliters) | 0.1 |
| `cm3` (Cubic Centimeters) | `dL` (Deciliters) | 0.01 |
| `cm3` (Cubic Centimeters) | `daL` (Decaliters) | 0.0001 |
| `cm3` (Cubic Centimeters) | `dm3` (Cubic Decimeters) | 0.001 |
| `cm3` (Cubic Centimeters) | `hL` (Hectoliters) | 1e-05 |
| `cm3` (Cubic Centimeters) | `kL` (Kiloliters) | 1e-06 |
| `cm3` (Cubic Centimeters) | `m3` (Cubic Meters) | 1e-06 |
| `cm3` (Cubic Centimeters) | `mL` (Milliliters) | 1 |
| `cm3` (Cubic Centimeters) | `mm3` (Cubic Millimeters) | 1000 |
| `cm3` (Cubic Centimeters) | `uL` (Microliters) | 1000 |
| `dL` (Deciliters) | `L` (Liters) | 0.1 |
| `dL` (Deciliters) | `cL` (Centiliters) | 10 |
| `dL` (Deciliters) | `cm3` (Cubic Centimeters) | 100 |
| `dL` (Deciliters) | `daL` (Decaliters) | 0.01 |
| `dL` (Deciliters) | `dm3` (Cubic Decimeters) | 0.1 |
| `dL` (Deciliters) | `hL` (Hectoliters) | 0.001 |
| `dL` (Deciliters) | `kL` (Kiloliters) | 0.0001 |
| `dL` (Deciliters) | `m3` (Cubic Meters) | 0.0001 |
| `dL` (Deciliters) | `mL` (Milliliters) | 100 |
| `dL` (Deciliters) | `mm3` (Cubic Millimeters) | 100000 |
| `dL` (Deciliters) | `uL` (Microliters) | 100000 |
| `daL` (Decaliters) | `L` (Liters) | 10 |
| `daL` (Decaliters) | `cL` (Centiliters) | 1000 |
| `daL` (Decaliters) | `cm3` (Cubic Centimeters) | 10000 |
| `daL` (Decaliters) | `dL` (Deciliters) | 100 |
| `daL` (Decaliters) | `dm3` (Cubic Decimeters) | 10 |
| `daL` (Decaliters) | `hL` (Hectoliters) | 0.1 |
| `daL` (Decaliters) | `kL` (Kiloliters) | 0.01 |
| `daL` (Decaliters) | `m3` (Cubic Meters) | 0.01 |
| `daL` (Decaliters) | `mL` (Milliliters) | 10000 |
| `daL` (Decaliters) | `mm3` (Cubic Millimeters) | 10000000 |
| `daL` (Decaliters) | `uL` (Microliters) | 10000000 |
| `dm3` (Cubic Decimeters) | `L` (Liters) | 1 |
| `dm3` (Cubic Decimeters) | `cL` (Centiliters) | 100 |
| `dm3` (Cubic Decimeters) | `cm3` (Cubic Centimeters) | 1000 |
| `dm3` (Cubic Decimeters) | `dL` (Deciliters) | 10 |
| `dm3` (Cubic Decimeters) | `daL` (Decaliters) | 0.1 |
| `dm3` (Cubic Decimeters) | `hL` (Hectoliters) | 0.01 |
| `dm3` (Cubic Decimeters) | `kL` (Kiloliters) | 0.001 |
| `dm3` (Cubic Decimeters) | `m3` (Cubic Meters) | 0.001 |
| `dm3` (Cubic Decimeters) | `mL` (Milliliters) | 1000 |
| `dm3` (Cubic Decimeters) | `mm3` (Cubic Millimeters) | 1000000 |
| `dm3` (Cubic Decimeters) | `uL` (Microliters) | 1000000 |
| `hL` (Hectoliters) | `L` (Liters) | 100 |
| `hL` (Hectoliters) | `cL` (Centiliters) | 10000 |
| `hL` (Hectoliters) | `cm3` (Cubic Centimeters) | 100000 |
| `hL` (Hectoliters) | `dL` (Deciliters) | 1000 |
| `hL` (Hectoliters) | `daL` (Decaliters) | 10 |
| `hL` (Hectoliters) | `dm3` (Cubic Decimeters) | 100 |
| `hL` (Hectoliters) | `kL` (Kiloliters) | 0.1 |
| `hL` (Hectoliters) | `m3` (Cubic Meters) | 0.1 |
| `hL` (Hectoliters) | `mL` (Milliliters) | 100000 |
| `hL` (Hectoliters) | `mm3` (Cubic Millimeters) | 100000000 |
| `hL` (Hectoliters) | `uL` (Microliters) | 100000000 |
| `kL` (Kiloliters) | `L` (Liters) | 1000 |
| `kL` (Kiloliters) | `cL` (Centiliters) | 100000 |
| `kL` (Kiloliters) | `cm3` (Cubic Centimeters) | 1000000 |
| `kL` (Kiloliters) | `dL` (Deciliters) | 10000 |
| `kL` (Kiloliters) | `daL` (Decaliters) | 100 |
| `kL` (Kiloliters) | `dm3` (Cubic Decimeters) | 1000 |
| `kL` (Kiloliters) | `hL` (Hectoliters) | 10 |
| `kL` (Kiloliters) | `m3` (Cubic Meters) | 1 |
| `kL` (Kiloliters) | `mL` (Milliliters) | 1000000 |
| `kL` (Kiloliters) | `mm3` (Cubic Millimeters) | 1000000000 |
| `kL` (Kiloliters) | `uL` (Microliters) | 1000000000 |
| `m3` (Cubic Meters) | `L` (Liters) | 1000 |
| `m3` (Cubic Meters) | `cL` (Centiliters) | 100000 |
| `m3` (Cubic Meters) | `cm3` (Cubic Centimeters) | 1000000 |
| `m3` (Cubic Meters) | `dL` (Deciliters) | 10000 |
| `m3` (Cubic Meters) | `daL` (Decaliters) | 100 |
| `m3` (Cubic Meters) | `dm3` (Cubic Decimeters) | 1000 |
| `m3` (Cubic Meters) | `hL` (Hectoliters) | 10 |
| `m3` (Cubic Meters) | `kL` (Kiloliters) | 1 |
| `m3` (Cubic Meters) | `mL` (Milliliters) | 1000000 |
| `m3` (Cubic Meters) | `mm3` (Cubic Millimeters) | 1000000000 |
| `m3` (Cubic Meters) | `uL` (Microliters) | 1000000000 |
| `mL` (Milliliters) | `L` (Liters) | 0.001 |
| `mL` (Milliliters) | `cL` (Centiliters) | 0.1 |
| `mL` (Milliliters) | `cm3` (Cubic Centimeters) | 1 |
| `mL` (Milliliters) | `dL` (Deciliters) | 0.01 |
| `mL` (Milliliters) | `daL` (Decaliters) | 0.0001 |
| `mL` (Milliliters) | `dm3` (Cubic Decimeters) | 0.001 |
| `mL` (Milliliters) | `hL` (Hectoliters) | 1e-05 |
| `mL` (Milliliters) | `kL` (Kiloliters) | 1e-06 |
| `mL` (Milliliters) | `m3` (Cubic Meters) | 1e-06 |
| `mL` (Milliliters) | `mm3` (Cubic Millimeters) | 1000 |
| `mL` (Milliliters) | `uL` (Microliters) | 1000 |
| `mm3` (Cubic Millimeters) | `L` (Liters) | 1e-06 |
| `mm3` (Cubic Millimeters) | `cL` (Centiliters) | 0.0001 |
| `mm3` (Cubic Millimeters) | `cm3` (Cubic Centimeters) | 0.001 |
| `mm3` (Cubic Millimeters) | `dL` (Deciliters) | 1e-05 |
| `mm3` (Cubic Millimeters) | `daL` (Decaliters) | 1e-07 |
| `mm3` (Cubic Millimeters) | `dm3` (Cubic Decimeters) | 1e-06 |
| `mm3` (Cubic Millimeters) | `hL` (Hectoliters) | 1e-08 |
| `mm3` (Cubic Millimeters) | `kL` (Kiloliters) | 1e-09 |
| `mm3` (Cubic Millimeters) | `m3` (Cubic Meters) | 1e-09 |
| `mm3` (Cubic Millimeters) | `mL` (Milliliters) | 0.001 |
| `mm3` (Cubic Millimeters) | `uL` (Microliters) | 1 |
| `uL` (Microliters) | `L` (Liters) | 1e-06 |
| `uL` (Microliters) | `cL` (Centiliters) | 0.0001 |
| `uL` (Microliters) | `cm3` (Cubic Centimeters) | 0.001 |
| `uL` (Microliters) | `dL` (Deciliters) | 1e-05 |
| `uL` (Microliters) | `daL` (Decaliters) | 1e-07 |
| `uL` (Microliters) | `dm3` (Cubic Decimeters) | 1e-06 |
| `uL` (Microliters) | `hL` (Hectoliters) | 1e-08 |
| `uL` (Microliters) | `kL` (Kiloliters) | 1e-09 |
| `uL` (Microliters) | `m3` (Cubic Meters) | 1e-09 |
| `uL` (Microliters) | `mL` (Milliliters) | 0.001 |
| `uL` (Microliters) | `mm3` (Cubic Millimeters) | 1 |

### WeightSI

| Source | Target | Factor |
|--------|--------|--------|
| `cg` (Centigrams) | `dag` (Decagrams) | 0.001 |
| `cg` (Centigrams) | `g` (Grams) | 0.01 |
| `cg` (Centigrams) | `hg` (Hectograms) | 0.0001 |
| `cg` (Centigrams) | `kg` (Kilograms) | 1e-05 |
| `cg` (Centigrams) | `mg` (Milligrams) | 10 |
| `cg` (Centigrams) | `mt` (Metric Ton) | 1e-08 |
| `cg` (Centigrams) | `ug` (Micrograms) | 10000 |
| `dag` (Decagrams) | `cg` (Centigrams) | 1000 |
| `dag` (Decagrams) | `g` (Grams) | 10 |
| `dag` (Decagrams) | `hg` (Hectograms) | 0.1 |
| `dag` (Decagrams) | `kg` (Kilograms) | 0.01 |
| `dag` (Decagrams) | `mg` (Milligrams) | 10000 |
| `dag` (Decagrams) | `mt` (Metric Ton) | 1e-05 |
| `dag` (Decagrams) | `ug` (Micrograms) | 10000000 |
| `g` (Grams) | `cg` (Centigrams) | 100 |
| `g` (Grams) | `dag` (Decagrams) | 0.1 |
| `g` (Grams) | `hg` (Hectograms) | 0.01 |
| `g` (Grams) | `kg` (Kilograms) | 0.001 |
| `g` (Grams) | `mg` (Milligrams) | 1000 |
| `g` (Grams) | `mt` (Metric Ton) | 1e-06 |
| `g` (Grams) | `ug` (Micrograms) | 1000000 |
| `hg` (Hectograms) | `cg` (Centigrams) | 10000 |
| `hg` (Hectograms) | `dag` (Decagrams) | 10 |
| `hg` (Hectograms) | `g` (Grams) | 100 |
| `hg` (Hectograms) | `kg` (Kilograms) | 0.1 |
| `hg` (Hectograms) | `mg` (Milligrams) | 100000.0661 |
| `hg` (Hectograms) | `mt` (Metric Ton) | 0.0001 |
| `hg` (Hectograms) | `ug` (Micrograms) | 100000066.1 |
| `kg` (Kilograms) | `cg` (Centigrams) | 100000 |
| `kg` (Kilograms) | `dag` (Decagrams) | 100 |
| `kg` (Kilograms) | `g` (Grams) | 1000 |
| `kg` (Kilograms) | `hg` (Hectograms) | 10 |
| `kg` (Kilograms) | `mg` (Milligrams) | 1000000.661 |
| `kg` (Kilograms) | `mt` (Metric Ton) | 0.001 |
| `kg` (Kilograms) | `ug` (Micrograms) | 1000000661 |
| `mg` (Milligrams) | `cg` (Centigrams) | 0.1 |
| `mg` (Milligrams) | `dag` (Decagrams) | 0.0001 |
| `mg` (Milligrams) | `g` (Grams) | 0.001 |
| `mg` (Milligrams) | `hg` (Hectograms) | 1e-05 |
| `mg` (Milligrams) | `kg` (Kilograms) | 9.999993386e-07 |
| `mg` (Milligrams) | `mt` (Metric Ton) | 1.000003197e-09 |
| `mg` (Milligrams) | `ug` (Micrograms) | 1000 |
| `mt` (Metric Ton) | `cg` (Centigrams) | 100000000 |
| `mt` (Metric Ton) | `dag` (Decagrams) | 100000 |
| `mt` (Metric Ton) | `g` (Grams) | 1000000 |
| `mt` (Metric Ton) | `hg` (Hectograms) | 10000 |
| `mt` (Metric Ton) | `kg` (Kilograms) | 1000 |
| `mt` (Metric Ton) | `mg` (Milligrams) | 1000000661 |
| `mt` (Metric Ton) | `ug` (Micrograms) | 1000000661387 |
| `ug` (Micrograms) | `cg` (Centigrams) | 0.0001 |
| `ug` (Micrograms) | `dag` (Decagrams) | 1e-07 |
| `ug` (Micrograms) | `g` (Grams) | 1e-06 |
| `ug` (Micrograms) | `hg` (Hectograms) | 1e-08 |
| `ug` (Micrograms) | `kg` (Kilograms) | 9.999993386e-10 |
| `ug` (Micrograms) | `mg` (Milligrams) | 0.001 |
| `ug` (Micrograms) | `mt` (Metric Ton) | 1.0000032e-12 |

</details>

## Cleanup Seeded Records

New Fuuz environments come with platform-seeded Unit, UnitType, and UnitConversion records that will conflict with package imports. **Delete these before importing.**

Run the three mutations in [`deleteSeededUnitData.graphql`](deleteSeededUnitData.graphql) **in order** using the Fuuz API Explorer:

1. **DeleteSeededUnitConversions** — removes 20 seeded conversion records
2. **DeleteSeededUnits** — removes 27 seeded unit records
3. **DeleteSeededUnitTypes** — removes 17 seeded unit type records

> **Order matters:** Conversions reference Units, which reference UnitTypes. Delete in the order above to avoid FK constraint errors.

## Package Structure

```
SIUnits@1.0.0.fuuz  (gzipped tarball)
├── manifest.json          # Package metadata
├── definition.json        # Selection definitions for import
└── package-data.json      # Seed data (UnitTypes, Units, Conversions)
```

Repository also includes:

```
├── deleteSeededUnitData.graphql  # Mutations to remove platform-seeded records
├── CHANGELOG.md                  # Version history
└── .gitignore
```

## Related Packages

| Package | Description | UnitTypes | Units | Conversions |
|---------|-------------|-----------|-------|-------------|
| [SIUnits](https://github.com/Fuuz-Industrial-Intelligence/SIUnits) | SI/Metric units only | 17 | 110 | 686 |
| [ImperialUnits](https://github.com/Fuuz-Industrial-Intelligence/ImperialUnits) | Imperial units only | 17 | 83 | 364 |
| [AllUnits](https://github.com/Fuuz-Industrial-Intelligence/AllUnits) | Both systems + cross-conversions | 30 | 164 | 1,720 |

> Install **only one** package per environment.

## License

Proprietary — [Fuuz Industrial Intelligence](https://fuuz.com)
