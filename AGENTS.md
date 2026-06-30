# KiCAD MCP Server Setup

## Server Location
- Path: `/home/wardaddy/Documents/KiCAD-MCP-Server`
- Start: `node /home/wardaddy/Documents/KiCAD-MCP-Server/dist/index.js`
- Rebuild: `npm run build` (in that directory)

## Project Files
- Schematic: `WarBoard.kicad_sch`
- PCB: `WarBoard.kicad_pcb`
- Project: `WarBoard.kicad_pro`
- Custom symbols: `War_Library.kicad_sym`
- Symbol libs: `sym-lib-table`
- Footprint libs: `fp-lib-table`

## Key Info
- KiCad version: 10.0.4
- Python bindings: `/usr/lib/python3.14/site-packages/pcbnew.py`
- MCP server uses STDIO transport, `pcbnew` module validated on launch
- The MCP server spawns a Python child process (`kicad_interface.py`) in a venv at `KiCAD-MCP-Server/venv/`
- Server automatically detects KiCad install; PYTHONPATH only needed if pcbnew is not in default site-packages

## Temporary Session Notes (2026-06-30)

### Handover Prompt
The user is working on a WarBoard (nRF52840 wireless macropad). A backup branch `routing-experiment` was created. Battery wiring in schematic has an issue — U3 pin 13 (BAT+) is unconnected, and the battery+ wire has no net label (unnamed net). Track widths don't change with net classes — likely the "Track Width" dropdown in PCB Editor is set to a fixed value instead of "Use Net Class Values". The KiCad MCP server connection was lost (killed by accident). Restart opencode to re-establish.

### Net Class Plan
Three net classes planned: **Default** (0.2mm/0.2mm/0.6mm), **Power** (0.4mm/0.2mm/0.7mm), **GND** (0.3mm/0.2mm/0.6mm). Need to verify PCB Editor toolbar dropdown is set to "Use Net Class Values", assign nets to classes via Board Setup, and update existing track widths via Edit Track & Via Properties.

## MCP Config (opencode.json)
```json
{
  "mcp": {
    "kicad": {
      "type": "local",
      "command": ["node", "/home/wardaddy/Documents/KiCAD-MCP-Server/dist/index.js"],
      "environment": {
        "NODE_ENV": "production",
        "LOG_LEVEL": "info",
        "KICAD_AUTO_LAUNCH": "false",
        "PYTHONPATH": "/usr/lib/python3.14/site-packages"
      },
      "enabled": true,
      "timeout": 60000
    }
  }
}
```
