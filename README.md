# Building a custom TensorFlow Wheel
My PC setup has an uncommon combination of HW & SW. 
I have a  10+ years old CPU (Intel Core 2 Duo E8400), yet I'm using the most updated SW. I'm using Fedora 30 (and it ships with Python3.7 & gcc9). I also have an entry level NVIDIA GPU (that's the 1050 Ti).  
The official tesnsorflow wheels are not compatible with my old CPU, as they are compiled with the [AVX instuction set](https://github.com/tensorflow/tensorflow/issues/19584), which is not supported by the Core2 Duo. 
I searched online for a community pre-built custom wheel, but I couldn't find a one that is compatible with my HW & SW combination (there are various wheels that support my old CPU, but they were for Python3.6 or Python2.7. And also, some of them were not built for GPU suppot). 


### Methodolgy

To build the wheel, I mostly followed the [official tensorflow documentation](
https://www.tensorflow.org/install/source). But of course, there were some caveats hiding around.  

### Challenges
+ Fedora 30 ships with gcc9. but the latest version of CUDA is only compatible with gcc up to gcc8.   Luckily, I found a package called `cuda-gcc` supplied by the [negativo17](https://negativo17.org/) repository. This is a gcc package that is compatible with CUDA, and can be co-installed on Fedora 30 with the existing gcc9.  
+ The `Bazel` compiler installed via `dnf` had a newer version that is not compatible with tensorflow. I had to manually install an older version from the Bazel official page. I mostly followed the intructions at this [page](https://docs.bazel.build/versions/master/install-compile-source.html)
+ Building the TensforFlow wheel took 16 hours.
+ I had to connect remotely to my Desktop PC (which was used for building the wheel). To avoid disconnections and restarting the build each time after a disconnect, I learnt to use the `tmux` tool. The `tmux` tool is an indespensible tool for working with a remote PC with an unstable connection. It's also useful for resuming a remote session from various locations/laptops. Another tool that serves the same purpose is `screen`.  
*Living on the bleeding edge of the SW has its price*

### Wheel Specs
+ TensorFlow  1.14
+ Python 3.7
+ No AVX instruction set
+ CUDA 10.1
+ CuDNN 7.4.2 & NCCL 2.4.7

### Download
The WHL file can be downloaded from [here](https://mega.nz/#!DFlC2SiR!_KfsXOspwDDje7a1C8mawhGxz2ObUwW5Mukfhn32Mb8)

