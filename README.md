# log parser / wine / docker

[Log Parser](https://www.microsoft.com/en-us/download/details.aspx?id=24659) is a
WindowsXP era command line tool for running SQL queries over files. It supports
many different file formats.

This repo provides a script for running LogParser, inside wine, inside a docker
container.

## Install

    ./logparser build

## Usage

Standard queries are great.

    $./logparser "select * from test.csv"
    Filename         RowNumber a b c
    ---------------- --------- - - -
    Z:\work\test.csv 2         1 2 3
    Z:\work\test.csv 3         4 5 6
    Z:\work\test.csv 4         1 1 1
    Z:\work\test.csv 5         4 2 1

    Statistics:
    -----------
    Elements processed: 4
    Elements output:    4
    Execution time:     0.01 seconds

There is also support for some aggregation functions.

    $./logparser "select a, min(b), sum(c) from test.csv group by a"
    a MIN(ALL b) SUM(ALL c)
    - ---------- ----------
    1 1          4
    4 2          7

    Statistics:
    -----------
    Elements processed: 4
    Elements output:    2
    Execution time:     0.01 seconds


## References

  * https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-xp/bb878032(v=technet.10)
  * https://blog.codinghorror.com/microsoft-logparser/
