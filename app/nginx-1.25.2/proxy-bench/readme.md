# Customization
1. Copying the following config file to the (f-stack) nginx as the regular test cases.
2. Customizing the content with "#TBC" comments with the valid path of the sub module file. Verified the customized value as
{{{
nginx -c {configfile} -t
}}}

# Generate file with random data as the response:
bs: block size
count: number of blocks
{{{
dd if=/dev/random of=./1kb.txt bs=1024 count=1
}}}

# config files for workload benchmark
* nginx.workload.conf
configfile as the workload service in regular nginx.
* nginx-ff.workload.conf
configfile as the workload service in f-stack nginx.

* workload.conf
regular workload sub config with files as response
