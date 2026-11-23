# industry-compares-with-a-comparison-industry
# [Do better-than-expected earnings lead to a higher stock reaction?]

**Author:** [Xiang Ni] · BAN 4550, Fall 2026 · [Industry: 2-digit SIC 36 and Electronic Equipment] ·
Comparison industry: [2-digit SIC 49 and Electric, Gas & Sanitary]
## The question
One or two sentences in plain words: who the client is and what they want to know.
Harry Potter, who leads your project, and the client will hear your complete analysis: your industry (Project 1), your earnings-surprise analysis (Project 2, corrected), and how your industry compares with a comparison industry assigned to you.Do better-than-expected earnings lead to a higher stock reaction?
## Main result
Two or three sentences with your key number, then Figure 1.
![Figure 1](figures/figure1.png)
<img width="1000" height="547" alt="image" src="https://github.com/user-attachments/assets/081d7afe-c51c-4544-a931-62ff2416e635" />
<img width="1018" height="532" alt="image" src="https://github.com/user-attachments/assets/0f7a1656-253d-421c-804d-13d63b84d104" />
Better-than-expected like middle or high-surprise truly lead to higher stock reaction in average 2.6% in both two industries.
## Is the difference real?
The t-test (difference, t-statistic, p-value) and the regression (b, p-value, R²)
for each industry, in plain words, then Figure 2. If you ran more than one model,
say in one sentence whether b changed.
![Figure 2](figures/figure2.png)
<img width="659" height="134" alt="image" src="https://github.com/user-attachments/assets/23889550-10c6-4304-82bd-befb03d4c4ff" />
<img width="659" height="142" alt="image" src="https://github.com/user-attachments/assets/a75b9c90-0110-4f20-8503-8439f73bc0f8" />
<img width="1629" height="673" alt="image" src="https://github.com/user-attachments/assets/5324c34f-fffb-4105-9dd7-403605721016" />
<img width="1802" height="673" alt="image" src="https://github.com/user-attachments/assets/47164dec-e4fd-4ec6-a4eb-b7e0ffc020a5" />

## Why the industries differ
The reason you proposed, and what Figure 3 showed when you checked it.
![Figure 3](figures/figure3.png)
<img width="942" height="548" alt="image" src="https://github.com/user-attachments/assets/47561d0f-bc47-4b38-8d75-93c11d881fab" />
<img width="1925" height="708" alt="image" src="https://github.com/user-attachments/assets/0862f17e-8d89-4011-b471-62796ef03372" />

<img width="1040" height="397" alt="image" src="https://github.com/user-attachments/assets/fbf46bdd-009f-46b0-ac4c-3e7b2dd30762" />
One possible explanation is that stock returns are more dispersed in SIC 36 than in SIC 49. Greater dispersion may be associated with a larger difference between the High-SUE and Low-SUE groups.

Figure 3 checks this explanation by comparing the standard deviation of CAR in the two industries. SIC 49 has a CAR standard deviation of approximately 5.0%, while SIC 36 has a standard deviation of approximately 10.8%. Thus, CAR dispersion in SIC 36 is about 2.16 times that of SIC 49.

This is consistent with the larger High–Low CAR difference in SIC 36 (4.19 percentage points versus 1.38 percentage points in SIC 49). However, this is only a descriptive explanation. It does not prove that higher return dispersion causes the larger difference. Differences in company characteristics, announcement timing, and other factors could also contribute


## Advice for the client
- **Business implication:** The results suggest that companies should not focus only on beating earnings expectations. For NVIDIA (NVDA), which operates in the technology and semiconductor sector, investors may also care about future AI demand, revenue guidance, profit margins, and whether current growth can continue. A positive earnings surprise is associated with higher abnormal returns, but the low R² for SIC 36 shows that earnings surprises alone explain very little of the variation in stock returns. NVDA should communicate both its current performance and its future growth outlook clearly.
- **Limitation:** Companies within SIC 36 have different sizes, business models, and growth prospects, so the industry average may not accurately predict how investors will react to NVDA's earnings announcements. The results also show associations rather than causal effects.
- **Next questions:**- Predictive question: Can NVIDIA's future revenue guidance, AI chip demand, and analyst forecast revisions predict its post-earnings stock returns better than SUE alone? Additional data needed: historical NVDA earnings announcements, analyst EPS forecasts, revenue guidance, data-center revenue, AI chip demand indicators, and stock returns around announcements.

