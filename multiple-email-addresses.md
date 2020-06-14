# Configuration

1. Update `.gitconfig` using **conditional includes**.

    ```
    [includeIf "gitdir:side_project/"]
        path = .gitconfig-side_proejct
    [includeIf "gitdir:work_project/"]
        path = .gitconfig-work_project
    ... 
    ```

2. Configure side project or work project 

    * Side project (`~/.gitconfig-side_proejct`)

        ```
        [user]
            name = <user name>
            email = <acct>@<side project>.com
        [gui]
            editor = vi
        [diff]
            tool = meld
        [merge]
            tool = meld
        ```

    * Work project (`~/.gitconfig-work_project`)

        ```
        [user]
            name = <user name>
            email = <acct>@<work project>.com
        [gui]
            editor = vi
        [diff]
            tool = meld
        [merge]
            tool = meld

        ```

# References

  [1]. [Git Tips #6 - Using Git with Multiple Email Addresses](https://www.kevinkuszyk.com/2018/12/10/git-tips-6-using-git-with-multiple-email-addresses/)
