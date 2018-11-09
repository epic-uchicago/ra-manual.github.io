# GitHub Issues

We use GitHub for task management. Any quick question that would take less than one hour to answer can be done via Slack. Any task that will take more than one hour should be set up as an Issue in the GitHub repo. 

#### Task deliverables
* Each task should have a final deliverable summarizing the results.
* The form of the deliverable may be:
  - Content added to the draft, slides, or appendix
  - A note in the /Notes directory
  - A final summary comment in the task comment thread (e.g., for tasks involving modifications to data preparation code that do not directly yield paper content or for small tasks where the deliverable content is no more than a paragraph or so of text)
* The deliverable should be self-contained. It should usually begin with a concise summary of the conclusions (e.g., an answer to an empirical question or a modification to the code), followed by supporting detail. A user should be able to learn all relevant results from a task from the deliverable without looking back at the comment thread or task description. The source of any figures, tables, or statistics should also be clear; this will be automatic for markdown files or checked in drafts, slides, etc. so long as figures and tables are produced from links to checked-in files in the repository.
* The final comment at the time a task is closed should include a clear, [revision-stable pointer](https://help.github.com/articles/getting-permanent-links-to-files/) to the deliverable -- usually a link along with additional information if needed (e.g., relevant page / table / figure numbers in the draft or line numbers in code).

#### Creating a task
* Anyone can create a task
* If Ryan/other more senior person asks you to do a task (via email or Slack or in a meeting), you are responsible for recording this in a GitHub Issue and assigning it to yourself. This should be your first step after the meeting so we don't lose track of tasks.
* The assignee should create a separate git branch for each task that involves code or output stored in the repository. The new branch should be called `issue###-brief_description`, where ### corresponds with the issue number. Make sure you do not push your changes to `master` before the task is completed.
  * Additional branches can be made off of the main `issue###-brief_description` branch as needed. These sub-issue branches should be merged into the main `issue###-brief_description` branch, not into the `master` branch.

#### Comment threads in GitHub Issues
* You should add regular comments to tasks summarizing progress. The comment threads are your real estate and you are free to include updates as often as you find useful. Preliminary output, "notes to self," etc. are fine.
* If you have a question that requires input from another lab member, you should write a comment, including an '@' reference, that makes clear exactly what input is needed. E.g., '@kelloggrk, Where would you like me to store the data files?' Users should keep email notifications for '@' references turned on.
* It is up to you to judge the optimal time to request feedback. You should usually not send results until you have spent some time making sure they are correct and make sense. When you do request feedback, you should provide a clear and concise summary making clear the situation and exactly what input you need. At the same time, you should not feel shy about requesting feedback when you are confident it will be efficient and valuable.
* The Issues pages are our primary documentation of decisions we are making as we move through the project. If you have an important interaction about a task outside of GitHub -- in person, over IM, etc. -- add a comment to briefly summarize the content of that interaction and the conclusions reached. The reason is that we don't want to have to search through meeting notes, emails, or Slack threads to understand how/why we made a decision 15 months ago.
* Any link in a comment to other files in the repo should link to the file at a specific commit (see [here](https://help.github.com/articles/getting-permanent-links-to-files/) for details).
* Any link within an issue to another issue should be hyperlinked using the '#' reference. E.g., #123. 

#### Completing a task
When an assignee thinks a task is complete, he/she should:
* Ensure that the deliverable meets our standards as outlined above
* If the deliverable involves commits to GitHub files:
  * Submit a pull request to merge the issue-specific branch into the master branch.
  * Pull requests should be titled as follows: "Pull request for #[ORIGINAL ISSUE NO]: [ORIGINAL ISSUE TITLE]"
  * Pull requests should hyperlink to the issue using the '#' reference. E.g., #123. 
  * You are empowered to merge your own pull request once you are satisfied.
  * [Squash merges](https://help.github.com/articles/about-pull-request-merges/) are typically preferred to merge the issue-specific branch into the master branch.
  * Delete the `issue###-brief_description` branch  
* Close the original issue after adding a final comment that summarizes the deliverable and includes a link to the pull request and a revision-stable link to the deliverable.


#### Back-burner issues
We will sometimes acknowledge issues that must be addressed before completion of a project but are not of high enough priority that they will be worked on within a month. To make sure such issues are not forgotten, each project will have a single GitHub issue named "Back-burner issues list" that lists all such issues. This approach avoids clogging up the list of GitHub issues with tasks we will not address for some time.

When the time comes to address a back-burner issue, the assignee will create a new, proper GitHub issue that adheres to the standards above and remove the corresponding entry from the back-burner issues list. All back-burner issues must be addressed before completion of a project.
