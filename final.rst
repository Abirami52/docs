Patch Review in Gerrit
-----------------------

How to submit a patch in Gerrit?
---------------------------------

#. Navigate to https://gerrit.tungsten.io/ and sign in using the icon in upper right corner with your Linux Foundation login credentials.

#. After signing in, click Settings icon, select **Agreements** from left pane, and then click **New Contributor Agreement** hyperlink.

     - Select any one of the agreement types: CCLA is Corporate Contributor Level Agreement and ICLA is Individual Contributor Level Agreement. Then, click Please review the agreement hyperlink. For further clarifications on whether to fill CCLA or ICLA, mail your queries to cla@lists.tungsten.io.

     - Select your Company name from drop down menu and sign the agreement after providing necessary details.

     - You can now push changes for review.Click on the Create Change button and follow the step by step instructions to create a new patch for review. https://gerrit.tungsten.io/r/dashboard/self.

#. As a new contributor, you have to first clone the project to the local repository. Before cloning, verify if you are authorized to contribute changes to repositories that you want to clone.

     **Cloning a repository** 

     - Navigate to the Gerrit site. For example, the URL for the Gerrit is: https://gerrit.tungsten.io/r/q/status:open.

     - If you have not already done so, sign in using the icon in the upper right corner.

     - From the main menu bar, click **Browse**. A list of available repositories opens.

     - Click the name of the repository you want to clone. A Downloads screen opens. This screen includes several commands that you can copy and use on your local machine.

     - Copy the contents of the Clone with **commit-msg hook** text box or simply the **Clone** text box.

     - From a terminal window on your local machine, paste the command and run it. You now have a clone of the repository on your local machine. 

     - In addition, any commits you push to the remote repository automatically include a Change-Id if you clone using Clone with **commit-msg hook**.

#. Use **git status** command to display the state of the working directory and the staging area. It lets you see which changes have been staged, which haven't, and which files aren't being tracked by Git. Status output does not show you any information regarding the committed project history.

#. Use **git add** command to add a change in the working directory to the staging area. It tells Git that you want to include updates to a particular file in the next commit.

    *Note:* Verify your name and email or set it using the following
    
    git config --global user.email "<email>"
    
    git config --global user.name "<name>"


#. Use **git commit** command to Commit the file that you've staged in your local repository. 

#. Use **git review** command to push your changes to the main repository. 

#. You can see your recently created change in **Outgoing changes** section on Your changes page.


How to review a patch in Gerrit?
--------------------------------

Patch review is an essential process of any contribution workflow. Any patch must undergo review by others before it gets committed. Who can review? After creating a developer account in Gerrit, anyone can comment and express their opinions and approvals. But only a small group of people in Gerrit will be given the authority to approve code and merge it into Gerrit repository.Highest vote (+2 in Code-Review and +1 in Verified) enables submitting.

Gerrit patch review from the command line
------------------------------------------

Using command line, we can review and approve a patch without using the web UI. Below are the steps for reviewing a patch in Gerrit command line interface.

- The first step is to clone the repository:

      $> git clone git://github.com/openstack/glance.git

      $> cd glance

- For making it easier, we can also add a host alias to the SSH configuration.

     $> cat >> ~/.ssh/config <<EOF

     Host review

     Hostname review.openstack.org

     Port 29418

     User markmc

     EOF

 
- Add gerrit server as a git remote.

      $> git remote add -f gerrit

      ssh://markmc@review/openstack/glance.git

- Browse the patches that need reviews.

      $> ssh review gerrit query status:open project:openstack/glance | less

- After picking a patch, take its Change-Id and look at its patch sets and reviews.

      $> ssh review gerrit query status:open project:openstack/glance 
      \
      
      change:I27bb6b3951422ad32e5e0225765b1056c5b3ffc5 \
       
      --current-patch-set --all-approvals | less

- Using "ref" in output, its easy to fetch the patches into your repository and review them.

      $> git fetch gerrit refs/changes/36/636/2

      $> git checkout -b git-authors FETCH_HEAD

- When ready to submit the review, we can do the following

      $> git checkout master

      $> git branch -D git-authors

      $> ssh review gerrit review --code-review +1 -m "'Looks good to me.'" 

      cd9b3a0f2fb91d0d01606ef4bbd90cf8f29267da


Gerrit patch review from the Web UI
-----------------------------------

**To start a review in Web UI**

- Open the changes and click Start Review.

- In the change notification form

     #. Add the names of the reviewers or anyone else you want to copy.

     #. Describe changes.

     #. Click Start Review.

     #. The change is now displayed in other Gerrit dashboards and the reviewers are notified that the change is available for code review.

Searching for changes with pending edits
-----------------------------------------

To find changes with pending edits: Select Your< **Changes** from the Gerrit dashboard. All the changes are listed here, according to works in progress, outgoing reviews, incoming reviews, and so on.

