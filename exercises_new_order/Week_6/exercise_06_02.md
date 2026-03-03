## Week 6, Part 2: Views and Functions Practice

1. In this exercise, you'll convert a query to both a view and function to encapsulate the same logic.  
a. Start by writing a query using the visit_occurrence table to find the total number of patients per provider, considering only inpatient visits (visit_concept_id=9201).
b. Convert your query into both a standard view and a materialized view.
c. Perform a select all from both views? Which is faster? 

2. Build a view that shows each patient's first inpatient visit date. Then use that view in a query that calculates how many patients had a follow-up visit within 90 days. Hint: You may want to make use of the [INTERVAL keyword](https://www.datacamp.com/doc/postgresql/interval).

**For the next questions, you'll be working with the new_york_trees dataset in BigQuery's public datasets.

3. First create a dataset in your BigQuery sandbox project. Then create a logical view named "healthy_tree_stats" for simplified, normalized access to tree health. You should include tree_id, boroname, zipcode, and spc_common fields. (Hint: you can use a CASE statement to take the existing values and not only make them more meaningful but also clean up missing data. Health status Good should become "Vigorous", Fair should be "Stable", Poor becomes "At Risk", and null values should be replaced with "Unknown")

4. Using the logical view created in question 4 and the 2005 tree census table, find the count of "Vigorous" trees added after 2005 (ie, they appear in 2015 but not 2005). Include the first word of spc_common from the view. (Hint: the 2005 census has a different schema than 2015, think about the most logical joining column)

5. Create a materialized view for pre-aggregating the count of trees by species within each borough. Include the boroname and src_common columns, as well as the count of trees per borough and species. Note that a limitation of using the public datasets is that you can't create a materialized view directly from the table (it's in a different organization/project). A workaround for the purposes of this exercise is to copy the table to your dataset and create the materialized view on the copy. You can write a multi-part statement to do this. The first part will use the CREATE TABLE syntax in SQL from a query result (https://docs.cloud.google.com/bigquery/docs/tables). Separate the two parts with a semi-colon and you can run the CREATE TABLE statement in the same job as the CREATE MATERIALIZED VIEW statement. Contain all logic in the CREATE MATERIALIZED VIEW statement. (If you need to recreate the table or materialized view , you will need to drop or delete them first.)

6. Using the materialized view created in the previous question, find the top 5 most common species across NYC and their percentage of the total tree population. (Hint: the count will be by borough)

## Challenge Questions

1. In this exercise, you'll chain together views.  
a. Start by creating a view to find all inpatient visits in 2009.
b. Then create a materialized view that counts distinct patients per provider from that filtered view.
c. Finally, write a query using the materialized view to get the top 5 providers by number of distinct patients in 2009.