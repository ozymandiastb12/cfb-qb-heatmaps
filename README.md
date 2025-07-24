# College Football QB Passing Accuracy Heatmaps

This R script creates professional-quality heatmaps visualizing quarterback passing accuracy across different field sections. The visualization shows accuracy percentages in a 3x4 grid representing field width (Left, Center, Right) and depth (Deep, Medium, Short, Behind LOS).

## Features

- **Professional styling** with team-specific title colors
- **Intuitive field layout** (Deep at top, Behind LOS at bottom)
- **Color-coded accuracy** (Gold = Low, Dark Green = High)
- **Automatic team color detection** for 15+ major programs
- **Clean typography** with consistent formatting
- **Proper attribution** (PFF data source + custom watermark)

## Requirements

```r
# Required packages
library(tidyverse)
library(ggplot2)
```

## Data Format

Your CSV file should contain these columns:
- `player` - Player name
- `team_name` - Team name
- `left_behind_los_accuracy_percent` through `right_deep_accuracy_percent` (12 field sections)

## Quick Start

1. **Place your CSV file** in the Downloads folder
2. **Run the script** as-is to see Drew Allar's heatmap
3. **Modify for other players** by changing the search term

## Usage Examples

### Current Example (Drew Allar)
```r
# The script currently searches for "Drew Allar"
allar_rows <- which(grepl("Allar", passing_data$player, ignore.case = TRUE))
```

### Modify for Any Player
```r
# For a different player, change the search term:
player_rows <- which(grepl("Williams", passing_data$player, ignore.case = TRUE))

# Or search by exact name:
player_rows <- which(passing_data$player == "Caleb Williams")

# Or search by team:
team_players <- which(grepl("USC", passing_data$team_name, ignore.case = TRUE))
```

### Multiple Players
```r
# Create a function for easy player switching
create_heatmap_for <- function(search_term) {
  player_rows <- which(grepl(search_term, passing_data$player, ignore.case = TRUE))
  if (length(player_rows) > 0) {
    player_data <- passing_data[player_rows[1], ]
    # ... rest of heatmap code
  }
}

# Usage
create_heatmap_for("McCarthy")  # J.J. McCarthy
create_heatmap_for("Daniels")   # Jayden Daniels
create_heatmap_for("Penix")     # Michael Penix Jr.
```

## Customization Options

### Team Colors
The script includes colors for major programs:
- Penn State, Ohio State, Michigan, Texas, Alabama, Georgia
- Oregon, USC, Notre Dame, Florida, LSU, Clemson
- Oklahoma, Washington, Miami

Add new teams to the `team_colors` list:
```r
team_colors <- list(
  "YOUR TEAM" = "#HEXCOLOR",
  # ... existing teams
)
```

### Color Scheme
Modify the accuracy colors:
```r
scale_fill_gradient2(
  low = "#FFD700",    # Change low accuracy color
  mid = "#7CB342",    # Change medium accuracy color  
  high = "#1B5E20",   # Change high accuracy color
  midpoint = 65       # Adjust midpoint threshold
)
```

### Styling
Adjust visual elements:
```r
# Text size
size = 5.5          # Percentage label size

# Title styling
size = 18           # Title font size

# Tile borders
linewidth = 2       # Border thickness
```

## Field Layout

The heatmap represents a football field from the quarterback's perspective:

```
|  Deep Left  | Deep Center | Deep Right |
| Medium Left |Medium Center|Medium Right|
| Short Left  |Short Center | Short Right|
|Behind LOS L |Behind LOS C |Behind LOS R|
```

## Output

The script generates a publication-ready heatmap showing:
- **Player name and team** in team colors
- **Accuracy percentages** for each field section
- **Color coding** from gold (low) to dark green (high)
- **Professional styling** with proper attribution

## Example Output Description

For Drew Allar (Penn State):
- **Strong areas**: Behind LOS (85.7%-100%), Short passes (76.5%-85.3%)
- **Weak areas**: Deep left (25%), Medium left (54.2%)
- **Patterns**: Better accuracy in center field and shorter distances

## File Structure

```
project/
├── passing_depth.csv          # Your data file (in Downloads)
├── qb_heatmap_script.R       # Main script
└── README.md                 # This file
```

## Data Source

- **Data**: Pro Football Focus (PFF)
- **Created by**: @cpatfbanalysis
- **Visualization**: R/ggplot2

## Contributing

Feel free to:
- Add more team colors
- Improve styling
- Add new features
- Submit pull requests

## License

Open source - feel free to use and modify for your own analysis!

---

**Note**: Update the file path in the script if your CSV isn't in Downloads:
```r
passing_data <- read_csv("~/Downloads/passing_depth.csv")  # Mac/Linux
# or
passing_data <- read_csv("C:/Users/YourName/Downloads/passing_depth.csv")  # Windows
```
