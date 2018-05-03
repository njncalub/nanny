# Nanny

[![Latest Version](https://img.shields.io/badge/version-0.0.1-blue.svg)](https://pypi.org/project/nanny/0.0.1)

Simple utility to babysit your folders and files.

Inspired by [benjaminoakes/maid](https://github.com/benjaminoakes/maid).

## Installation

Use pip to install the latest version:

```
$ pip install nanny
```

## Defining rules

Nanny uses a simple DSL for defining the rules. To get started, create your own `~/.nanny/sample.rules` file:

```
rule 'Move files to their respective directories':
    
    for file in '~/Downloads/*':
    
        if file.extension in '.jpg .jpeg .png .gif .bmp .ico':
            move file to '~/Downloads/Images'
        
        if file.extension in '.flv .mp4 .avi .wmv .mkv':
            move file to '~/Downloads/Videos'

rule 'Delete video files bigger than 2GB and older than 3 months to save space':
    
    for file in '~/Downloads/Videos/*':
    
        if file.extension in '.flv .mp4 .avi .wmv .mkv':
            if file.size.gb > 2 and file.age.months > 3:
                move file to trash
```

## Usage

Run `nanny` to view the list of all available options and commands:

```
$ nanny
```

You can run the `clean` command with the `--force` option to overwrite the files:

```
$ nanny clean --force
```

## Automation

You can automate the file cleaning by inserting it to your cron jobs:

```
$ crontab -e
```

Sample for running `nanny clean` every day at 1 am:

```
# minute hour day_of_month month day_of_week command_to_execute
0 1 * * * /bin/bash -li -c "nanny clean --force"
```

## License

MIT. See [LICENSE.md](LICENSE.md).
