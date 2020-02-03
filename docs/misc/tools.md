# My Tools
This section contains a brief description of some of the software I use, why I use them, and how to configure them.

## IDE
I use atom.

To enable direct edit of scripts on the cluster,
I installed the __Remote FTP__ and __platformio-ide-terminal__ packages.<br>
![](links/atom.png){: style="width:500px"}

## Documentation
I use markdown, mkdocs, combined with github and readthedocs to create online documentation
for common processes. This guide is created using this exact process.
To enable mkdocs locally on 127.0.0.1:8000, activate the conda environment for mkdocs and run `mkdocs serve`.
```
conda activate markdown_env
mkdocs serve
```
