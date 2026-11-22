# Analysis data dictionary

Outcome: 95% Brownian-bridge home-range area (km²).

| Column | Meaning |
|---|---|
| `unit` | Analytical individual or social group. Packs/prides are the independent units for wild dogs/lions. |
| `date` | Observation date; monthly values use the first calendar day, not a GPS fix timestamp. |
| `outcome` | Positive behavior response; see species-specific outcome and units in README. |
| `index` | Three-month SPEI for elephants or SPI for predators; dimensionless. Absent for daily herbivores. |
| `annual_index` | Twelve-month drought index; dimensionless. |
| `animal` | Source animal identifier(s); semicolon-separated where social-group/month rows were combined. |
| `month` | Calendar month 1–12. |
| `year` | Calendar year. |
| `monthnum` | year * 12 + month; monthly continuity index. |
| `sin_month` | sin(2*pi*month/12), seasonal predictor. |
| `cos_month` | cos(2*pi*month/12), seasonal predictor. |
| `dryness` | Negative of three-month drought index; larger means drier. |
| `annual_dryness` | Negative of annual drought index; larger means drier. |

Source-table fields are retained under source/ and documented in the original README where available. Blank source fields are not imputed. The analysis table includes positive outcomes only. No missing stage is synthesized. For result tables, change_pct/low_pct/high_pct are percentage contrasts and nominal bounds; p is unadjusted and q_primary_family is BH-adjusted across the original 11 primary contrasts. Prediction columns observed/predicted use outcome units; predicted_log uses the natural logarithm. Error metrics beginning log_ are on the natural-log scale, not percentages.
