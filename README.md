# Houdini Nuke Locator

**Export transform/matrix data from Houdini to Nuke via CSV**

A production-ready toolset that bridges the gap between Houdini and Nuke by exporting null/locator transforms as CSV files, then converting them to animated Axis nodes in Nuke.

## The Problem

Transferring animated nulls/locators from Houdini to Nuke has been a long-standing challenge in VFX pipelines. Unlike Maya locators, Houdini nulls don't export properly via Alembic or FBX in a way that Nuke can interpret as Axis nodes. This toolset solves that problem.

## How It Works

1. **In Houdini**: Use the provided HDA to export your null/locator's world transform matrix to a CSV file on each frame
2. **In Nuke**: Load the CSV using the provided tool, which parses the matrix data and generates an animated Axis node

The CSV format stores complete 4×4 transformation matrices, preserving translation, rotation, and scale data with full animation support.

## Installation

### Houdini Setup

1. Copy `Recipes.hdanc` to your Houdini OTL/HDA directory:
   - **Windows**: `C:\Users\<username>\Documents\houdini20.x\otls\`
   - **macOS**: `~/Library/Preferences/houdini/20.x/otls/`
   - **Linux**: `~/houdini20.x/otls/`

2. *(Optional)* Add `RECIPES_PATHs.py` to your Houdini Python path for additional functionality

### Nuke Setup

1. Copy `HOUDINI_NUKE_LOCATOR_TOOL.nk` to your `.nuke` folder or preferred location
2. Import the tool into your Nuke session or add it to your menu.py for easy access

## Usage

### Exporting from Houdini

1. In your Houdini scene, create or locate the null/transform you want to export
2. Add the **Recipes** HDA to your network
3. Connect or reference your null node
4. Set the output CSV file path
5. Export the animation range

### Importing to Nuke

1. Create a new HOUDINI_LOCATOR node (from the provided `.nk` file)
2. Set the **CSV FILE** path to your exported matrix data
3. Click **CALCULATE**
4. The tool creates an Axis node with animated translation and rotation keyframes matching your Houdini source

## Repository Contents

| File | Description |
|------|-------------|
| `Recipes.hdanc` | Houdini Digital Asset for exporting matrix data |
| `RECIPES_PATHs.py` | Houdini Python helper script |
| `HOUDINI_NUKE_LOCATOR_TOOL.nk` | Nuke tool for CSV import and Axis generation |
| `HOUDINI_NUKE_LOCATOR.nk` | Example Nuke script demonstrating the workflow |
| `matrix_data.csv` | Sample exported CSV file |
| `matrix_data_2.csv` | Additional sample CSV file |

## CSV Format

The exported CSV contains the following columns:

- `Frame` - Frame number
- Matrix components for reconstructing the 4×4 transform matrix
- Translation (X, Y, Z)
- Rotation data (converted to Euler angles in Nuke)

## Compatibility

- **Houdini**: 19.x, 20.x (tested with Houdini.school curriculum)
- **Nuke**: 13.x, 14.x, 15.x (tested with Nuke 15.1)
- **Platforms**: Windows, macOS, Linux

## Acknowledgements

This project was developed over two years with guidance and inspiration from:

- [Houdini.school](https://www.houdini.school/) - Educational resources and methodology
- **Ivan DeWolf** - Technical guidance and support

## Author

**Peter Mercell**  
[www.petermercell.com](http://www.petermercell.com)

## License

This project is licensed under the MIT License - see the [LICENSE.txt](LICENSE.txt) file for details.

---

*If you find this tool useful in your pipeline, consider giving the repository a star!*
