# Course Outline

## Unit One: Defining the problem

* How big is my data?  Long, wide or both? 
* How big is my analysis?  Big because many groups?  Big because looping?  Big because matrix computation?
* How often will I repeat my analysis? By myself as I refine it?  In production?

* How to choose a tool? 
-> You have one dataset.  It can read into R, but tasks are slow:
- grouping and summarizing, esp over a variable with many cats
- mapping through a column, e.g to string process or custom function
- computing lags, sliders, etc.
- making many new columns

What's my slowdown?
-> profvis

Persona: Survey research

-> You have one dataset.  It is too large to read into R.



Persona: Biological genetic data

What's my slowdown?
-> read a few lines, develop your pipeline, profvis

-> You have many datasets.  At least one is too large to read into R.  Joining and subsetting is slow.

Persona: Customer data


* What makes some code faster than others?
- Efficiency of **pipeline**: filter before mutate.
- Efficiency of **algorithm**: think matrix order
- Efficiency of **memory handling**: careful C allocations
- Efficiency of **interpreting** or **compiling**
- Efficiency of **data storage structure**
- Smart saving of **intermediate objects**.


x: data size
y: number of repeated operations

1,1: any
1,2: data table. [write more efficient code]
2,1: parquet & arrow [use better storage formats]
2,2: duckdb & arrow [run in SQL not R]

higher x -> cloud database
higher y -> bigger machine/parallelize across machines/whatever

## Unit Two: Handle it in R with data.table

## Unit Three: Handle it in a local "database" with arrow and duckdb


small: < 1000 or something, everything is split second

medium: 100000 or so, and/or many categories, can read into R but analysis is slow

large: parquet can store on local machine

massive: too big for local machine


Questions for Tyson/Jon:
- Easy way to convert csv to parquet w/o reading into R?  
- Column and row size; handled differently in R?  In parquet?  In a db?


	
Title of course	Storing, Importing, Managing, and Analyzing Large Data Locally with R
Instructor 1	Kelly Bodwin
Instructor 1 Email	kbodwin@calpoly.edu
Instructor 2	Tyson Barrett
Instructor 2 Email	tyson.barrett@usu.edu
Instructor 3	Jonathan Keane
Instructor 3 Email	jkeane@gmail.com
Length of Course	
Full-day (7.5 contact hours)
Course Description	It is increasingly common in academic and professional settings to encounter datasets large enough to exceed the capabilities of standard data processing tools, yet small enough to be stored on local computers. Recent articles even claim that “the era of big data is over” and that data analysts and researchers should “think small, develop locally, ship joyfully.”  Such “medium” dataests are instrumental in measuring, tracking, and recording a wide array of phenomena across disciplines such as human behavior, animal studies, geology, economics, and astronomy. In this workshop, we will present modern techniques for handling large local data in R using a tidy data pipeline, encompassing stages from data storage and importing to cleaning, analysis, and exporting data and analyses.  Specifically, we will teach a combination of tools from the data.table, arrow, and duckDB packages, with a focus on parquet data files for storage and transfer. By the end of the workshop, participants will understand how to integrate these tools to establish a legible, reproducible, efficient, and high-performance workflow.  
Course Outline	The following outline shows our planned approach to managing and analyzing large data locally in R. Our target audience are individuals in academic or professional data analysis positions, who work regularly with datasets that are manageable in terms of local storage but pose significant challenges in processing and cleaning due to their size and complexity.

Unit 1:  Identifying slowdowns in your local data process  (Bodwin; 1 hour)

1.1  Finding the problem:  
   - User-friendly code timing with tictoc
   - Comparing runtimes with atime
   - Code profiling with profvis

1.2  Categories of bottlenecks
   - Common scenarios for repeated runs of code sections
   - Speed impact from order-of-operations in data wrangling
   - Fast vs. slow types of dataset operations in R

1.3  Activity:  Code-along demo
   - Walkthrough of common data structures and tasks that could benefit from modern large-data tools

Unit 2: In-Memory data wrangling with data.table  (Barrett; 2 hours)

2.1  Introduction
   - Basic syntax and structure of data.table
   - Speed comparison for common simple data tasks
   - High-level, user-friendly intuition for data.table’s “under the hood” parallel processing and C optimization

2.2 Data wrangling tools
   - Filtering, summarizing, grouping, and mutating data
   - Sophisticated data processing with the set* functions.

2.3 Activity: Code-Along
   - Real-data examples of data.table use for processing and analyzing data.

2.4 Reference semantics
   - Speed and memory gains from modify-by-reference
   - Effects and side-effects of modify-by-reference
   - data.table syntax for fast no-copy data transformation

2.5 Helper packages
   - Brief highlight of dtplyr and tidyfast as syntactical wrappers to data.table
   - Storing and reading data.table objects with parquet.

2.6 Activity: Case Study
   - Learners work through a guided but incomplete real-data analysis.

Unit 3:  Storing, Reading, and Converting data with arrow, parquet, and duckdb (Keane 2 hours, Bodwin/Barrett 1 hour)

