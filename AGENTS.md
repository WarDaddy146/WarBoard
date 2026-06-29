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
