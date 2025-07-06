# Swap Files
﷽
* Swap files store the changes that are made to the buffer. If Vim or your computer crashes, the swap files allow you to recover those changes. Swap files also provide a way to avoid multiple instances of an editor like Vim from editing the same file. More information on swap files can be [found here.](https://www.techtarget.com/searchwindowsserver/definition/swap-file-swap-space-or-pagefile)
* the extension for them is `.swp`
## exploitation
* download the swap file
* print out the human-readable content:
  * `strings {file.swp}`
* save that to a file by `strings {file.swp} >> file.txt`, and use `tac` to reverse it to make it a bit more readable:
  * `tac {file.txt}`