3.1 Introduction to Arrow and Parquet
   - Intro to history and development of Arrow
   - Basic Arrow infrastructure and syntax
   - Discussion of the interchange problem
   - Using arrow reader and nanoparquet for efficient dataset storage and input.
   - Discussion of the Parquet structure, including column orientation and its benefits

3.2 Activity:  Code-Along
   - Data analysis with Arrow.

3.3  Introduction to DuckDB
   - Introduction to duckDB and the local database model.
   - Basic duckDB syntax.
   - Data processing and analysis in duckDB
   - Helper packages such as duckplyr.
   - Working with duckDB and parquet files simultaneously.

3.4  Activity:  Code-Along
   - Data analysis with duckDB.

3.5  Comparison of tools
   - Similarities and trade-offs of arrow, duckDB, and data.table.
   - Options for dplyr syntax in all three packages.

3.6 Activity:  Case Study
   - Goals: Compare, contrast, and benchmark
   - Learners repeat a data analysis task three times, using each of the three tools.
   - Learners benchmark the speed of each step of the task in the three implementations.
   - Discussion and reflection on learner-preferred syntax and usage.

Unit 4:  Putting it together: a workflow for efficient data manipulation (Bodwin/Barrett 1.5 hours)

4.1 Showcase: A tidy pipeline using these modern, efficient tools
   - Import/export: fread, parquet with arrow/duckDB
   - Tidy: dtplyr, duckplyr, arrow
   - Transform: dtplyr, duckplyr, arrow

4.2  Decisions and Guidelines
   - When to choose fread with csv versus parquet conversion.
   - Pros and cons of the local database structure versus local raw data files.
   - Specific data sizes, formats, and computations that are best suited to each tool.

4.3  Activity:  Final Case Study
   - Learners take ownership of a case study of real world large data, writing their own code with a large dataset from start to finish with instructor support
Learning Objectives	Diagnosing and Benchmarking:
   - Incorporate time checks into a data analysis workflow to identify slowdowns.
   - Recognize workflow sections that are likely to be re-run
   - Design data pipeline steps to isolate and improve bottlenecks

Syntax:
   - Write basic data analysis code in data.table
   - Write basic data analysis code in arrow
   - Write basic data analysis code in duckDB
   - Write dplyr syntax code with dtplyr and duckplyr

Concepts and Ideas:
   - Recognize grouping and summarizing operations that will benefit from the data.table implementation
   - Understand the modify-by-reference approach
   - Understand the benefits of parquet’s column orientation storage
   - Know the difference between a collection of local files and a local database.

Workflow:
   - Read csv data with fread and parquet format data with arrow
   - Set up and read/write data in a local duckDB database
   - Smoothly switch between major large data tools within a single data processing and analyzing pipeline.
Instructor(s) Background	Dr. Kelly Bodwin is an educator with over a decade of experience of teaching statistics and data science with R.  She has co-authored multiple R packages, including flair and tidyclust, and she is currently a consultant on an NSF Grant building infrastructure for the data.table package.  Her published applied research frequently involves manipulating large, in-memory data.  Examples include: performing large matrix computations on high-dimensional GWAS (genome-wide association studies) data; constructing temporal social networks at hundreds of time checkpoints for organizational membership data; and summarizing biodiversity metrics grouped over exhaustive permutations of taxa level organism counts and experimental conditions.  Above all, Dr. Bodwin’s educational goal is to lower barriers to entry for beginner and intermediate R users to benefit from modern tools and enable more efficient and effective data workflows.

Dr. Tyson Barrett is a researcher and an applied statistician at Highmark Health and Utah State University. He has over 15 years of R package development and programming experience, including maintaining data.table (with over 600,000 monthly downloads) and 3 other published R packages. He is currently a consultant on an NSF Grant building infrastructure for the data.table package. In his research work, he regularly works with large datasets with millions of rows and hundreds of columns. He and his team use data.table, arrow, and duckDB daily to manage and analyze their data to efficiently and quickly communicate insights with stakeholders.

Dr. Jonathan Keane is an engineering leader at Posit, PBC with a background in data science and social science. They have been building data tooling for 15 years, including both R and Python data tools for scientific and data science computing. They are a member of the PMC for Apache Arrow, a maintainer of the Apache Arrow package, and the author of dittodb. They have also worked as a data scientist in a number of different industries (identify verification and fraud, market research, call centers, and social justice among other areas) using a wide range of tools to analyze, model, and use data at large enterprise scales. On top of building data tooling, they have a passion for teaching data scientists and others how to use data and tools to do their work and inform their decisions.

Additional Comments	Learners should bring a working laptop with an installation of R 4.0+ and a recent (2023 or later) installation of RStudio or Positron.  Learners should ensure that their laptop has admin permission for installation of new R packages.

A beginner-intermediate level of working knowledge in R with the tidyverse is assumed; at approximately the level of Chapters 1-8 in Wickham's R for Data Science (2e).