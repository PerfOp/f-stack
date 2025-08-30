# Customization
1. Copying the following config file to the (f-stack) nginx as the regular test cases.
2. Customizing the content with "#TBC" comments with the valid path of the sub module file. Verified the customized value as
{{{
nginx -c {configfile} -t
}}}

# config files for workload benchmark
* nginx.workload.conf
configfile as the workload service in regular nginx.
* nginx-ff.workload.conf
configfile as the workload service in f-stack nginx.

* workload.conf
regular workload sub config with files as response

# config files for proxy benchmark
* nginx.proxy.conf
configfile as the proxy service in regular nginx.
* nginx-ff.proxy.conf
configfile as the proxy service in f-stack nginx.

# bench scripts

## Generate file with random data as the response:
bs: block size
count: number of blocks
{{{
dd if=/dev/random of=./1kb.txt bs=1024 count=1
}}}

## wrk
{{{
/home/azureuser/wrk/wrk -c ${conn} -t {1} --duration {1m} -s upload_file_1kb.lua --latency http://$host:80/1kb
}}}

* upload_file_1kb.lua

{{{
-- Place this file in ramdisk containing placeholder payload
-- load the payload.bin into memory once

-- TBC
local f = io.open("1kb.txt", "rb")
assert(f, "failed to open 1kb.txt")

local payload = f:read("*all")
f:close()

-- wrk will GET this body
wrk.method  = "GET"
wrk.body    = payload
wrk.headers["Content-Length"]   = tostring(#payload)
-- adjust to whatever your endpoint expects:
wrk.headers["Content-Type"]     = "application/octet-stream"
}}}
