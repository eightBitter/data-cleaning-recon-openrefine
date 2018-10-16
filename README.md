# Data Cleaning and Reconciliation using OpenRefine

This workshop was designed for NCSU Libraries' workshop program. Feel free to reuse and remix.

Workshop folder: *insert go link*

## Data Cleaning with OpenRefine

OpenRefine (formerly Google Refine) is a data manipulation and cleaning tool that runs in your browser. The data is not stored online.

OpenRefine allows you to clean data and it saves all of your edits as steps, which you can Undo and Redo (unlike in Excel)

If you know how to use regular expressions, OpenRefine is even more powerful.

GREL (*[OpenRefine Expression Language](https://github.com/OpenRefine/OpenRefine/wiki/General-Refine-Expression-Language) (GREL)* is a programming language for OpenRefine that allows you to do many types of manipulations of the data. We will use it in this workshop.

**To open the software on a Mac:**
Press command + Space Bar: type in “Refine”
Or, search for it in the Applications folder

Download this data set from the workshop folder:
NC_LEED_2002-2010.csv

In Refine, click **Create Project**

Choose Files > Open  > Next

Click **Create Project**

Click on **Show 50 Rows** to see more data

You can see your data by clicking on **first/previous/next/last** options in the menu:

[insert image]

Scanning over the data we can see that it is pretty clean, but there are some things that need to be changed.

**1. Fix inconsistencies in upper/lower case**

Click on the down arrow in the **name** column

Select Edit Cells  > Common Transforms > To titlecase

This should make all values in the cells have a capitalized first letter of each word

**2. Cluster and edit column owner_organization**

owner_organization > Facet > Text Facet

[insert image]

in the left column, click the Cluster button

[insert image]

Here you should be able to edit any inconsistencies in organization names.

Choose what you would like to Merge then Select **Merge Selected & Re-Cluster**

Select different options of clustering algorithms from the **Key Function** dropdown menu to find different potential clusters.

**3. Edit directly in the cluster menu**

[insert image]

Here you can scroll through and manually edit based on any errors you find. Click on edit to the right of the name of the item.

**4. Separate address from Lat/Longitude**

In Location 1, choose Edit column > Split into several columns...

[insert image]

Type in the open parenthesis sign “(“ as the delimiter value (without quote marks)

This should split the column so that the address is in its own column.

**5. Split the column that has latitude and longitude values:**

Edit column > Split into several columns...

“,” as the delimiter

rename latitude column (Edit column > Rename this column)


**6. Remove trailing parenthesis ) from longitude column**

Edit cells > transform

In the expression box, type or copy/paste the following:

`value.replace(")", "")`

To make the longitude values into numbers (they are currently strings) type:

Edit cells…
Common transforms > To number

**7. Create a new column for the year only.**

date_certified column, click on the down arrow

choose **Edit column...**

then **Add column based on this column...**

[insert image]

Type in a new column name

In the Expression window that pops up, type the following formula:

`value.toDate('MM/dd/yy').toString('yyyy')`

This will convert the date that you have from its current format (MM/dd/yy) to the the 4-character year (‘yyyy’)

**8. Find the blanks in name column**

In name column, select  Facet > Customized facets > Facet by blank

This will give you a facet window on the left-side of the screen with “true” and “false” groups.

The “true” group are all of the rows with a blank value for this column. Click on true to find all of the blanks

To exclude the blanks, click “false”

[insert image]

**12. Export the data.** Click “Export” and choose your preferred file type.

## Using Extract/Apply to Clean Future Datasets

[insert image]

With OpenRefine, you can save your work and apply those changes to future data sets!

Here’s how:

On the left hand column, click Undo/Redo

Click the Extract button

Make sure all values are selected (they should be highlighted blue). command +A to select all

Copy with command + c

Open a plain text editor. Paste the JSON code in there

Now load **NC_LEED_2011 2014.xslx** data set into Refine
Open > Create Project > Choose files > NC_LEED_2011 2014.xslx > Next> Create project

This data set is structured the same as the previous one, only different years.

Click Undo/Redo

Click Apply

Paste the JSON code into the window and click **Perform Operations.**

[insert image]

### Test Yourself!

Now try doing some data cleaning in OpenRefine with the **practice data.xslx** file in the materials folder.

## Reconciliation with OpenRefine

[add explanation of reconciliation in OpenRefine and why you would do it]
[add screenshots throughout the notes]

**1.  Reconcile owner_organization against Wikidata**

Click dropdown > Reconcile > Start reconciling

Choose **Wikidata Reconciliation for OpenRefine (en)**. Choose **Reconcile against no particular type** > Start Reconciling

**2. Select the correct matches**

For those that did not automatically match, click on the options to determine best match. Choose **Match this Cell** or **Match All Identical Cells** if you want to apply the same match to identical cells.

**3. Extract labels and identifiers**

Click dropdown > Edit column > Add column based on this column...

In Expression box `type cell.recon.match.name`. Name the column **owner_organization_name**

Repeat; this time type `“https://wikidata.org/wiki/” + cell.recon.match.id`. Name the column **owner_organization_id**

**4. Extract other data from Wikidata!**

Open the Wikidata page of one of the organizations by clicking on link in **owner_organization**.

Looking at the Wikidata page, find a data point you would like to extra. For example, **official website**.

Click dropdown of “owner_organization” > Edit column > Add column from reconciled values...

In the **Add Property** box type in the name of the data point you would like to extract. Choose the desired property. Click OK

## Further Reading

- OpenRefine Documentation - http://openrefine.org/documentation.html
- OpenRefine User Guide - https://github.com/OpenRefine/OpenRefine/wiki/User-Guide
- Cleaning Data with OpenRefine - https://programminghistorian.org/en/lessons/cleaning-data-with-openrefine
- OpenRefine Reconciliation - https://github.com/OpenRefine/OpenRefine/wiki/Reconciliation
