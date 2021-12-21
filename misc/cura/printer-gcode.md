### Start G-Code
```
; CR10-V3 Custom Start G-code
M117 Getting the bed up to temp!
M140 S{material_bed_temperature_layer_0} ; Set Heat Bed temperature
M190 S{material_bed_temperature_layer_0} ; Wait for Heat Bed temperature

M117 Pre-heating the extruder!
M104 S160; start warming extruder to 160

G28 ; Home all axes

M117 Auto bed-level GO!
G29 A	; Enable UBL
G29 L1	; Load the mesh stored in slot 1 (from G29 S1)
G29 J	; No size specified on the J option tells G29 to probe the specified 3 points
	; and tilt the mesh according to what it finds.

G92 E0 ; Reset Extruder

G1 X10.1 Y20 Z0.28 F5000.0 ; move to start-line position

M117 Getting the extruder up to temp!
M104 S{material_print_temperature_layer_0} ; Set Extruder temperature
M109 S{material_print_temperature_layer_0} ; Wait for Extruder temperature

G1 Z2.0 F3000 ; move z up little to prevent scratching of surface
G1 X10.1 Y20 Z0.28 F5000.0 ; move to start-line position

M117 LET THE PURGE BEGIN!
G1 X10.1 Y200.0 Z0.28 F1500.0 E15 ; draw 1st line
G1 X10.4 Y200.0 Z0.28 F5000.0 ; move to side a little
G1 X10.4 Y20 Z0.28 F1500.0 E30 ; draw 2nd line

G92 E0 ; reset extruder

G1 Z2.0 F3000 ; move z up little to prevent scratching of surface

M117 Autobots! Roll Out!
; End of custom start GCode
```

### End G-Code
```
G91 ;Relative positioning
G1 E-2 F2700 ;Retract a bit
G1 E-2 Z0.2 F2400 ;Retract and raise Z
G1 X5 Y5 F3000 ;Wipe out
G1 Z10 ;Raise Z more
G90 ;Absolute positioning

G1 X0 Y{machine_depth} ;Present print
M106 S0 ;Turn-off fan
M104 S0 ;Turn-off hotend
M140 S0 ;Turn-off bed

M84 X Y E ;Disable all steppers but Z
```