- Prescriptive question: What earnings communication strategy should NVIDIA use to improve investor confidence and manage market expectations? Additional data needed: earnings-call transcripts, historical management guidance, analyst reactions, forecast revisions, investor sentiment, and stock-price reactions to different types of announcements.
## Data
- Sources: Compustat quarterly fundamentals (comp.fundq), CRSP daily stock returns (crsp.dsf), and CRSP daily market returns (crsp.dsi), accessed through WRDS. The CCM link file (ccm_link.csv) connects Compustat company identifiers to CRSP security identifiers.
- **The data are not included in this repository** because of the WRDS license.
Someone with WRDS access can rebuild the results by running the notebook with the
link file in the same folder.
- Sample period and rules: [period, filters].
- Earnings announcements from January 1, 2021, through December 31, 2024. Compustat data are pulled from January 1, 2019, to provide historical information for calculating SUE and prior-quarter prices. CRSP daily returns include a buffer around the announcement period to calculate event-window returns.
- Keep observations with a known earnings announcement date.
Keep announcements between January 2021 and December 2024.
Keep observations for which SUE can be calculated using current EPS, EPS four quarters earlier, and the previous-quarter share price.
Require the previous-quarter share price to be at least $5.
Require absolute SUE to be no greater than 1.
For the CAR analysis, keep observations with complete abnormal returns for days -1, 0, and +1.
## How the tables fit together
Your merge map (image) and two or three sentences on the keys and the date rule.
![Merge map](figures/merge_map.png)

<img width="913" height="1125" alt="image" src="https://github.com/user-attachments/assets/199a862a-02c3-4823-a104-742125da394c" />

<img width="733" height="1125" alt="image" src="https://github.com/user-attachments/assets/4bd4e7ca-8dc0-42f9-9cf9-7b056767f603" />

Compustat quarterly fundamentals and the CCM link table are joined using gvkey with an inner merge. The link dates (linkdt and linkenddt) are then used to retain valid company-security links for the relevant observation dates.



Historical EPS is attached using a left merge on gvkey and the quarterly sequence key, matching EPS from four quarters earlier.



Previous-quarter stock price is attached using another left merge on gvkey and the quarterly sequence key, matching the price from one quarter earlier.



CRSP daily stock returns and CRSP market returns are joined using date with an inner merge. Abnormal returns are calculated as stock returns minus the CRSP value-weighted market return.



The event-window returns are attached to the earnings-announcement sample using event_id with a left merge.

The missing historical EPS and previous-quarter price values are expected when the required historical observations are unavailable. The analysis does not replace these missing values with zero. Observations without calculable SUE are excluded under Rule 3.
## How I checked the results
Your most useful check in two or three sentences: 
I checked that the company-quarter key (gvkey and quarterly sequence number) was unique before attaching historical EPS and price information. I also checked that the CRSP market-return merge did not unexpectedly multiply stock observations and that the event-window merge preserved the announcement sample. Finally, I checked that only observations with complete abnormal returns for days -1, 0, and +1 entered the final CAR analysis.
## Changes since Project 2
<img width="667" height="622" alt="Screenshot 2026-11-22 210250" src="https://github.com/user-attachments/assets/ee6a4329-6504-4e2a-8ee0-5e1201c6a8ae" />

Write "None" if there was nothing to fix.
## Where the code came from
The class notebook, an AI tool, or your own changes. List every AI conversation you
used, one line per conversation:
| AI tool | Link (or PDF in docs/) | What I used it for |
| Gemini | https://share.google/aimode/XW9SlHF0fCkauUluy | 1. Financial & Statistical Concepts: Understanding winsorization (capping outliers), Compustat’s epspx variable (basic earnings per share excluding extraordinary items), CRSP’s market return table (mkt / vwretd), and interpreting a Day −5 to +5 Cumulative Abnormal Return (CAR) chart across Low, Middle, and High SUE groups.
2. Code Walkthrough: Breaking down your data-cleaning, merging, and object-oriented (Industry class) Python pipeline into plain, easy-to-understand steps.
3. Debugging Python Errors: Fixing KeyError: 'mon', KeyError: 'vwretd', and AttributeError: 'Industry' object has no attribute 'car_window_paths'.
4. Data Visualization: Writing Python code to generate and compare charts (including Day −5 to +5 CAR line charts, High-minus-Low spread lines, and regression plots) across two different industries. |
| Chaptgpt| https://chatgpt.com/share/6b03a13a-6d38-83ea-a924-9fcd2f5a91fa| Data and merging / Missing values and sample selection / T-test and regression results / Figure 1 and Figure 2, Figure 3 and industry differences / Business implication for NVIDIA / Limitation|
Write "None" if you used no AI.
## Files
```
notebooks/ Last_First_Project3.ipynb (runs top to bottom on WRDS JupyterHub)
figures/ figure1.png, figure2.png, figure3.png, merge_map.png
docs/ Last_First_Project3.pdf (slides)
README.md
```

your industry (Project 1), your earnings-surprise analysis (Project 2, corrected), and how your industry compares with a comparison industry assigned to you. You also publish a clean GitHub repository that you can show to future employers.

change since project2 on 11.21:
From Emails with TA
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
