# Checking out a file with special characters

I had been repository in databricks and pushed these to git. I then tried to pull the changes on the branch to my local machine. One of the filenames contained a ">" character, which is not [permitted in filenames](https://stackoverflow.com/a/35352640) on Windows. 

Trying to pull from git gave an error like the below

    error: invalid path 'test>123.md'

I updated the filename in databricks and was then able to make the pull the changes on the branch to my local machine. 
 