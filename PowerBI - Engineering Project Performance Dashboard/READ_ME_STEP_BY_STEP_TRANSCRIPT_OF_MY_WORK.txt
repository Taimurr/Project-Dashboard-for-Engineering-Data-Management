Transcript of my work (Muhammad Taimur Rizwan):

1. Opened Power BI Desktop
2. Loaded all databases into Power BI

-- ETL Part (Data Cleaning) --
3. Clicked Transform Data to open the Power Query Editor
4. For the Milestones database:
    - Fixed the "Due Date" column by changing the data type from 'Whole Number' to the 'Date' format.
5. For the Teams database:
    - No changes needed
6. For the ProjectUpdates database:
    - Fixed the Start and End Date data types to the 'Date' format
    - Noticed duplicate columns "TeamName" and "Team" within Teams and ProjectUpdates databases so I renamed then to "Team" for consistency.
7. Merged Teams with ProjectUpdates for error handling and simplicity purposes.
    - After clicking to select ProjectUpdates, and then the 'Home' menu in Power Query Editor, I clicked 'Merge Queries as New' then chose ProjectUpdates and Teams. I then merged Team and TeamName  as set the Join Kind to Left Outer.
8. Noticed a new Column called "Teams" with "Table" entered in every field under it so I clicked the 'Expand' button on the right side of the Teams column and unchecked "Use original column name as prefix" to correctly merge and show the data.
   - Removed the duplicate 'Team.1' column
9. Reviewed each database's Applied Steps in Power Query Editor before saving and applying my ETL tool made changes.



-- Relationship Management -- 

10. Reviewed relationships to ensure consistency (this one is the important one): ProjectUpdates[Team] → Teams[TeamName]

-- DAX formulas --

11. Clicked 'New Measure' and applied DAX formulas:
Total Completed = COUNTROWS(FILTER(ProjectUpdates, ProjectUpdates[% Completed] = 100))
Open Issues = COUNTROWS(FILTER(ProjectUpdates, ProjectUpdates[Issue Flag] = "Yes"))
Overall Completion % = AVERAGE(ProjectUpdates[% Completed])

-- Dashboard Creation and Chart Visuals Part (Data Modelling) -- 

12. Added a Multi-Card visual with the following DAX measures: TaskID, TotalCompleted, OpenIssues, OverallCompletion %
13. Added a stacked bar chart to represent the overall task completion % by each engineering discipline (civil, electrical, mechanical) including how many flags each disciplined faced while working through their tasks.
14. Added a line chart to represent the Project Timeline
15. Added a table to act as a Milestone Tracker
16. Added 3 unique slicer buttons to filter between each engineering discipline, raised flags, and which particular task.