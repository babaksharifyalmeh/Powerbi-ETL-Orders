Data Quality Exploration Notes
Dataset: OrderBreakdown_Raw
1. Row Count

The visible sample contains ~20 rows, but the full dataset needs to be counted programmatically during ingestion.

2. Column Quality & NULL Issues

Column	Observed Issues
Order ID	High number of NULL values (~40%). Many rows appear to belong to the same order and require Fill Down. Currently unsuitable as a primary key.
Product Name	No critical issues observed.
Discount	Numeric and clean.
Sales	Contains the suffix “ريال” and thousands separators → must be cleaned and converted to numeric (float).
Profit	Same issue as Sales: textual currency suffix + thousands separator → requires cleaning.
Quantity	Numeric, no major issues.
Category / Sub-Category	Seems complete and consistent.

3. Data Types

Many columns are inferred as any.
Sales and Profit must become float.
Category and Sub-Category should be categorical/string.

4. Structural Issues

The sheet is not a formal Table, only a loose range. This can cause ingestion and PowerQuery parsing issues.
Filter icons and manual formatting may interfere with automated processing.

5. Key Issue Summary

OrderBreakdown_Raw: Order ID is missing in many rows and requires Fill Down. Sales and Profit contain the “ريال” suffix and thousand separators, preventing numeric parsing. Column data types are not correctly detected.

6. Additional Potential Challenges

Possible duplicate rows due to missing Order IDs.
Mixed formatting or Unicode variants of the word “ريال”.
Need to validate whether negative sales/profit exist (returns).

The dataset may combine multiple logical order breakdown formats into a single sheet.