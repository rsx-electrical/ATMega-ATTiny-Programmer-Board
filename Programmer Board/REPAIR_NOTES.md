# Programmer board repair

The combined ProgrammerBoard project targets the Arduino Uno R3 header pattern. The ATmega and ATtiny sockets are on the top side. J1–J4 mount on the underside and plug into the Uno.

## Changes

- Replaced the 100 × 100 mm rectangle with the Uno shield outline, approximately 68.58 × 53.34 mm.
- Placed and locked all 32 Uno header pads and four 3.2 mm mounting holes against KiCad's Arduino Uno shield template. Header row spacing is 48.26 mm. D8–D7 spacing is 4.064 mm.
- Combined the split digital connector into one 10-pin header.
- Replaced the ATtiny socket with a correctly numbered DIP-8 socket footprint. Replaced the ATmega socket with a standard DIP-28 socket footprint.
- Moved the target sockets to the top side and restored all three GPIO/ADC breakout headers.
- Removed the existing shorts and completed the routing, with a back-side GND pour.
- Connected Uno D13 directly to SCK. R2 is now a 10 kΩ pull-up from target RESET to 5 V.
- Added Y1 and C5/C6 so an ATmega with 16 MHz crystal fuse settings has a clock during programming. Added C7 to decouple the ATmega AREF pin.
- Replaced the ambiguous electrolytic designation with a nonpolar 10 µF ceramic capacitor compatible with the existing 0805 footprint.
- Used standard KiCad symbols and footprints. The local footprint library contains the slim-post mounting hole beside the Uno SCL header.

## Parts and assembly

| References | Part |
| --- | --- |
| U1 | 28-pin, 7.62 mm row-spacing DIP socket for ATmega328/328P |
| U2 | 8-pin, 7.62 mm row-spacing DIP socket for ATtiny85 |
| J1, J4 | 1×8, 2.54 mm through-hole male shield headers, underside |
| J2 | 1×10, 2.54 mm through-hole male shield header, underside |
| J3 | 1×6, 2.54 mm through-hole male shield header, underside |
| J5 | 1×8, 2.54 mm breakout header, top |
| J6, J7 | 1×6, 2.54 mm breakout headers, top |
| R2 | 10 kΩ, 0603 |
| C1, C2, C3, C7 | 100 nF, 0603, at least 10 V |
| C4 | 10 µF ceramic, 0805, at least 10 V, nonpolar |
| C5, C6 | 18 pF, C0G/NP0, 0603 |
| Y1 | ECS-160-12-33-AGN-TR, 16 MHz, 12 pF load, 3.2 × 2.5 mm crystal |
| H1–H4 | 3.2 mm holes. H1 requires a slim insulating post of at most 4.4 mm outside diameter. |

Use shield headers tall enough to clear the Uno USB connector, barrel jack and ICSP pins. A 13 mm board-to-board gap is the assembly target. Check the actual header engagement and connector heights before soldering. The physical stack has not been tested.

## Programming

Upload ArduinoISP to the Uno before plugging in this shield, because C4 suppresses Uno auto-reset. Program one target at a time, with only one chip installed. Both sockets share RESET, MOSI, MISO and SCK.

The ATmega supports its internal RC clock or the fitted 16 MHz crystal, according to its fuse settings. Select the matching device and clock settings in the programming software. ATmega328 and ATmega328P have different device signatures. The ATtiny uses its internal clock in this design. J7 pin 6 is unused.

| Uno pin | Target connection |
| --- | --- |
| 5 V | Both target supply pins and ATmega AVCC |
| GND | Both target ground pins |
| D10 | Target RESET |
| D11 | Target MOSI |
| D12 | Target MISO |
| D13 | Target SCK |
| Uno RESET | C4 to GND |

## Verification

KiCad 10.0.6 reports zero electrical-rule errors or warnings, zero PCB design-rule violations, zero open connections and zero schematic parity issues. All 32 header pad centers and four mounting-hole centers match the Uno shield template exactly.

The PCB check retains the project's disabled footprint-filter/type checks and tuning-geometry check. Short-circuit, clearance, outline, connectivity, courtyard and silkscreen checks are enabled. Hardware programming, crystal startup, assembly height and fit to a particular Uno or clone remain untested.

The previous PCB, schematic and project settings are preserved in the dated ZIP inside ProgrammerBoard-backups.
