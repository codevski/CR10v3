### G-Code commands for Mesh Update Process
```
G28       ; home all axes
M155 S30  ; reduce temperature reporting rate to reduce output pollution
M190 S55  ; (optional) wait for the bed to get up to temperature
G29 P1    ; automatically populate mesh with all reachable points
G29 P3    ; infer the rest of the mesh values
G29 P3    ; infer the rest of the mesh values again
@BEDLEVELVISUALIZER	; tell the plugin to watch for reported mesh
M420 S1 V ; enabled leveling and report the new mesh
G29 S1       ; Save UBL mesh points to EEPROM.
M500      ; save the new mesh to EEPROM
M155 S3   ; reset temperature reporting
M140 S0   ; cooling down the bed
```