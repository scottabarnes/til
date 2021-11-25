# Reverting a commit

Wanted to check I'd be able to revert a commit prior to making some changes to a repository. Some good answers [here](https://stackoverflow.com/questions/4114095/how-do-i-revert-a-git-repository-to-a-previous-commit). Adopted the below approach. 

    # This will create three separate revert commits:
    git revert a867b4af 25eee4ca 0766c053

When running on windows terminal, you then have the option to provide a new commit message in vim. Once the message has been updated, the commit can be made by hitting `Cntrl-C` and then typing `:qa!`.