Some files with lots of data (more than 1000 samples, sometimes a few million) regarding certain phenomena.

These files are used for benchmarking my [statistics calculator](https://github.com/Icelk/std-dev/).

# Data

-   `air-pressure`, air pressure (hPa) at altitudes (m)
    -   Fits an exponential function.
    -   5 638 790 samples.
    -   Taken from [a GitHub repo](https://github.com/stsievert/air-pressure-heights/blob/master/noaa-igra-monthly-avgs.zip)
        (I'm using the file `noaa-igra-monthly-avgs/ghgt_12z-mly.txt`).
    -   There are no negative values in this set.

# Usage

The data is stored in tar archives with zstd compression.

Use the `./extract` script to print the data to stdout.
You can then pipe it into a program (e.g. `std-dev` for regression, `xsel -b` to copy it) or
pipe it to a file.

# Creating the data

If you've got a text file with loads of data, I suggest using the following strategy to format it.

The text in square brackets `[]` should be replaced by you.
To extract columns, use `cat [your file] | awk '{print $[column number, starting from 1]}' > first-column-of-data`.
To limit output, add `| head -n[number of lines]` before the pipe to awk.
To then combine two columns again, run `paste [filename of first column] [filename of second column] > data-output`.

To then compress, use `tar -caf compressed.tzst data-output`. The file extension `.tzst` is important for tar to compress it using Zstd.
You can naturally then rename the file and change the file extension.
