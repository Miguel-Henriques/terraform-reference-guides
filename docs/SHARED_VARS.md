# Shared variables: How to leverage symlinks

Symlinks are a great way to share variables between configurations and reducing the amount of duplicates variables and variable files.

Symlinks are persisted in SCM when you push your changes to the remote repository, meaning that anyone pulling your changes will cause the symlinks to be correctly restored in their local workspace. There is a great [stack overflow topic on this](https://stackoverflow.com/questions/954560/how-does-git-handle-symbolic-links).

Beware that creating symlinks is **OS specific**.