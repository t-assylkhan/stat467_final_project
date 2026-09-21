# Analysis of the Polish Real Estate Market Using Multivariate Techniques

STAT 467 (Multivariate Data Analysis) course project, Group 19.

**Authors:** Tamerlan Assylkhan, Kirill Kiselev, Alikhan Karimov

We apply the multivariate methods from the course to apartment listings from the 15 largest Polish cities, asking what drives prices, how cities differ, and whether the market falls into natural segments.

## Repository contents

| File | Description |
|------|-------------|
| `Stat 467 Project Presentation Group 19.pptx` | Final presentation slides |
| `Stat 467 Project Presentation Group 19 Code.ipynb` | Jupyter notebook with all analysis code and figures |
| `apartments_pl_2024_06.csv` | Dataset (June 2024 snapshot) |

## Data

The dataset is [*Apartment Prices in Poland*](https://www.kaggle.com/datasets/krzysztofjamroz/apartment-prices) by Krzysztof Jamroz (Kaggle, 2024). It contains 21,501 apartment listings from 15 cities and 28 columns (including a listing `id`):

- **Property features:** `squareMeters`, `rooms`, `floor`, `floorCount`, `buildYear`, `type`, `ownership`, `buildingMaterial`, `condition`
- **Amenities (yes/no):** `hasParkingSpace`, `hasBalcony`, `hasElevator`, `hasSecurity`, `hasStorageRoom`
- **Location and accessibility:** `city`, `latitude`, `longitude`, `centreDistance`, `poiCount`, and distances to the nearest school, clinic, post office, kindergarten, restaurant, college and pharmacy
- **Target:** `price` (PLN)

Missing values were handled without dropping rows: continuous variables were imputed with the median, and missing categorical values were assigned an `unknown` category.

## Methods and key results

| Method | Question | Result |
|--------|----------|--------|
| One-sample Hotelling's T² | Is the mean distance to the 7 infrastructure types (school, clinic, post office, etc.) equal to 1 km for Warsaw apartments? (n = 6,962) | H₀ rejected (F = 24,641, p < 0.001) |
| Two-sample Hotelling's T² | Do apartments with and without each amenity differ on size, price, rooms, floor and build year? | H₀ rejected for balcony, parking, elevator, security and storage room |
| MANOVA | Do Warsaw, Kraków and Wrocław differ? | H₀ rejected (F = 252.97); Warsaw is the most expensive and has the tallest buildings |
| PCA / PCR | Can 12 correlated numeric variables be reduced? | 4 components explain 75.2% of variance: location quality, apartment size, building height, suburbanization. PCR on components alone gives R² = 0.375 |
| Hybrid PCR | Do amenities and categorical features add explanatory power? | log(price) on 4 PCs + 5 binary + 23 dummy variables gives R² = 0.831 |
| Factor analysis | What latent factors underlie the data? | Same 4-factor structure under Varimax and Promax rotations |
| LDA / QDA | Can high- and low-priced apartments be told apart? | LDA outperforms QDA; size, distance to centre and distance to restaurants are the top discriminators |
| Clustering | Are there natural market segments? | 3 segments: Standard Urban (63%), Premium/Luxury (20%), Modern Suburban (17%) |

See the slides for the full discussion, figures and conclusions.

## Running the notebook

The notebook reads `apartments_pl_2024_06.csv` from its own directory, so open it from the repository root.

Requirements: Python 3 and the following packages.

```bash
pip install pandas numpy scipy scikit-learn statsmodels factor_analyzer matplotlib seaborn jupyter
jupyter notebook "Stat 467 Project Presentation Group 19 Code.ipynb"
```

## References

- Johnson, R. A., & Wichern, D. W. (2007). *Applied Multivariate Statistical Analysis* (6th ed.). Pearson.
- Rencher, A. C., & Christensen, W. F. (2012). *Methods of Multivariate Analysis* (3rd ed.). Wiley.
- Jamroz, K. (2024). *Apartment Prices in Poland* [Data set]. Kaggle. https://www.kaggle.com/datasets/krzysztofjamroz/apartment-prices
