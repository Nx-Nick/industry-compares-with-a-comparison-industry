# industry-compares-with-a-comparison-industry
your industry (Project 1), your earnings-surprise analysis (Project 2, corrected), and how your industry compares with a comparison industry assigned to you. You also publish a clean GitHub repository that you can show to future employers.

change since project2 on 11.21:

1.Your notebook stops at Step 5. Step 4 applies Rules 1 to 5 and saves the result as "sample", but Step 5 uses "events", so Python can't find it and throws an error. Use the same name in both steps, for example by saving the table as "events" at the end of Step 4.

2.Your final results came from an old "events" table left in memory from an earlier run. That table only had Rules 1 and 2 applied, so rows that Rules 3, 4 and 5 should have removed are still in your results. You can see it in your notebook: 2,879 rows go into the CAR step, when it should be 2,209 after Rule 5. That's also where the huge CAR of about 5.08 for KOSS comes from.

3.Some cells use names that aren't created anywhere in the notebook (record_count, sample_counts, qnum). They were probably in cells you deleted, so add them back or remove those lines.

4.Before you submit, click Kernel > Restart Kernel and Run All Cells. It clears memory and runs everything from the top, so anything missing shows up right away.

5.Step 6b gives an error because qnum is never created. Make it from fyearq and fqtr before you use it. The later errors (Step 7, Check 5/6, Q2, Q3) come from this one, so they should go away once it's fixed.

6.Q2 keeps the five largest CARs. It should remove them.

7.The lags still use shift(). Use the quarter number to find the EPS 4 quarters ago and the price 1 quarter ago.

8.Day 0 should come from the market trading days (dsi), not the stock's own dates.

9.In the rules, use the settings from Step 0 instead of typing the numbers again.

10.Remove the extra test cells and the last cell that saves NVDA_final_events.csv.

conclusion:
Step 0: Move all your imports here (matplotlib, scipy, statsmodels, summary_col). Also add LABELS here. Then delete the second import cell further down. You can also delete FY_START and FY_END, since they aren't used.
Step 3c: SUE is calculated twice. Keep the first one (the one with abs() on price) and delete the second block and its display.
Step 6b: Delete the leftover record_count text in triple quotes. You can print how many rows Rule 6 removed instead.
Step 7, Check 3b: You reuse the name market_dates, which overwrites the one from Step 6. Give it a different name.
Q2: Right now it keeps the five largest CARs. Add the "not" sign (~) in front of the isin part so it removes them instead.
Figures 1 and 2: Change the labels. "12-month abnormal return" should be 3-day CAR, "EPS change" should be SUE, and "company-year" should be announcement.
Day -5 to +5 chart (last cell): Find Day 0 the same way you did in Step 6, using market_calendar. Then take the 11 market dates around it and use reindex on the stock's data to get the ARs for those dates. This also fixes the KeyError 'date'.
Delete the test cells: the scratch calculation, the NVIDIA check cell, the quick bar plot, sample.info, and the empty last cell.
