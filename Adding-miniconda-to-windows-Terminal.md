## How to add `Miniconda` prompt to `Windows Terminal`

To add the miniconda prompt to windows terminal, go to settings from windows terminal and then open the settings json file. Now append the following new profile in the profile list,

```
{
    "guid": "{2337f50b-bd5c-4877-b127-d643395b8fe2}",
    "hidden": false,
    "name": "Miniconda",
    "commandline": "powershell.exe -ExecutionPolicy ByPass -NoExit -Command \"& 'C:\\Users\\%USERNAME%\\miniconda3\\shell\\condabin\\conda-hook.ps1' ; conda activate 'C:\\Users\\%USERNAME%\\miniconda3' \""
}
```

While doing this, just make sure the `guid` id is unique among all profiles. Then save and close this settings.json file and to make more changes, do those from the windows terminal settings using the gui.


### Acknowledgment

Took this note from [this site](https://dev.to/voodu/windows-terminal-conda-d3e). Thanks to **Piotr Ładoński** who posted this helpful post on that site.