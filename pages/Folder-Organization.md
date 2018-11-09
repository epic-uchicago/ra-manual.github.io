# Folder Organization

We store project files on both the GitHub repo and a Dropbox folder. 

There is one important principle: all files on GitHub and Dropbox must ultimately be either completed (clean, documented, and checked into the system ready for others to use them) or abandoned (all files deleted), but never left indefinitely in a half-finished state. For storing intermediate work and personal files, you could set up a separate Dropbox folder called ProjectName-Personal.

GitHub and Dropbox have different features, which determine which file types we store on them. GitHub cannot store large files, but it keeps complete version histories and makes it easy to roll back to previous versions. Dropbox can store large files, but it may keep incomplete version histories (depending on your Dropbox account) and makes it difficult to comprehensively roll back to previous versions. We thus store all code and final output files on GitHub, while we store large data files and various other project files (e.g., literature and notes), on Dropbox.

### GitHub repository
The GitHub repo has two main folders: Code and Paper. 
* /Code/Build contains all data prep code.
* /Code/Analysis contains all code to construct tables and figures.
* /Paper/ contains the .tex and .bib files for the paper, and the compiled pdfs
* /Paper/Figures contains ONLY figures for use in the paper and presentations
  - Other figures should go into a scratch or other output folder on dropbox
* /Paper/Tables contains ONLY tables for use in the paper and presentation
  - Other tables should go into a scratch or other output folder on dropbox
* /Paper/Ppt contains Powerpoint slides, which is useful for creating cartoon figures and for creating full presentations (Ryan is old-school and does not like Beamer presentations).

The repo may also include a notes folder for plain text notes that we would like to be versioned.

GitHub likes to keep total storage low, and will not allow users to push files larger than 100MB. If for some reason a code or output file is larger than about 10 MB, then we should store it on Dropbox.

There are two ways of storing something on GitHub: regularly within the repo and in git-lfs ([download git-lfs](https://git-lfs.github.com/) and see [additional info](https://github.com/blog/2079-managing-large-files-with-git-lfs), including GitHub desktop implementation).

The following types of files are the only files that can be stored regularly in the GitHub repository:
* Diffable files (.txt, .csv, .R, .do, etc.) that are under 10 MB.

The following files can be stored in git-lfs:
* Files that are not diffable (binaries, such as: .pdf, .dta, .rds, .ppt, etc.) but are under 10MB (or darn close...)
* Diffable files that are over 10 MB.
All non-diffable files should be added to the git-lfs tracking (e.g., `git lfs track *.pdf`). This will cause git to automatically place these files within git-lfs. Large diffable files should be added to lfs manually (e.g., `git lfs track output/data/somebigfile.txt`).

### Dropbox
Dropbox stores all data files as well as other project documents.
* dropbox/ProjectName/RawData stores all original data files that are used in the analysis. (If there is a data file that we want to store for possible future use/reference but we are not using in the analysis, we should store it in a separate folder called dropbox/ProjectName/DataStorage/.) 
  * The only manipulations that we will generally make within the /RawData folder are: (1) unzipping; and (2) importing into formats readable by Stata, R, etc. When such manipulations are necessary, we should use the following subfolder structure
    * /RawData/orig contains the data as originally obtained. We perform no direct edits in this subfolder, not even unzipping.
    * /RawData/data contains data from RawData/orig that have been unzipped and/or imported into a .dta, .Rdata, etc format. We usually do not make any further manipulations here (one exception: correcting double-entry conflicts).
  * The output from any further manipulations of data should go into dropbox/ProjectName/IntermediateData.
  * All folders containing raw data should have a plain text README file that details the data source and any additional information that is necessary for replication.
* dropbox/ProjectName/IntermediateData stores all intermediate data files, i.e. files created by the code in the GitHub Code folder.
* /Admin stores time sheets, data use agreements, etc.
* /Literature stores all relevant literature, typically in pdf format. Please use the following format to name files: Authors_ShortTitle_Year.pdf.
* /Notes stores any comments or notes that we want to share between each other that are too long or complicated for a post on slack (e.g. a latex file and associated pdf that works through a proof). Very long notes in plain text format (e.g., long latex proofs) could be done in a Notes folder within the Github repo.
* /Scratch stores figures, tables, and other output that we generate in the course of data exploration and are not intended to be used in the paper (see "Exploratory Work" further below)

### Code structure
In general, the code in GitHub/.../Code/Build/ will operate on data from dropbox/.../RawData/ and place it in dropbox/.../IntermediateData/. Then code in GitHub/.../Code/Analysis/ will take data from dropbox/.../IntermediateData/ and construct figures and tables to be placed in GitHub/.../Paper/Figures or /Tables. We also want to be able to trace dependencies and keep the folders clean of unused files. Thus, to the extent that is reasonable, GitHub/.../Code/Build, dropbox/.../RawData/, dropbox/.../IntermediateData/, and perhaps GitHub/.../Code/Analysis should have parallel structures. For example, these folders might all have a subfolder called "CensusData", so code from GitHub/.../Code/Build/CensusData/ prepares data from dropbox/.../RawData/CensusData/ and puts prepared data in dropbox/.../IntermediateData/CensusData/. 

### Log files
Log files can be useful tools for recording the most recent run of each script. If you set up your code to keep a log file, it should adhere to the following guidelines:
* Logs should always be plain text files (e.g. use `, replace text` in the Stata log command, and name the file with a .txt extension)
* Name the log file the same as the script, but with "_log.txt" at the end. E.g., the file "merge_data.do" should create a log named "merge_data_log.txt"
* Log files are stored in GitHub. Each script writes the log file to a "Logfiles" subdirectory located in the same folder as the script.

### Exploratory work
Especially early in a project, there will be exploratory work that may or may not go into the paper. This code for this work could live in git branches, with output going to /Scratch/ subfolders on Dropbox. For instance, we might generate initial descriptive statistics or diagnostics that inform our data wrangling but will not be included in the paper or appendices. Please keep this work clean: once we are fairly sure that an analysis is not in the paper, it should be removed from the master repo. We can always return to it if needed.
