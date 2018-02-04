# Build caffe2 from source on ubuntu-16.04
## Build with the system python-2.7
Follow the direction of [caffe2-official](https://caffe2.ai/docs/getting-started.html?platform=ubuntu&configuration=compile).

But, make sure that no `protobuf`, `glog` and `gflags` in your machine, as the program would download by itself. 
If you download them by yourself, you must make sure there isn't any conflict.

By the way, you could also install `gflags` from source if you have to: [caffe2-issues-1810:SniperZhao](https://github.com/caffe2/caffe2/issues/1810).

## Build with a conda environment
When using a conda environment, follow the direction of [caffe2-official-anaconda-custom](https://caffe2.ai/docs/getting-started.html?platform=mac&configuration=compile#custom-anaconda-install), 
for no conflicts, make sure that no `protobuf`, `glog` and `gflags` under your conda environment, as the program would download by itself. 

The anaconda path should stay above the system python path in `~/.bashrc`, for the sake of not overlapping the system python-2.7 by the anaconda python-3.6. You should find the following codes in your `~/.bashrc`
```
export PATH="~/anaconda3/bin:$PATH"
export PATH="/usr/bin:$PATH"
```

During cmake, you should do as follows to specify the proper python version (according to [caffe2-issues-1204](https://github.com/caffe2/caffe2/issues/1204)):
```
cmake .. -DPYTHON_EXECUTABLE=~/anaconda3/envs/caffe2_envs/bin/python -DPYTHON_LIBRARY=~/anaconda3/envs/caffe2_envs/lib/libpython3.6m.so -DPYTHON_INCLUDE_DIR=~/anaconda3/envs/caffe2_envs/include/python3.6m
```
Only in this way, caffe2 will be built by the environment's python-3.6 instead of the system python-2.7.

After biult with caffe2-downloaded `protobuf`, write the `~/caffe2/build/lib` to `~/.bashrc` as `PYTHONPATH`
```
export PYTHONPATH=~/caffe2/build/lib:$PYTHONPATH
```
 
Then conda install the same version `protobuf` as `~/caffe2/build/bin/protoc` has, 
i.e., use `~/caffe2/build/bin/protoc --version` to find the version caffe2 downloaded, then conda install protobuf
```
source activate caffe2_envs && conda install protobuf=3.5.0
```
here `3.5.0` is the caffe2-downloaded `protoc` version.

Enjoy your caffe2 :)


