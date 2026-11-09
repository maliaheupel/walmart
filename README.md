# Walmart Hurricane Analytics — DS2002 Midterm Project
Reflection questions answered at the bottom of the file.

## Members
- Claire Zhang (GitHub: https://github.com/legsleggylegs/ds2002-fa26)
- Jennifer Lutchen (GitHub: https://github.com/Jennifer-Lutchen/ds2002-fa26)
- Malia Heupel (GitHub: https://github.com/maliaheupel)

## Overview
This repository contains our team's ETL data pipeline, weather API integration, and analytics notebook analyzing Walmart's transaction data during Hurricane Helene. The project evaluates pre-storm demand surges, resolves fragmented SKUs, and analyzes weather correlations to guide inventory decisions.

## Repository Layout
```
walmart/
├── CHARTER.md                # Team charter and working agreements
├── README.md                 # Project summary and documentation
├── data/                     # Raw transaction files and SQLite database
└── notebooks/
    ├── team_notebook.ipynb   # Main deliverable notebook
    └── scratch/              # Individual working notebooks
```
**Reflection Questions**

**1. Data Quality: Which single data-quality problem, if it had gone unnoticed, would have changed your conclusion the most? Give the number both ways.**

Before data cleaning in question 2, the data for Pop-Tart sales was fragmented, as there were multiple SKUs in the data set all corresponding to the same product. As a result of this, the fragmented nature of the data hid the true demand surge for strawberry Pop-Tarts as a result of the incoming hurricane. After consolidation, the surge became much more apparent; the daily sales peak for Pop-Tarts seems to nearly 700 units after consolidation, compared to less than 300 across fragmented data. Being able to see this surge more clearly might includence business decisions on how much inventory to stock in regards to this product.


**2. ETL Trade Offs: Name a cleaning decision where a reasonable person could have chosen the other way. What was the other option, what would it have done to your reported numbers, and would you make the same call again?**

During the merging of the weather data and the sales data, we decided to join the data sets on the dates that this occured. Naturally, we had one set of weather parameters corresponding to a specific date, but there were often multiple sales that happened on the same day. We decided to try to preserve as much data as possible by adding the column values for individual sales on a given day to a list, then assigning that list to the date. However, since this was not strictly necessary for answering the questions, as Q3 concerns total sales volume per day, a reasonable person could have omitted this information in the merge and just kept track of quantity. Either of these decisions would have yielded the same reported result, as the questions didn't concern other parameters. Since we didn't end up relying on the extra information, it might have been easier to forgo this extra step if we were asked to make the call again. However, if there were additional questions or curiosity where information about specific sales per day would be useful, then we should keep our original approach.


**3. Pipeline Trust: If someone handed you this notebook and asked whether the numbers are right, what would you check first? Is that check currently in the notebook? If not, that is your first capstone improvement.**

The first thing I would check if someone asked if the numbers were right is whether the cleaning and joining steps preserved the data correctly. Specifically, I would look for validation checks throughout the notebook showing rows before and after a function was run to confirm the numbers look right. Some data cleaning resulted in fewer rows, and that should be accurately documented along with how many rows are affected. Other effects like joining should have resulted in the same number of rows before and after, and that too should either be shown through a validation check or an assertion. All of these things can be found in our code throughout each question. In scrolling through the outputs from each cell, there are numerous validation checks stating the number of rows before and after something happened to the data. Additionally, there are multiple assertions throughout the code itself, so the fact that the whole code runs smoothly is another good sign.

**4. Business vs Data: Your recommendation went past what the data strictly proves — every useful recommendation does. Where exactly is that line in your work, and how would you say it out loud to someone who is about to spend money based on it?**

Our data analysis of the Walmart transactions demonstrated that in the three-day period prior to Hurricane Helene, product demand surged up to 3.4x normal levels for breakfast foods and 2.4x for emergency supplies. Although this data accurately represents past consumer behavior, the line is our work is deciding whether these exact behaviors will repeat for future severe weather events to justify upfront expenditures. To someone who is about to spend money based on this, we would say: "While past data does not offer a 100% guarantee that shoppers will act the exact same in the future, we can assume that future buyers will act similarly. Therefore, rather than waiting until demand spikes or the storm hits, we would recommend increasing breakfast foods by at least 3x normal levels and emergency supplies 2x normal levels at least three-days before the storm is expected to hit.


**5. Team Process: What cost your team the most time that was not a data problem? Merge conflicts, duplicated work, waiting on someone, unclear ownership? Name the specific change you will make for the capstone.**

Throughout the course of this project, we were able to work efficiently with each other. However, one thing that cost our team the most time was waiting on each other to finish our portion, so that the next person could complete the next step. Since it is difficult on Colab to all edit at the same time, we ended up dividing our work by questions and the write-ups associated with them, so we had to wait for each person to finish their section before starting our own. Since we all have different, busy schedules sometimes the timing of wanting to start your own section would not align perfectly with the person working on the section before, even though sometimes it did not matter. We ended up working on a few different copies and then compiled it all into one notebook at the end. One change we will make for the capstone would be reviewing the entire project outline upfront so we could divide out truly independent sections from day one, eliminating the need to wait on each other's progress.
