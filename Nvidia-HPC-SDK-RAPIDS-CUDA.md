# The Nvidia HPC-SDK, CUDA, RAPIDS ,  PyCuda, CuPy, DASK, SCIKIT, SCIPY, JUPITER, NUMBA, CuPy, CuDNN, NCCL,CuTensor


1. https://cupy.dev/
2. https://docs.rapids.ai/
3. https://numba.pydata.org/
4. https://developer.nvidia.com/hpc-sdk
5. https://developer.nvidia.com/cuda-toolkit
6. https://developer.nvidia.com/blog/rapids-24-12-introduces-cudf-on-pypi-cuda-unified-memory-for-polars-and-faster-gnns/
7. https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2404/x86_64/

```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2404/x86_64/cuda-ubuntu2404.pin
sudo mv cuda-ubuntu2404.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/12.8.0/local_installers/cuda-repo-ubuntu2404-12-8-local_12.8.0-570.86.10-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu2404-12-8-local_12.8.0-570.86.10-1_amd64.deb
sudo cp /var/cuda-repo-ubuntu2404-12-8-local/cuda-*-keyring.gpg /usr/share/keyrings/
sudo apt-get update
sudo apt-get -y install cuda-toolkit-12-8

wget https://developer.download.nvidia.com/compute/nvidia-driver/550.144.03/local_installers/nvidia-driver-local-repo-ubuntu2404-550.144.03_1.0-1_amd64.deb
sudo dpkg -i nvidia-driver-local-repo-ubuntu2404-550.144.03_1.0-1_amd64.deb
sudo cp /var/nvidia-driver-local-repo-ubuntu2404-550.144.03/nvidia-driver-*-keyring.gpg /usr/share/keyrings/
sudo apt-get update
sudo apt-get install -y nvidia-driver-550-open

wget https://www.mellanox.com/downloads/DOCA/DOCA_v2.9.1/host/doca-host_2.9.1-018000-24.10-ubuntu2404_amd64.deb
sudo dpkg -i doca-host_2.9.1-018000-24.10-ubuntu2404_amd64.deb
sudo apt-get update
sudo apt-get -y install doca-all

```


### TESTS


```
ssh admins@Studio-Svr
Welcome to Ubuntu 24.04.1 LTS (GNU/Linux 6.8.0-51-generic x86_64)


Last login: Wed Jan 22 09:06:37 2025 from 192.168.1.99
❯ lspci
1d2c:00:02.0 Ethernet controller: Mellanox Technologies MT27710 Family [ConnectX-4 Lx Virtual Function] (rev 80)
81df:00:00.0 3D controller: NVIDIA Corporation TU104GL [Tesla T4] (rev a1)
b0d2:00:00.0 Non-Volatile memory controller: Micron/Crucial Technology P2 [Nick P2] / P3 / P3 Plus NVMe PCIe SSD (DRAM-less) (rev 01)
╭─ ~/cuda-samples/Samples/1_Utilities/bandwidthTest  on master ?6 ──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────── ✔  with admins@studio-svr  at 10:57:18 ─╮

❯ nvidia-smi
Wed Jan 22 10:44:29 2025
+-----------------------------------------------------------------------------------------+
| NVIDIA-SMI 550.127.08             Driver Version: 550.127.08     CUDA Version: 12.4     |
|-----------------------------------------+------------------------+----------------------+
| GPU  Name                 Persistence-M | Bus-Id          Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |           Memory-Usage | GPU-Util  Compute M. |
|                                         |                        |               MIG M. |
|=========================================+========================+======================|
|   0  Tesla T4                       Off |   000081DF:00:00.0 Off |                    0 |
| N/A   61C    P0             28W /   70W |       1MiB /  15360MiB |      0%      Default |
|                                         |                        |                  N/A |
+-----------------------------------------+------------------------+----------------------+

+-----------------------------------------------------------------------------------------+
| Processes:                                                                              |
|  GPU   GI   CI        PID   Type   Process name                              GPU Memory |
|        ID   ID                                                               Usage      |
|=========================================================================================|
|  No running processes found                                                             |
+-----------------------------------------------------------------------------------------+

❯ nvcc --version
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2024 NVIDIA Corporation
Built on Thu_Mar_28_02:18:24_PDT_2024
Cuda compilation tools, release 12.4, V12.4.131
Build cuda_12.4.r12.4/compiler.34097967_0
❯  git clone https://github.com/NVIDIA/cuda-samples.git
Cloning into 'cuda-samples'...
remote: Enumerating objects: 19507, done.
remote: Counting objects: 100% (4227/4227), done.
remote: Compressing objects: 100% (655/655), done.
remote: Total 19507 (delta 3932), reused 3572 (delta 3572), pack-reused 15280 (from 2)
Receiving objects: 100% (19507/19507), 133.82 MiB | 17.48 MiB/s, done.
Resolving deltas: 100% (17105/17105), done.
Updating files: 100% (4026/4026), done.
❯ cd ./cuda-samples/Samples/1_Utilities/deviceQuery
❯ nano makefile
❯ make
/usr/local/cuda/bin/nvcc -ccbin g++ -I../../../Common -m64 --threads 0 --std=c++11 -gencode arch=compute_50,code=sm_50 -gencode arch=compute_52,code=sm_52 -gencode arch=compute_60,code=sm_60 -gencode arch=compute_61,code=sm_61 -gencode arch=compute_70,code=sm_70 -gencode arch=compute_75,code=sm_75 -gencode arch=compute_80,code=sm_80 -gencode arch=compute_86,code=sm_86 -gencode arch=compute_89,code=sm_89 -gencode arch=compute_90,code=sm_90 -gencode arch=compute_90,code=compute_90 -o deviceQuery.o -c deviceQuery.cpp
/usr/local/cuda/bin/nvcc -ccbin g++ -m64 -gencode arch=compute_50,code=sm_50 -gencode arch=compute_52,code=sm_52 -gencode arch=compute_60,code=sm_60 -gencode arch=compute_61,code=sm_61 -gencode arch=compute_70,code=sm_70 -gencode arch=compute_75,code=sm_75 -gencode arch=compute_80,code=sm_80 -gencode arch=compute_86,code=sm_86 -gencode arch=compute_89,code=sm_89 -gencode arch=compute_90,code=sm_90 -gencode arch=compute_90,code=compute_90 -o deviceQuery deviceQuery.o
mkdir -p ../../../bin/x86_64/linux/release
cp deviceQuery ../../../bin/x86_64/linux/release
❯  ./deviceQuery
./deviceQuery Starting...

 CUDA Device Query (Runtime API) version (CUDART static linking)

Detected 1 CUDA Capable device(s)

Device 0: "Tesla T4"
  CUDA Driver Version / Runtime Version          12.4 / 12.4
  CUDA Capability Major/Minor version number:    7.5
  Total amount of global memory:                 14918 MBytes (15642329088 bytes)
  (040) Multiprocessors, (064) CUDA Cores/MP:    2560 CUDA Cores
  GPU Max Clock rate:                            1590 MHz (1.59 GHz)
  Memory Clock rate:                             5001 Mhz
  Memory Bus Width:                              256-bit
  L2 Cache Size:                                 4194304 bytes
  Maximum Texture Dimension Size (x,y,z)         1D=(131072), 2D=(131072, 65536), 3D=(16384, 16384, 16384)
  Maximum Layered 1D Texture Size, (num) layers  1D=(32768), 2048 layers
  Maximum Layered 2D Texture Size, (num) layers  2D=(32768, 32768), 2048 layers
  Total amount of constant memory:               65536 bytes
  Total amount of shared memory per block:       49152 bytes
  Total shared memory per multiprocessor:        65536 bytes
  Total number of registers available per block: 65536
  Warp size:                                     32
  Maximum number of threads per multiprocessor:  1024
  Maximum number of threads per block:           1024
  Max dimension size of a thread block (x,y,z): (1024, 1024, 64)
  Max dimension size of a grid size    (x,y,z): (2147483647, 65535, 65535)
  Maximum memory pitch:                          2147483647 bytes
  Texture alignment:                             512 bytes
  Concurrent copy and kernel execution:          Yes with 3 copy engine(s)
  Run time limit on kernels:                     No
  Integrated GPU sharing Host Memory:            No
  Support host page-locked memory mapping:       Yes
  Alignment requirement for Surfaces:            Yes
  Device has ECC support:                        Enabled
  Device supports Unified Addressing (UVA):      Yes
  Device supports Managed Memory:                Yes
  Device supports Compute Preemption:            Yes
  Supports Cooperative Kernel Launch:            Yes
  Supports MultiDevice Co-op Kernel Launch:      Yes
  Device PCI Domain ID / Bus ID / location ID:   33247 / 0 / 0
  Compute Mode:
     < Default (multiple host threads can use ::cudaSetDevice() with device simultaneously) >

deviceQuery, CUDA Driver = CUDART, CUDA Driver Version = 12.4, CUDA Runtime Version = 12.4, NumDevs = 1
Result = PASS
❯  cd ~/cuda-samples/Samples/1_Utilities/bandwidthTest
❯ make
/usr/local/cuda/bin/nvcc -ccbin g++ -I../../../Common -m64 --threads 0 --std=c++11 -gencode arch=compute_50,code=sm_50 -gencode arch=compute_52,code=sm_52 -gencode arch=compute_60,code=sm_60 -gencode arch=compute_61,code=sm_61 -gencode arch=compute_70,code=sm_70 -gencode arch=compute_75,code=sm_75 -gencode arch=compute_80,code=sm_80 -gencode arch=compute_86,code=sm_86 -gencode arch=compute_89,code=sm_89 -gencode arch=compute_90,code=sm_90 -gencode arch=compute_90,code=compute_90 -o bandwidthTest.o -c bandwidthTest.cu
/usr/local/cuda/bin/nvcc -ccbin g++ -m64 -gencode arch=compute_50,code=sm_50 -gencode arch=compute_52,code=sm_52 -gencode arch=compute_60,code=sm_60 -gencode arch=compute_61,code=sm_61 -gencode arch=compute_70,code=sm_70 -gencode arch=compute_75,code=sm_75 -gencode arch=compute_80,code=sm_80 -gencode arch=compute_86,code=sm_86 -gencode arch=compute_89,code=sm_89 -gencode arch=compute_90,code=sm_90 -gencode arch=compute_90,code=compute_90 -o bandwidthTest bandwidthTest.o
mkdir -p ../../../bin/x86_64/linux/release
cp bandwidthTest ../../../bin/x86_64/linux/release
❯ ./bandwidthTest
[CUDA Bandwidth Test] - Starting...
Running on...

 Device 0: Tesla T4
 Quick Mode

 Host to Device Bandwidth, 1 Device(s)
 PINNED Memory Transfers
   Transfer Size (Bytes)        Bandwidth(GB/s)
   32000000                     13.1

 Device to Host Bandwidth, 1 Device(s)
 PINNED Memory Transfers
   Transfer Size (Bytes)        Bandwidth(GB/s)
   32000000                     13.2

 Device to Device Bandwidth, 1 Device(s)
 PINNED Memory Transfers
   Transfer Size (Bytes)        Bandwidth(GB/s)
   32000000                     134.9

Result = PASS

NOTE: The CUDA Samples are not meant for performance measurements. Results may vary when GPU Boost is enabled.


```

![image](https://github.com/user-attachments/assets/6723422a-3c0b-40e7-9da2-e0af06b0563c)



### iNSTALL SDK

```
╭─ ∅ /usr/lib/jvm ─────────────────────────────────────────────────────────────────────────────────────────────────────────────── 2 ✘  took 3s  with admins@studio-svr  at 06:00:30 ─╮
╰─ curl https://developer.download.nvidia.com/hpc-sdk/ubuntu/DEB-GPG-KEY-NVIDIA-HPC-SDK | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-hpcsdk-archive-keyring.gpg                      ─╯
echo 'deb [signed-by=/usr/share/keyrings/nvidia-hpcsdk-archive-keyring.gpg] https://developer.download.nvidia.com/hpc-sdk/ubuntu/amd64 /' | sudo tee /etc/apt/sources.list.d/nvhpc.list
sudo apt-get update -y
sudo apt-get install -y nvhpc-25-1-cuda-multi
[sudo] password for admins:   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  1626  100  1626    0     0   4039      0 --:--:-- --:--:-- --:--:--  4034


[sudo] password for admins:
deb [signed-by=/usr/share/keyrings/nvidia-hpcsdk-archive-keyring.gpg] https://developer.download.nvidia.com/hpc-sdk/ubuntu/amd64 /
Get:1 file:/var/cuda-repo-ubuntu2204-11-8-local  InRelease [1,575 B]
Get:2 file:/usr/share/doca-host-2.9.1-018000-24.10-ubuntu2404/repo main/ InRelease
Hit:9 http://us.archive.ubuntu.com/ubuntu noble InRelease
Get:10 http://us.archive.ubuntu.com/ubuntu noble-updates InRelease [126 kB]
Get:11 http://security.ubuntu.com/ubuntu noble-security InRelease [126 kB]
Hit:12 https://download.docker.com/linux/ubuntu noble InRelease
Get:14 https://developer.download.nvidia.com/hpc-sdk/ubuntu/amd64  InRelease [2,126 B]
Get:15 http://us.archive.ubuntu.com/ubuntu noble-backports InRelease [126 kB]
Hit:16 https://ppa.launchpadcontent.net/deadsnakes/ppa/ubuntu noble InRelease
Get:17 https://developer.download.nvidia.com/hpc-sdk/ubuntu/amd64  Packages [25.9 kB]
Hit:13 https://repos.citusdata.com/community/ubuntu jammy InRelease
Get:18 http://us.archive.ubuntu.com/ubuntu noble-updates/main amd64 Packages [783 kB]
Get:19 http://us.archive.ubuntu.com/ubuntu noble-updates/main amd64 Components [151 kB]
Get:20 http://us.archive.ubuntu.com/ubuntu noble-updates/restricted amd64 Components [212 B]
Get:21 http://us.archive.ubuntu.com/ubuntu noble-updates/universe amd64 Packages [977 kB]
Get:22 http://us.archive.ubuntu.com/ubuntu noble-updates/universe amd64 Components [313 kB]
Get:23 http://us.archive.ubuntu.com/ubuntu noble-updates/multiverse amd64 Components [940 B]
Get:24 http://us.archive.ubuntu.com/ubuntu noble-backports/main amd64 Components [208 B]
Get:25 http://us.archive.ubuntu.com/ubuntu noble-backports/restricted amd64 Components [216 B]
Get:26 http://us.archive.ubuntu.com/ubuntu noble-backports/universe amd64 Components [17.6 kB]
Get:27 http://us.archive.ubuntu.com/ubuntu noble-backports/multiverse amd64 Components [212 B]
Get:28 http://security.ubuntu.com/ubuntu noble-security/main amd64 Components [7,220 B]
Get:29 http://security.ubuntu.com/ubuntu noble-security/restricted amd64 Components [212 B]
Get:30 http://security.ubuntu.com/ubuntu noble-security/universe amd64 Components [52.0 kB]
Get:31 http://security.ubuntu.com/ubuntu noble-security/multiverse amd64 Components [212 B]
Fetched 2,709 kB in 2s (1,643 kB/s)
Reading package lists... Done
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  nvhpc-25-1
The following NEW packages will be installed:
  nvhpc-25-1 nvhpc-25-1-cuda-multi
0 upgraded, 2 newly installed, 0 to remove and 1 not upgraded.
Need to get 6,660 MB of archives.
After this operation, 24.3 GB of additional disk space will be used.
Get:1 https://developer.download.nvidia.com/hpc-sdk/ubuntu/amd64  nvhpc-25-1 25.1-0 [4,172 MB]
Get:2 https://developer.download.nvidia.com/hpc-sdk/ubuntu/amd64  nvhpc-25-1-cuda-multi 25.1-0 [2,488 MB]
Fetched 6,660 MB in 2min 43s (41.0 MB/s)
Selecting previously unselected package nvhpc-25-1.
(Reading database ... 197894 files and directories currently installed.)
Preparing to unpack .../nvhpc-25-1_25.1-0_amd64.deb ...
Unpacking nvhpc-25-1 (25.1-0) ...
Selecting previously unselected package nvhpc-25-1-cuda-multi.
Preparing to unpack .../nvhpc-25-1-cuda-multi_25.1-0_amd64.deb ...
Unpacking nvhpc-25-1-cuda-multi (25.1-0) ...
Setting up nvhpc-25-1 (25.1-0) ...
Setting up nvhpc-25-1-cuda-multi (25.1-0) ...
Scanning processes...
Scanning candidates...
Scanning linux images...

Running kernel seems to be up-to-date.

Restarting services...
 systemctl restart rstudio-server.service

Service restarts being deferred:
 systemctl restart getty@tty1.service
 systemctl restart systemd-logind.service

No containers need to be restarted.

User sessions running outdated binaries:
 admins @ session #171: bash[1931811,3143103]
 admins @ user manager service: systemd[127130]

No VM guests are running outdated hypervisor (qemu) binaries on this host.
```





![image](https://github.com/user-attachments/assets/61cb7185-33ed-4ef6-b30d-c6ab2eeb2f8d)

![image](https://github.com/user-attachments/assets/075697a6-5456-4955-bdbc-aa843fb9b01b)

![image](https://github.com/user-attachments/assets/e0a56e8a-2760-4fc9-89f3-ae338166ac0a)

### INSTALL PyCuda, CuPy, DASK, SCIKIT, SCIPY, JUPITER, NUMBA

```
admins@studio-svr:/usr/lib/python3.12$ sudo rm EXTERNALLY-MANAGED
[sudo] password for admins: 
admins@studio-svr:/usr/lib/python3.12$ pip install \
    --extra-index-url=https://pypi.nvidia.com \
    "cudf-cu12==24.12.*" "dask-cudf-cu12==24.12.*" "cuml-cu12==24.12.*" \
    "cugraph-cu12==24.12.*" "nx-cugraph-cu12==24.12.*" "cuspatial-cu12==24.12.*" \
    "cuproj-cu12==24.12.*" "cuxfilter-cu12==24.12.*" "cucim-cu12==24.12.*" \
    "pylibraft-cu12==24.12.*" "raft-dask-cu12==24.12.*" "cuvs-cu12==24.12.*" \
    "nx-cugraph-cu12==24.12.*"
Defaulting to user installation because normal site-packages is not writeable
Looking in indexes: https://pypi.org/simple, https://pypi.nvidia.com
Collecting cudf-cu12==24.12.*
  Downloading https://pypi.nvidia.com/cudf-cu12/cudf_cu12-24.12.0-cp312-cp312-manylinux_2_24_x86_64.manylinux_2_28_x86_64.whl (26.7 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 26.7/26.7 MB 17.7 MB/s eta 0:00:00
Collecting dask-cudf-cu12==24.12.*
  Downloading https://pypi.nvidia.com/dask-cudf-cu12/dask_cudf_cu12-24.12.0-py3-none-any.whl (67 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 67.2/67.2 kB 34.6 MB/s eta 0:00:00
Collecting cuml-cu12==24.12.*
  Downloading https://pypi.nvidia.com/cuml-cu12/cuml_cu12-24.12.0-cp312-cp312-manylinux_2_28_x86_64.whl (547.9 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 547.9/547.9 MB 21.5 MB/s eta 0:00:00
Collecting cugraph-cu12==24.12.*
  Downloading https://pypi.nvidia.com/cugraph-cu12/cugraph_cu12-24.12.0-cp312-cp312-manylinux_2_28_x86_64.whl (920.1 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 920.1/920.1 MB 829.6 kB/s eta 0:00:00
Collecting nx-cugraph-cu12==24.12.*
  Downloading https://pypi.nvidia.com/nx-cugraph-cu12/nx_cugraph_cu12-24.12.0-py3-none-any.whl (152 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 152.0/152.0 kB 50.7 MB/s eta 0:00:00
Collecting cuspatial-cu12==24.12.*
  Downloading https://pypi.nvidia.com/cuspatial-cu12/cuspatial_cu12-24.12.0-cp312-cp312-manylinux_2_24_x86_64.manylinux_2_28_x86_64.whl (5.0 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 5.0/5.0 MB 57.8 MB/s eta 0:00:00
Collecting cuproj-cu12==24.12.*
  Downloading https://pypi.nvidia.com/cuproj-cu12/cuproj_cu12-24.12.0-cp312-cp312-manylinux_2_24_x86_64.manylinux_2_28_x86_64.whl (914 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 914.6/914.6 kB 65.7 MB/s eta 0:00:00
Collecting cuxfilter-cu12==24.12.*
  Downloading https://pypi.nvidia.com/cuxfilter-cu12/cuxfilter_cu12-24.12.0-py3-none-any.whl (83 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 83.6/83.6 kB 37.4 MB/s eta 0:00:00
Collecting cucim-cu12==24.12.*
  Downloading https://pypi.nvidia.com/cucim-cu12/cucim_cu12-24.12.0-cp312-cp312-manylinux_2_28_x86_64.whl (5.6 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 5.6/5.6 MB 56.9 MB/s eta 0:00:00
Collecting pylibraft-cu12==24.12.*
  Downloading https://pypi.nvidia.com/pylibraft-cu12/pylibraft_cu12-24.12.0-cp312-cp312-manylinux_2_28_x86_64.whl (11.8 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 11.8/11.8 MB 22.2 MB/s eta 0:00:00
Collecting raft-dask-cu12==24.12.*
  Downloading https://pypi.nvidia.com/raft-dask-cu12/raft_dask_cu12-24.12.0-cp312-cp312-manylinux_2_28_x86_64.whl (196.9 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 196.9/196.9 MB 27.2 MB/s eta 0:00:00
Collecting cuvs-cu12==24.12.*
  Downloading https://pypi.nvidia.com/cuvs-cu12/cuvs_cu12-24.12.0-cp312-cp312-manylinux_2_28_x86_64.whl (849.7 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 849.7/849.7 MB 1.2 MB/s eta 0:00:00
Collecting cachetools (from cudf-cu12==24.12.*)
  Downloading cachetools-5.5.1-py3-none-any.whl.metadata (5.4 kB)
Collecting cuda-python<13.0a0,<=12.6.0,>=12.0 (from cudf-cu12==24.12.*)
  Downloading cuda_python-12.6.0-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (12 kB)
Collecting cupy-cuda12x>=12.0.0 (from cudf-cu12==24.12.*)
  Downloading cupy_cuda12x-13.3.0-cp312-cp312-manylinux2014_x86_64.whl.metadata (2.7 kB)
Collecting fsspec>=0.6.0 (from cudf-cu12==24.12.*)
  Downloading fsspec-2024.12.0-py3-none-any.whl.metadata (11 kB)
Collecting libcudf-cu12==24.12.* (from cudf-cu12==24.12.*)
  Downloading https://pypi.nvidia.com/libcudf-cu12/libcudf_cu12-24.12.0-py3-none-manylinux_2_28_x86_64.whl (457.8 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 457.8/457.8 MB 16.5 MB/s eta 0:00:00
Collecting numba-cuda<0.0.18,>=0.0.13 (from cudf-cu12==24.12.*)
  Downloading numba_cuda-0.0.17.1-py3-none-any.whl.metadata (1.4 kB)
Collecting numpy<3.0a0,>=1.23 (from cudf-cu12==24.12.*)
  Downloading numpy-2.2.2-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (62 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 62.0/62.0 kB 171.2 kB/s eta 0:00:00
Collecting nvtx>=0.2.1 (from cudf-cu12==24.12.*)
  Downloading nvtx-0.2.10-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (740 bytes)
Requirement already satisfied: packaging in /usr/lib/python3/dist-packages (from cudf-cu12==24.12.*) (24.0)
Collecting pandas<2.2.4dev0,>=2.0 (from cudf-cu12==24.12.*)
  Downloading pandas-2.2.3-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (89 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 89.9/89.9 kB 81.5 kB/s eta 0:00:00
Collecting pyarrow<19.0.0a0,>=14.0.0 (from cudf-cu12==24.12.*)
  Downloading pyarrow-18.1.0-cp312-cp312-manylinux_2_28_x86_64.whl.metadata (3.3 kB)
Collecting pylibcudf-cu12==24.12.* (from cudf-cu12==24.12.*)
  Downloading https://pypi.nvidia.com/pylibcudf-cu12/pylibcudf_cu12-24.12.0-cp312-cp312-manylinux_2_24_x86_64.manylinux_2_28_x86_64.whl (37.2 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 37.2/37.2 MB 16.7 MB/s eta 0:00:00
Collecting pynvjitlink-cu12 (from cudf-cu12==24.12.*)
  Downloading pynvjitlink_cu12-0.4.0-cp312-cp312-manylinux_2_27_x86_64.manylinux_2_28_x86_64.whl.metadata (1.5 kB)
Requirement already satisfied: rich in /usr/lib/python3/dist-packages (from cudf-cu12==24.12.*) (13.7.1)
Collecting rmm-cu12==24.12.* (from cudf-cu12==24.12.*)
  Downloading https://pypi.nvidia.com/rmm-cu12/rmm_cu12-24.12.1-cp312-cp312-manylinux_2_24_x86_64.manylinux_2_28_x86_64.whl (2.0 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.0/2.0 MB 65.1 MB/s eta 0:00:00
Collecting typing_extensions>=4.0.0 (from cudf-cu12==24.12.*)
  Downloading typing_extensions-4.12.2-py3-none-any.whl.metadata (3.0 kB)
Collecting pynvml<12.0.0a0,>=11.4.1 (from dask-cudf-cu12==24.12.*)
  Downloading pynvml-11.5.3-py3-none-any.whl.metadata (8.8 kB)
Collecting rapids-dask-dependency==24.12.* (from dask-cudf-cu12==24.12.*)
  Downloading https://pypi.nvidia.com/rapids-dask-dependency/rapids_dask_dependency-24.12.0-py3-none-any.whl (15 kB)
Collecting dask-cuda==24.12.* (from cuml-cu12==24.12.*)
  Downloading https://pypi.nvidia.com/dask-cuda/dask_cuda-24.12.0-py3-none-any.whl (134 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 134.4/134.4 kB 53.6 MB/s eta 0:00:00
Collecting joblib>=0.11 (from cuml-cu12==24.12.*)
  Downloading joblib-1.4.2-py3-none-any.whl.metadata (5.4 kB)
Collecting numba>=0.57 (from cuml-cu12==24.12.*)
  Downloading numba-0.61.0-cp312-cp312-manylinux2014_x86_64.manylinux_2_17_x86_64.whl.metadata (2.8 kB)
Collecting nvidia-cublas-cu12 (from cuml-cu12==24.12.*)
  Downloading https://pypi.nvidia.com/nvidia-cublas-cu12/nvidia_cublas_cu12-12.8.3.14-py3-none-manylinux_2_27_x86_64.whl (609.6 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 609.6/609.6 MB 12.8 MB/s eta 0:00:00
Collecting nvidia-cufft-cu12 (from cuml-cu12==24.12.*)
  Downloading https://pypi.nvidia.com/nvidia-cufft-cu12/nvidia_cufft_cu12-11.3.3.41-py3-none-manylinux2014_x86_64.manylinux_2_17_x86_64.whl (193.1 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 193.1/193.1 MB 31.0 MB/s eta 0:00:00
Collecting nvidia-curand-cu12 (from cuml-cu12==24.12.*)
  Downloading https://pypi.nvidia.com/nvidia-curand-cu12/nvidia_curand_cu12-10.3.9.55-py3-none-manylinux_2_27_x86_64.whl (63.6 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 63.6/63.6 MB 29.6 MB/s eta 0:00:00
Collecting nvidia-cusolver-cu12 (from cuml-cu12==24.12.*)
  Downloading https://pypi.nvidia.com/nvidia-cusolver-cu12/nvidia_cusolver_cu12-11.7.2.55-py3-none-manylinux_2_27_x86_64.whl (260.4 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 260.4/260.4 MB 33.4 MB/s eta 0:00:00
Collecting nvidia-cusparse-cu12 (from cuml-cu12==24.12.*)
  Downloading https://pypi.nvidia.com/nvidia-cusparse-cu12/nvidia_cusparse_cu12-12.5.7.53-py3-none-manylinux2014_x86_64.manylinux_2_17_x86_64.whl (292.1 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 292.1/292.1 MB 4.1 MB/s eta 0:00:00
Collecting scipy>=1.8.0 (from cuml-cu12==24.12.*)
  Downloading scipy-1.15.1-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (61 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 62.0/62.0 kB 220.2 kB/s eta 0:00:00
Collecting treelite==4.3.0 (from cuml-cu12==24.12.*)
  Downloading treelite-4.3.0-py3-none-manylinux2014_x86_64.whl.metadata (1.5 kB)
Collecting pylibcugraph-cu12==24.12.* (from cugraph-cu12==24.12.*)
  Downloading https://pypi.nvidia.com/pylibcugraph-cu12/pylibcugraph_cu12-24.12.0-cp312-cp312-manylinux_2_28_x86_64.whl (921.4 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 921.4/921.4 MB 1.7 MB/s eta 0:00:00
Collecting ucx-py-cu12==0.41.* (from cugraph-cu12==24.12.*)
  Downloading https://pypi.nvidia.com/ucx-py-cu12/ucx_py_cu12-0.41.0-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.manylinux_2_28_x86_64.whl (2.2 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.2/2.2 MB 40.8 MB/s eta 0:00:00
Collecting networkx>=3.2 (from nx-cugraph-cu12==24.12.*)
  Downloading networkx-3.4.2-py3-none-any.whl.metadata (6.3 kB)
Collecting geopandas>=1.0.0 (from cuspatial-cu12==24.12.*)
  Downloading geopandas-1.0.1-py3-none-any.whl.metadata (2.2 kB)
Collecting libcuspatial-cu12==24.12.* (from cuspatial-cu12==24.12.*)
  Downloading https://pypi.nvidia.com/libcuspatial-cu12/libcuspatial_cu12-24.12.0-py3-none-manylinux_2_24_x86_64.manylinux_2_28_x86_64.whl (17.7 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━�� 17.7/17.7 MB 25.1 MB/s eta 0:00:00
Collecting bokeh>=3.1 (from cuxfilter-cu12==24.12.*)
  Downloading bokeh-3.6.2-py3-none-any.whl.metadata (12 kB)
Collecting datashader>=0.15 (from cuxfilter-cu12==24.12.*)
  Downloading datashader-0.16.3-py2.py3-none-any.whl.metadata (12 kB)
Collecting holoviews>=1.16.0 (from cuxfilter-cu12==24.12.*)
  Downloading holoviews-1.20.0-py3-none-any.whl.metadata (9.9 kB)
Collecting jupyter-server-proxy (from cuxfilter-cu12==24.12.*)
  Downloading jupyter_server_proxy-4.4.0-py3-none-any.whl.metadata (8.7 kB)
Collecting panel>=1.0 (from cuxfilter-cu12==24.12.*)
  Downloading panel-1.6.0-py3-none-any.whl.metadata (15 kB)
Requirement already satisfied: click in /usr/lib/python3/dist-packages (from cucim-cu12==24.12.*) (8.1.6)
Collecting lazy_loader>=0.1 (from cucim-cu12==24.12.*)
  Downloading lazy_loader-0.4-py3-none-any.whl.metadata (7.6 kB)
Collecting scikit-image<0.25.0a0,>=0.19.0 (from cucim-cu12==24.12.*)
  Downloading scikit_image-0.24.0-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (14 kB)
Collecting distributed-ucxx-cu12==0.41.* (from raft-dask-cu12==24.12.*)
  Downloading https://pypi.nvidia.com/distributed-ucxx-cu12/distributed_ucxx_cu12-0.41.0-py3-none-any.whl (24 kB)
Collecting zict>=2.0.0 (from dask-cuda==24.12.*->cuml-cu12==24.12.*)
  Downloading zict-3.0.0-py2.py3-none-any.whl.metadata (899 bytes)
Collecting ucxx-cu12==0.41.* (from distributed-ucxx-cu12==0.41.*->raft-dask-cu12==24.12.*)
  Downloading https://pypi.nvidia.com/ucxx-cu12/ucxx_cu12-0.41.0-cp312-cp312-manylinux_2_27_x86_64.manylinux_2_28_x86_64.whl (828 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 829.0/829.0 kB 75.8 MB/s eta 0:00:00
Collecting libkvikio-cu12==24.12.* (from libcudf-cu12==24.12.*->cudf-cu12==24.12.*)
  Downloading https://pypi.nvidia.com/libkvikio-cu12/libkvikio_cu12-24.12.1-py3-none-manylinux_2_28_x86_64.whl (2.0 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.0/2.0 MB 47.5 MB/s eta 0:00:00
Collecting nvidia-nvcomp-cu12==4.1.0.6 (from libcudf-cu12==24.12.*->cudf-cu12==24.12.*)
  Downloading https://pypi.nvidia.com/nvidia-nvcomp-cu12/nvidia_nvcomp_cu12-4.1.0.6-py3-none-manylinux_2_28_x86_64.whl (28.9 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 28.9/28.9 MB 42.5 MB/s eta 0:00:00
Collecting dask==2024.11.2 (from rapids-dask-dependency==24.12.*->dask-cudf-cu12==24.12.*)
  Downloading dask-2024.11.2-py3-none-any.whl.metadata (3.7 kB)
Collecting distributed==2024.11.2 (from rapids-dask-dependency==24.12.*->dask-cudf-cu12==24.12.*)
  Downloading distributed-2024.11.2-py3-none-any.whl.metadata (3.3 kB)
Collecting dask-expr==1.1.19 (from rapids-dask-dependency==24.12.*->dask-cudf-cu12==24.12.*)
  Downloading dask_expr-1.1.19-py3-none-any.whl.metadata (2.6 kB)
Collecting pynvml<12.0.0a0,>=11.4.1 (from dask-cudf-cu12==24.12.*)
  Downloading pynvml-11.4.1-py3-none-any.whl.metadata (7.7 kB)
Collecting libucx-cu12<1.18,>=1.15.0 (from ucx-py-cu12==0.41.*->cugraph-cu12==24.12.*)
  Downloading libucx_cu12-1.17.0.post1-py3-none-manylinux_2_28_x86_64.whl.metadata (2.9 kB)
Collecting cloudpickle>=3.0.0 (from dask==2024.11.2->rapids-dask-dependency==24.12.*->dask-cudf-cu12==24.12.*)
  Downloading cloudpickle-3.1.1-py3-none-any.whl.metadata (7.1 kB)
Collecting partd>=1.4.0 (from dask==2024.11.2->rapids-dask-dependency==24.12.*->dask-cudf-cu12==24.12.*)
  Downloading partd-1.4.2-py3-none-any.whl.metadata (4.6 kB)
Requirement already satisfied: pyyaml>=5.3.1 in /usr/lib/python3/dist-packages (from dask==2024.11.2->rapids-dask-dependency==24.12.*->dask-cudf-cu12==24.12.*) (6.0.1)
Collecting toolz>=0.10.0 (from dask==2024.11.2->rapids-dask-dependency==24.12.*->dask-cudf-cu12==24.12.*)
  Downloading toolz-1.0.0-py3-none-any.whl.metadata (5.1 kB)
Requirement already satisfied: jinja2>=2.10.3 in /usr/lib/python3/dist-packages (from distributed==2024.11.2->rapids-dask-dependency==24.12.*->dask-cudf-cu12==24.12.*) (3.1.2)
Collecting locket>=1.0.0 (from distributed==2024.11.2->rapids-dask-dependency==24.12.*->dask-cudf-cu12==24.12.*)
  Downloading locket-1.0.0-py2.py3-none-any.whl.metadata (2.8 kB)
Collecting msgpack>=1.0.2 (from distributed==2024.11.2->rapids-dask-dependency==24.12.*->dask-cudf-cu12==24.12.*)
  Using cached msgpack-1.1.0-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (8.4 kB)
Requirement already satisfied: psutil>=5.8.0 in /usr/lib/python3/dist-packages (from distributed==2024.11.2->rapids-dask-dependency==24.12.*->dask-cudf-cu12==24.12.*) (5.9.8)
Requirement already satisfied: sortedcontainers>=2.0.5 in /usr/lib/python3/dist-packages (from distributed==2024.11.2->rapids-dask-dependency==24.12.*->dask-cudf-cu12==24.12.*) (2.4.0)
Collecting tblib>=1.6.0 (from distributed==2024.11.2->rapids-dask-dependency==24.12.*->dask-cudf-cu12==24.12.*)
  Downloading tblib-3.0.0-py3-none-any.whl.metadata (25 kB)
Collecting tornado>=6.2.0 (from distributed==2024.11.2->rapids-dask-dependency==24.12.*->dask-cudf-cu12==24.12.*)
  Downloading tornado-6.4.2-cp38-abi3-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (2.5 kB)
Requirement already satisfied: urllib3>=1.26.5 in /usr/lib/python3/dist-packages (from distributed==2024.11.2->rapids-dask-dependency==24.12.*->dask-cudf-cu12==24.12.*) (2.0.7)
Collecting libucxx-cu12==0.41.* (from ucxx-cu12==0.41.*->distributed-ucxx-cu12==0.41.*->raft-dask-cu12==24.12.*)
  Downloading https://pypi.nvidia.com/libucxx-cu12/libucxx_cu12-0.41.0-py3-none-manylinux_2_24_x86_64.manylinux_2_28_x86_64.whl (513 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 513.3/513.3 kB 22.5 MB/s eta 0:00:00
Collecting contourpy>=1.2 (from bokeh>=3.1->cuxfilter-cu12==24.12.*)
  Downloading contourpy-1.3.1-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (5.4 kB)
Collecting pillow>=7.1.0 (from bokeh>=3.1->cuxfilter-cu12==24.12.*)
  Using cached pillow-11.1.0-cp312-cp312-manylinux_2_28_x86_64.whl.metadata (9.1 kB)
Collecting xyzservices>=2021.09.1 (from bokeh>=3.1->cuxfilter-cu12==24.12.*)
  Downloading xyzservices-2025.1.0-py3-none-any.whl.metadata (4.3 kB)
Collecting fastrlock>=0.5 (from cupy-cuda12x>=12.0.0->cudf-cu12==24.12.*)
  Downloading fastrlock-0.8.3-cp312-cp312-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_28_x86_64.whl.metadata (7.7 kB)
Collecting colorcet (from datashader>=0.15->cuxfilter-cu12==24.12.*)
  Downloading colorcet-3.1.0-py3-none-any.whl.metadata (6.3 kB)
Collecting multipledispatch (from datashader>=0.15->cuxfilter-cu12==24.12.*)
  Downloading multipledispatch-1.0.0-py3-none-any.whl.metadata (3.8 kB)
Collecting param (from datashader>=0.15->cuxfilter-cu12==24.12.*)
  Downloading param-2.2.0-py3-none-any.whl.metadata (6.6 kB)
Collecting pyct (from datashader>=0.15->cuxfilter-cu12==24.12.*)
  Downloading pyct-0.5.0-py2.py3-none-any.whl.metadata (7.4 kB)
Requirement already satisfied: requests in /usr/lib/python3/dist-packages (from datashader>=0.15->cuxfilter-cu12==24.12.*) (2.31.0)
Collecting xarray (from datashader>=0.15->cuxfilter-cu12==24.12.*)
  Downloading xarray-2025.1.1-py3-none-any.whl.metadata (11 kB)
Collecting aiohttp!=4.0.0a0,!=4.0.0a1 (from fsspec[http]>=0.6.0->cugraph-cu12==24.12.*)
  Downloading aiohttp-3.11.11-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (7.7 kB)
Collecting pyogrio>=0.7.2 (from geopandas>=1.0.0->cuspatial-cu12==24.12.*)
  Downloading pyogrio-0.10.0-cp312-cp312-manylinux_2_28_x86_64.whl.metadata (5.5 kB)
Collecting pyproj>=3.3.0 (from geopandas>=1.0.0->cuspatial-cu12==24.12.*)
  Downloading pyproj-3.7.0-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (31 kB)
Collecting shapely>=2.0.0 (from geopandas>=1.0.0->cuspatial-cu12==24.12.*)
  Downloading shapely-2.0.6-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (7.0 kB)
Collecting pyviz-comms>=2.1 (from holoviews>=1.16.0->cuxfilter-cu12==24.12.*)
  Downloading pyviz_comms-3.0.4-py3-none-any.whl.metadata (7.7 kB)
Collecting llvmlite<0.45,>=0.44.0dev0 (from numba>=0.57->cuml-cu12==24.12.*)
  Downloading llvmlite-0.44.0-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (5.0 kB)
Collecting numpy<3.0a0,>=1.23 (from cudf-cu12==24.12.*)
  Downloading numpy-2.1.3-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (62 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 62.0/62.0 kB 167.4 kB/s eta 0:00:00
Requirement already satisfied: python-dateutil>=2.8.2 in /usr/lib/python3/dist-packages (from pandas<2.2.4dev0,>=2.0->cudf-cu12==24.12.*) (2.8.2)
Requirement already satisfied: pytz>=2020.1 in /usr/lib/python3/dist-packages (from pandas<2.2.4dev0,>=2.0->cudf-cu12==24.12.*) (2024.1)
Collecting tzdata>=2022.7 (from pandas<2.2.4dev0,>=2.0->cudf-cu12==24.12.*)
  Downloading tzdata-2025.1-py2.py3-none-any.whl.metadata (1.4 kB)
Collecting bleach (from panel>=1.0->cuxfilter-cu12==24.12.*)
  Downloading bleach-6.2.0-py3-none-any.whl.metadata (30 kB)
Collecting linkify-it-py (from panel>=1.0->cuxfilter-cu12==24.12.*)
  Downloading linkify_it_py-2.0.3-py3-none-any.whl.metadata (8.5 kB)
Requirement already satisfied: markdown in /usr/lib/python3/dist-packages (from panel>=1.0->cuxfilter-cu12==24.12.*) (3.5.2)
Requirement already satisfied: markdown-it-py in /usr/lib/python3/dist-packages (from panel>=1.0->cuxfilter-cu12==24.12.*) (3.0.0)
Collecting mdit-py-plugins (from panel>=1.0->cuxfilter-cu12==24.12.*)
  Downloading mdit_py_plugins-0.4.2-py3-none-any.whl.metadata (2.8 kB)
Collecting tqdm (from panel>=1.0->cuxfilter-cu12==24.12.*)
  Downloading tqdm-4.67.1-py3-none-any.whl.metadata (57 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 57.7/57.7 kB 232.3 kB/s eta 0:00:00
Collecting imageio>=2.33 (from scikit-image<0.25.0a0,>=0.19.0->cucim-cu12==24.12.*)
  Downloading imageio-2.37.0-py3-none-any.whl.metadata (5.2 kB)
Collecting tifffile>=2022.8.12 (from scikit-image<0.25.0a0,>=0.19.0->cucim-cu12==24.12.*)
  Downloading tifffile-2025.1.10-py3-none-any.whl.metadata (31 kB)
Collecting jupyter-server>=1.24.0 (from jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading jupyter_server-2.15.0-py3-none-any.whl.metadata (8.4 kB)
Collecting simpervisor>=1.0.0 (from jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading simpervisor-1.0.0-py3-none-any.whl.metadata (4.3 kB)
Collecting traitlets>=5.1.0 (from jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading traitlets-5.14.3-py3-none-any.whl.metadata (10 kB)
Collecting nvidia-nvjitlink-cu12 (from nvidia-cufft-cu12->cuml-cu12==24.12.*)
  Downloading https://pypi.nvidia.com/nvidia-nvjitlink-cu12/nvidia_nvjitlink_cu12-12.8.61-py3-none-manylinux2010_x86_64.manylinux_2_12_x86_64.whl (39.2 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 39.2/39.2 MB 60.2 MB/s eta 0:00:00
Requirement already satisfied: pygments<3.0.0,>=2.13.0 in /usr/lib/python3/dist-packages (from rich->cudf-cu12==24.12.*) (2.17.2)
Collecting aiohappyeyeballs>=2.3.0 (from aiohttp!=4.0.0a0,!=4.0.0a1->fsspec[http]>=0.6.0->cugraph-cu12==24.12.*)
  Downloading aiohappyeyeballs-2.4.4-py3-none-any.whl.metadata (6.1 kB)
Collecting aiosignal>=1.1.2 (from aiohttp!=4.0.0a0,!=4.0.0a1->fsspec[http]>=0.6.0->cugraph-cu12==24.12.*)
  Downloading aiosignal-1.3.2-py2.py3-none-any.whl.metadata (3.8 kB)
Requirement already satisfied: attrs>=17.3.0 in /usr/lib/python3/dist-packages (from aiohttp!=4.0.0a0,!=4.0.0a1->fsspec[http]>=0.6.0->cugraph-cu12==24.12.*) (23.2.0)
Collecting frozenlist>=1.1.1 (from aiohttp!=4.0.0a0,!=4.0.0a1->fsspec[http]>=0.6.0->cugraph-cu12==24.12.*)
  Downloading frozenlist-1.5.0-cp312-cp312-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (13 kB)
Collecting multidict<7.0,>=4.5 (from aiohttp!=4.0.0a0,!=4.0.0a1->fsspec[http]>=0.6.0->cugraph-cu12==24.12.*)
  Downloading multidict-6.1.0-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (5.0 kB)
Collecting propcache>=0.2.0 (from aiohttp!=4.0.0a0,!=4.0.0a1->fsspec[http]>=0.6.0->cugraph-cu12==24.12.*)
  Downloading propcache-0.2.1-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (9.2 kB)
Collecting yarl<2.0,>=1.17.0 (from aiohttp!=4.0.0a0,!=4.0.0a1->fsspec[http]>=0.6.0->cugraph-cu12==24.12.*)
  Downloading yarl-1.18.3-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (69 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 69.2/69.2 kB 145.1 kB/s eta 0:00:00
Collecting anyio>=3.1.0 (from jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading anyio-4.8.0-py3-none-any.whl.metadata (4.6 kB)
Collecting argon2-cffi>=21.1 (from jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading argon2_cffi-23.1.0-py3-none-any.whl.metadata (5.2 kB)
Collecting jupyter-client>=7.4.4 (from jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading jupyter_client-8.6.3-py3-none-any.whl.metadata (8.3 kB)
Collecting jupyter-core!=5.0.*,>=4.12 (from jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading jupyter_core-5.7.2-py3-none-any.whl.metadata (3.4 kB)
Collecting jupyter-events>=0.11.0 (from jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading jupyter_events-0.11.0-py3-none-any.whl.metadata (5.8 kB)
Collecting jupyter-server-terminals>=0.4.4 (from jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading jupyter_server_terminals-0.5.3-py3-none-any.whl.metadata (5.6 kB)
Collecting nbconvert>=6.4.4 (from jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading nbconvert-7.16.5-py3-none-any.whl.metadata (8.5 kB)
Collecting nbformat>=5.3.0 (from jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading nbformat-5.10.4-py3-none-any.whl.metadata (3.6 kB)
Collecting overrides>=5.0 (from jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading overrides-7.7.0-py3-none-any.whl.metadata (5.8 kB)
Requirement already satisfied: prometheus-client>=0.9 in /usr/lib/python3/dist-packages (from jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*) (0.19.0)
Collecting pyzmq>=24 (from jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading pyzmq-26.2.0-cp312-cp312-manylinux_2_28_x86_64.whl.metadata (6.2 kB)
Collecting send2trash>=1.8.2 (from jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading Send2Trash-1.8.3-py3-none-any.whl.metadata (4.0 kB)
Collecting terminado>=0.8.3 (from jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading terminado-0.18.1-py3-none-any.whl.metadata (5.8 kB)
Collecting websocket-client>=1.7 (from jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading websocket_client-1.8.0-py3-none-any.whl.metadata (8.0 kB)
Requirement already satisfied: mdurl~=0.1 in /usr/lib/python3/dist-packages (from markdown-it-py->panel>=1.0->cuxfilter-cu12==24.12.*) (0.1.2)
Requirement already satisfied: certifi in /usr/lib/python3/dist-packages (from pyogrio>=0.7.2->geopandas>=1.0.0->cuspatial-cu12==24.12.*) (2023.11.17)
Collecting webencodings (from bleach->panel>=1.0->cuxfilter-cu12==24.12.*)
  Downloading webencodings-0.5.1-py2.py3-none-any.whl.metadata (2.1 kB)
Collecting uc-micro-py (from linkify-it-py->panel>=1.0->cuxfilter-cu12==24.12.*)
  Downloading uc_micro_py-1.0.3-py3-none-any.whl.metadata (2.0 kB)
Requirement already satisfied: idna>=2.8 in /usr/lib/python3/dist-packages (from anyio>=3.1.0->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*) (3.6)
Collecting sniffio>=1.1 (from anyio>=3.1.0->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading sniffio-1.3.1-py3-none-any.whl.metadata (3.9 kB)
Collecting argon2-cffi-bindings (from argon2-cffi>=21.1->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading argon2_cffi_bindings-21.2.0-cp36-abi3-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (6.7 kB)
Requirement already satisfied: platformdirs>=2.5 in /usr/lib/python3/dist-packages (from jupyter-core!=5.0.*,>=4.12->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*) (4.2.0)
Collecting jsonschema>=4.18.0 (from jsonschema[format-nongpl]>=4.18.0->jupyter-events>=0.11.0->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading jsonschema-4.23.0-py3-none-any.whl.metadata (7.9 kB)
Collecting python-json-logger>=2.0.4 (from jupyter-events>=0.11.0->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading python_json_logger-3.2.1-py3-none-any.whl.metadata (4.1 kB)
Collecting referencing (from jupyter-events>=0.11.0->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading referencing-0.36.1-py3-none-any.whl.metadata (2.8 kB)
Collecting rfc3339-validator (from jupyter-events>=0.11.0->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading rfc3339_validator-0.1.4-py2.py3-none-any.whl.metadata (1.5 kB)
Collecting rfc3986-validator>=0.1.1 (from jupyter-events>=0.11.0->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading rfc3986_validator-0.1.1-py2.py3-none-any.whl.metadata (1.7 kB)
Collecting beautifulsoup4 (from nbconvert>=6.4.4->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading beautifulsoup4-4.12.3-py3-none-any.whl.metadata (3.8 kB)
Collecting defusedxml (from nbconvert>=6.4.4->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading defusedxml-0.7.1-py2.py3-none-any.whl.metadata (32 kB)
Collecting jupyterlab-pygments (from nbconvert>=6.4.4->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading jupyterlab_pygments-0.3.0-py3-none-any.whl.metadata (4.4 kB)
Requirement already satisfied: markupsafe>=2.0 in /usr/lib/python3/dist-packages (from nbconvert>=6.4.4->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*) (2.1.5)
Collecting mistune<4,>=2.0.3 (from nbconvert>=6.4.4->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading mistune-3.1.0-py3-none-any.whl.metadata (1.7 kB)
Collecting nbclient>=0.5.0 (from nbconvert>=6.4.4->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading nbclient-0.10.2-py3-none-any.whl.metadata (8.3 kB)
Collecting pandocfilters>=1.4.1 (from nbconvert>=6.4.4->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading pandocfilters-1.5.1-py2.py3-none-any.whl.metadata (9.0 kB)
Collecting fastjsonschema>=2.15 (from nbformat>=5.3.0->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Using cached fastjsonschema-2.21.1-py3-none-any.whl.metadata (2.2 kB)
Requirement already satisfied: ptyprocess in /usr/lib/python3/dist-packages (from terminado>=0.8.3->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*) (0.7.0)
Collecting tinycss2<1.5,>=1.1.0 (from bleach[css]!=5.0.0->nbconvert>=6.4.4->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading tinycss2-1.4.0-py3-none-any.whl.metadata (3.0 kB)
Collecting jsonschema-specifications>=2023.03.6 (from jsonschema>=4.18.0->jsonschema[format-nongpl]>=4.18.0->jupyter-events>=0.11.0->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading jsonschema_specifications-2024.10.1-py3-none-any.whl.metadata (3.0 kB)
Collecting rpds-py>=0.7.1 (from jsonschema>=4.18.0->jsonschema[format-nongpl]>=4.18.0->jupyter-events>=0.11.0->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading rpds_py-0.22.3-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (4.2 kB)
Collecting fqdn (from jsonschema[format-nongpl]>=4.18.0->jupyter-events>=0.11.0->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading fqdn-1.5.1-py3-none-any.whl.metadata (1.4 kB)
Collecting isoduration (from jsonschema[format-nongpl]>=4.18.0->jupyter-events>=0.11.0->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading isoduration-20.11.0-py3-none-any.whl.metadata (5.7 kB)
Requirement already satisfied: jsonpointer>1.13 in /usr/lib/python3/dist-packages (from jsonschema[format-nongpl]>=4.18.0->jupyter-events>=0.11.0->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*) (2.0)
Collecting uri-template (from jsonschema[format-nongpl]>=4.18.0->jupyter-events>=0.11.0->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading uri_template-1.3.0-py3-none-any.whl.metadata (8.8 kB)
Collecting webcolors>=24.6.0 (from jsonschema[format-nongpl]>=4.18.0->jupyter-events>=0.11.0->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading webcolors-24.11.1-py3-none-any.whl.metadata (2.2 kB)
Collecting cffi>=1.0.1 (from argon2-cffi-bindings->argon2-cffi>=21.1->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Using cached cffi-1.17.1-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (1.5 kB)
Collecting soupsieve>1.2 (from beautifulsoup4->nbconvert>=6.4.4->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading soupsieve-2.6-py3-none-any.whl.metadata (4.6 kB)
Requirement already satisfied: six in /usr/lib/python3/dist-packages (from rfc3339-validator->jupyter-events>=0.11.0->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*) (1.16.0)
Collecting pycparser (from cffi>=1.0.1->argon2-cffi-bindings->argon2-cffi>=21.1->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Using cached pycparser-2.22-py3-none-any.whl.metadata (943 bytes)
Collecting arrow>=0.15.0 (from isoduration->jsonschema[format-nongpl]>=4.18.0->jupyter-events>=0.11.0->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading arrow-1.3.0-py3-none-any.whl.metadata (7.5 kB)
Collecting types-python-dateutil>=2.8.10 (from arrow>=0.15.0->isoduration->jsonschema[format-nongpl]>=4.18.0->jupyter-events>=0.11.0->jupyter-server>=1.24.0->jupyter-server-proxy->cuxfilter-cu12==24.12.*)
  Downloading types_python_dateutil-2.9.0.20241206-py3-none-any.whl.metadata (2.1 kB)
Downloading treelite-4.3.0-py3-none-manylinux2014_x86_64.whl (915 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 916.0/916.0 kB 2.7 MB/s eta 0:00:00
Downloading dask-2024.11.2-py3-none-any.whl (1.3 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.3/1.3 MB 3.8 MB/s eta 0:00:00
Downloading dask_expr-1.1.19-py3-none-any.whl (244 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 244.5/244.5 kB 854.2 kB/s eta 0:00:00
Downloading distributed-2024.11.2-py3-none-any.whl (1.0 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.0/1.0 MB 3.0 MB/s eta 0:00:00
Downloading bokeh-3.6.2-py3-none-any.whl (6.9 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 6.9/6.9 MB 13.3 MB/s eta 0:00:00
Downloading cuda_python-12.6.0-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (24.2 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 24.2/24.2 MB 11.8 MB/s eta 0:00:00
Downloading cupy_cuda12x-13.3.0-cp312-cp312-manylinux2014_x86_64.whl (91.0 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 91.0/91.0 MB 3.7 MB/s eta 0:00:00
Downloading datashader-0.16.3-py2.py3-none-any.whl (18.3 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 18.3/18.3 MB 15.8 MB/s eta 0:00:00
Downloading fsspec-2024.12.0-py3-none-any.whl (183 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 183.9/183.9 kB 730.0 kB/s eta 0:00:00
Downloading geopandas-1.0.1-py3-none-any.whl (323 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 323.6/323.6 kB 2.0 MB/s eta 0:00:00
Downloading holoviews-1.20.0-py3-none-any.whl (5.0 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 5.0/5.0 MB 13.4 MB/s eta 0:00:00
Downloading joblib-1.4.2-py3-none-any.whl (301 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 301.8/301.8 kB 1.1 MB/s eta 0:00:00
Downloading lazy_loader-0.4-py3-none-any.whl (12 kB)
Downloading networkx-3.4.2-py3-none-any.whl (1.7 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.7/1.7 MB 2.5 MB/s eta 0:00:00
Downloading numba-0.61.0-cp312-cp312-manylinux2014_x86_64.manylinux_2_17_x86_64.whl (3.9 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 3.9/3.9 MB 3.1 MB/s eta 0:00:00
Downloading numba_cuda-0.0.17.1-py3-none-any.whl (424 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 424.7/424.7 kB 494.3 kB/s eta 0:00:00
Downloading numpy-2.1.3-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (16.0 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 16.0/16.0 MB 7.2 MB/s eta 0:00:00
Downloading nvtx-0.2.10-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (695 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 695.5/695.5 kB 2.3 MB/s eta 0:00:00
Downloading pandas-2.2.3-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (12.7 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 12.7/12.7 MB 17.7 MB/s eta 0:00:00
Downloading panel-1.6.0-py3-none-any.whl (27.9 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 27.9/27.9 MB 11.0 MB/s eta 0:00:00
Downloading pyarrow-18.1.0-cp312-cp312-manylinux_2_28_x86_64.whl (40.1 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 40.1/40.1 MB 4.3 MB/s eta 0:00:00
Downloading pynvml-11.4.1-py3-none-any.whl (46 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 47.0/47.0 kB 135.9 kB/s eta 0:00:00
Downloading scikit_image-0.24.0-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (15.0 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 15.0/15.0 MB 7.6 MB/s eta 0:00:00
Downloading scipy-1.15.1-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (40.2 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 40.2/40.2 MB 10.2 MB/s eta 0:00:00
Downloading typing_extensions-4.12.2-py3-none-any.whl (37 kB)
Downloading cachetools-5.5.1-py3-none-any.whl (9.5 kB)
Downloading jupyter_server_proxy-4.4.0-py3-none-any.whl (37 kB)
Downloading pynvjitlink_cu12-0.4.0-cp312-cp312-manylinux_2_27_x86_64.manylinux_2_28_x86_64.whl (24.2 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 24.2/24.2 MB 11.1 MB/s eta 0:00:00
Downloading aiohttp-3.11.11-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.7 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.7/1.7 MB 7.2 MB/s eta 0:00:00
Downloading contourpy-1.3.1-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (323 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 323.6/323.6 kB 1.1 MB/s eta 0:00:00
Downloading fastrlock-0.8.3-cp312-cp312-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_28_x86_64.whl (53 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 53.9/53.9 kB 48.4 kB/s eta 0:00:00
Downloading imageio-2.37.0-py3-none-any.whl (315 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 315.8/315.8 kB 298.9 kB/s eta 0:00:00
Downloading jupyter_server-2.15.0-py3-none-any.whl (385 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 385.8/385.8 kB 481.1 kB/s eta 0:00:00
Downloading libucx_cu12-1.17.0.post1-py3-none-manylinux_2_28_x86_64.whl (26.9 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 26.9/26.9 MB 740.5 kB/s eta 0:00:00
Downloading llvmlite-0.44.0-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (42.4 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42.4/42.4 MB 2.6 MB/s eta 0:00:00
Downloading param-2.2.0-py3-none-any.whl (119 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 119.0/119.0 kB 270.0 kB/s eta 0:00:00
Using cached pillow-11.1.0-cp312-cp312-manylinux_2_28_x86_64.whl (4.5 MB)
Downloading pyogrio-0.10.0-cp312-cp312-manylinux_2_28_x86_64.whl (24.0 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 24.0/24.0 MB 6.8 MB/s eta 0:00:00
Downloading pyproj-3.7.0-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (9.5 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 9.5/9.5 MB 7.9 MB/s eta 0:00:00
Downloading pyviz_comms-3.0.4-py3-none-any.whl (83 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 83.8/83.8 kB 76.5 kB/s eta 0:00:00
Downloading shapely-2.0.6-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (2.5 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.5/2.5 MB 2.4 MB/s eta 0:00:00
Downloading simpervisor-1.0.0-py3-none-any.whl (8.3 kB)
Downloading tifffile-2025.1.10-py3-none-any.whl (227 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 227.6/227.6 kB 570.5 kB/s eta 0:00:00
Downloading toolz-1.0.0-py3-none-any.whl (56 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 56.4/56.4 kB 166.2 kB/s eta 0:00:00
Downloading tornado-6.4.2-cp38-abi3-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (437 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 437.2/437.2 kB 1.2 MB/s eta 0:00:00
Downloading traitlets-5.14.3-py3-none-any.whl (85 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 85.4/85.4 kB 235.4 kB/s eta 0:00:00
Downloading tzdata-2025.1-py2.py3-none-any.whl (346 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 346.8/346.8 kB 821.1 kB/s eta 0:00:00
Downloading xyzservices-2025.1.0-py3-none-any.whl (88 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 88.4/88.4 kB 20.7 kB/s eta 0:00:00
Downloading zict-3.0.0-py2.py3-none-any.whl (43 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 43.3/43.3 kB 37.9 kB/s eta 0:00:00
Downloading bleach-6.2.0-py3-none-any.whl (163 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 163.4/163.4 kB 149.4 kB/s eta 0:00:00
Downloading colorcet-3.1.0-py3-none-any.whl (260 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 260.3/260.3 kB 187.1 kB/s eta 0:00:00
Downloading linkify_it_py-2.0.3-py3-none-any.whl (19 kB)
Downloading mdit_py_plugins-0.4.2-py3-none-any.whl (55 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 55.3/55.3 kB 160.7 kB/s eta 0:00:00
Downloading multipledispatch-1.0.0-py3-none-any.whl (12 kB)
Downloading pyct-0.5.0-py2.py3-none-any.whl (15 kB)
Downloading tqdm-4.67.1-py3-none-any.whl (78 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 78.5/78.5 kB 289.8 kB/s eta 0:00:00
Downloading xarray-2025.1.1-py3-none-any.whl (1.2 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.2/1.2 MB 4.8 MB/s eta 0:00:00
Downloading aiohappyeyeballs-2.4.4-py3-none-any.whl (14 kB)
Downloading aiosignal-1.3.2-py2.py3-none-any.whl (7.6 kB)
Downloading anyio-4.8.0-py3-none-any.whl (96 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 96.0/96.0 kB 258.1 kB/s eta 0:00:00
Downloading argon2_cffi-23.1.0-py3-none-any.whl (15 kB)
Downloading cloudpickle-3.1.1-py3-none-any.whl (20 kB)
Downloading frozenlist-1.5.0-cp312-cp312-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (283 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 283.6/283.6 kB 283.8 kB/s eta 0:00:00
Downloading jupyter_client-8.6.3-py3-none-any.whl (106 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 106.1/106.1 kB 98.2 kB/s eta 0:00:00
Downloading jupyter_core-5.7.2-py3-none-any.whl (28 kB)
Downloading jupyter_events-0.11.0-py3-none-any.whl (19 kB)
Downloading jupyter_server_terminals-0.5.3-py3-none-any.whl (13 kB)
Downloading locket-1.0.0-py2.py3-none-any.whl (4.4 kB)
Using cached msgpack-1.1.0-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (401 kB)
Downloading multidict-6.1.0-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (131 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 131.0/131.0 kB 485.6 kB/s eta 0:00:00
Downloading nbconvert-7.16.5-py3-none-any.whl (258 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 258.1/258.1 kB 1.1 MB/s eta 0:00:00
Downloading nbformat-5.10.4-py3-none-any.whl (78 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 78.5/78.5 kB 225.4 kB/s eta 0:00:00
Downloading overrides-7.7.0-py3-none-any.whl (17 kB)
Downloading partd-1.4.2-py3-none-any.whl (18 kB)
Downloading propcache-0.2.1-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (243 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 243.6/243.6 kB 912.0 kB/s eta 0:00:00
Downloading pyzmq-26.2.0-cp312-cp312-manylinux_2_28_x86_64.whl (860 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 860.6/860.6 kB 3.1 MB/s eta 0:00:00
Downloading Send2Trash-1.8.3-py3-none-any.whl (18 kB)
Downloading tblib-3.0.0-py3-none-any.whl (12 kB)
Downloading terminado-0.18.1-py3-none-any.whl (14 kB)
Downloading websocket_client-1.8.0-py3-none-any.whl (58 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 58.8/58.8 kB 145.0 kB/s eta 0:00:00
Downloading yarl-1.18.3-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (336 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 336.9/336.9 kB 943.2 kB/s eta 0:00:00
Downloading uc_micro_py-1.0.3-py3-none-any.whl (6.2 kB)
Downloading webencodings-0.5.1-py2.py3-none-any.whl (11 kB)
Using cached fastjsonschema-2.21.1-py3-none-any.whl (23 kB)
Downloading jsonschema-4.23.0-py3-none-any.whl (88 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 88.5/88.5 kB 160.1 kB/s eta 0:00:00
Downloading mistune-3.1.0-py3-none-any.whl (53 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 53.7/53.7 kB 113.2 kB/s eta 0:00:00
Downloading nbclient-0.10.2-py3-none-any.whl (25 kB)
Downloading pandocfilters-1.5.1-py2.py3-none-any.whl (8.7 kB)
Downloading python_json_logger-3.2.1-py3-none-any.whl (14 kB)
Downloading referencing-0.36.1-py3-none-any.whl (26 kB)
Downloading rfc3986_validator-0.1.1-py2.py3-none-any.whl (4.2 kB)
Downloading sniffio-1.3.1-py3-none-any.whl (10 kB)
Downloading argon2_cffi_bindings-21.2.0-cp36-abi3-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (86 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 86.2/86.2 kB 262.5 kB/s eta 0:00:00
Downloading beautifulsoup4-4.12.3-py3-none-any.whl (147 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 147.9/147.9 kB 349.8 kB/s eta 0:00:00
Downloading defusedxml-0.7.1-py2.py3-none-any.whl (25 kB)
Downloading jupyterlab_pygments-0.3.0-py3-none-any.whl (15 kB)
Downloading rfc3339_validator-0.1.4-py2.py3-none-any.whl (3.5 kB)
Using cached cffi-1.17.1-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (479 kB)
Downloading jsonschema_specifications-2024.10.1-py3-none-any.whl (18 kB)
Downloading rpds_py-0.22.3-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (385 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 385.7/385.7 kB 988.7 kB/s eta 0:00:00
Downloading soupsieve-2.6-py3-none-any.whl (36 kB)
Downloading tinycss2-1.4.0-py3-none-any.whl (26 kB)
Downloading webcolors-24.11.1-py3-none-any.whl (14 kB)
Downloading fqdn-1.5.1-py3-none-any.whl (9.1 kB)
Downloading isoduration-20.11.0-py3-none-any.whl (11 kB)
Downloading uri_template-1.3.0-py3-none-any.whl (11 kB)
Downloading arrow-1.3.0-py3-none-any.whl (66 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 66.4/66.4 kB 190.6 kB/s eta 0:00:00
Using cached pycparser-2.22-py3-none-any.whl (117 kB)
Downloading types_python_dateutil-2.9.0.20241206-py3-none-any.whl (14 kB)
Installing collected packages: webencodings, nvtx, multipledispatch, libkvikio-cu12, fastrlock, fastjsonschema, cuda-python, zict, xyzservices, websocket-client, webcolors, uri-template, uc-micro-py, tzdata, typing_extensions, types-python-dateutil, traitlets, tqdm, tornado, toolz, tinycss2, tblib, soupsieve, sniffio, simpervisor, send2trash, rpds-py, rfc3986-validator, rfc3339-validator, pyzmq, python-json-logger, pyproj, pynvml, pynvjitlink-cu12, pycparser, pyarrow, propcache, pillow, param, pandocfilters, overrides, nvidia-nvjitlink-cu12, nvidia-nvcomp-cu12, nvidia-curand-cu12, nvidia-cublas-cu12, numpy, networkx, multidict, msgpack, mistune, locket, llvmlite, libucx-cu12, lazy_loader, jupyterlab-pygments, joblib, fsspec, frozenlist, fqdn, defusedxml, colorcet, cloudpickle, cachetools, bleach, aiohappyeyeballs, yarl, ucx-py-cu12, tifffile, terminado, shapely, scipy, referencing, pyviz-comms, pyogrio, pyct, partd, pandas, nvidia-cusparse-cu12, nvidia-cufft-cu12, numba, mdit-py-plugins, linkify-it-py, libucxx-cu12, libcudf-cu12, jupyter-core, imageio, cupy-cuda12x, contourpy, cffi, beautifulsoup4, arrow, anyio, aiosignal, xarray, treelite, scikit-image, rmm-cu12, nvidia-cusolver-cu12, numba-cuda, libcuspatial-cu12, jupyter-server-terminals, jupyter-client, jsonschema-specifications, isoduration, geopandas, dask, cuproj-cu12, bokeh, argon2-cffi-bindings, aiohttp, ucxx-cu12, pylibraft-cu12, pylibcudf-cu12, panel, jsonschema, distributed, datashader, dask-expr, cucim-cu12, argon2-cffi, rapids-dask-dependency, pylibcugraph-cu12, nbformat, holoviews, cuvs-cu12, cudf-cu12, nx-cugraph-cu12, nbclient, jupyter-events, distributed-ucxx-cu12, dask-cudf-cu12, dask-cuda, cuspatial-cu12, raft-dask-cu12, nbconvert, jupyter-server, cuml-cu12, cugraph-cu12, jupyter-server-proxy, cuxfilter-cu12
Successfully installed aiohappyeyeballs-2.4.4 aiohttp-3.11.11 aiosignal-1.3.2 anyio-4.8.0 argon2-cffi-23.1.0 argon2-cffi-bindings-21.2.0 arrow-1.3.0 beautifulsoup4-4.12.3 bleach-6.2.0 bokeh-3.6.2 cachetools-5.5.1 cffi-1.17.1 cloudpickle-3.1.1 colorcet-3.1.0 contourpy-1.3.1 cucim-cu12-24.12.0 cuda-python-12.6.0 cudf-cu12-24.12.0 cugraph-cu12-24.12.0 cuml-cu12-24.12.0 cuproj-cu12-24.12.0 cupy-cuda12x-13.3.0 cuspatial-cu12-24.12.0 cuvs-cu12-24.12.0 cuxfilter-cu12-24.12.0 dask-2024.11.2 dask-cuda-24.12.0 dask-cudf-cu12-24.12.0 dask-expr-1.1.19 datashader-0.16.3 defusedxml-0.7.1 distributed-2024.11.2 distributed-ucxx-cu12-0.41.0 fastjsonschema-2.21.1 fastrlock-0.8.3 fqdn-1.5.1 frozenlist-1.5.0 fsspec-2024.12.0 geopandas-1.0.1 holoviews-1.20.0 imageio-2.37.0 isoduration-20.11.0 joblib-1.4.2 jsonschema-4.23.0 jsonschema-specifications-2024.10.1 jupyter-client-8.6.3 jupyter-core-5.7.2 jupyter-events-0.11.0 jupyter-server-2.15.0 jupyter-server-proxy-4.4.0 jupyter-server-terminals-0.5.3 jupyterlab-pygments-0.3.0 lazy_loader-0.4 libcudf-cu12-24.12.0 libcuspatial-cu12-24.12.0 libkvikio-cu12-24.12.1 libucx-cu12-1.17.0.post1 libucxx-cu12-0.41.0 linkify-it-py-2.0.3 llvmlite-0.44.0 locket-1.0.0 mdit-py-plugins-0.4.2 mistune-3.1.0 msgpack-1.1.0 multidict-6.1.0 multipledispatch-1.0.0 nbclient-0.10.2 nbconvert-7.16.5 nbformat-5.10.4 networkx-3.4.2 numba-0.61.0 numba-cuda-0.0.17.1 numpy-2.1.3 nvidia-cublas-cu12-12.8.3.14 nvidia-cufft-cu12-11.3.3.41 nvidia-curand-cu12-10.3.9.55 nvidia-cusolver-cu12-11.7.2.55 nvidia-cusparse-cu12-12.5.7.53 nvidia-nvcomp-cu12-4.1.0.6 nvidia-nvjitlink-cu12-12.8.61 nvtx-0.2.10 nx-cugraph-cu12-24.12.0 overrides-7.7.0 pandas-2.2.3 pandocfilters-1.5.1 panel-1.6.0 param-2.2.0 partd-1.4.2 pillow-11.1.0 propcache-0.2.1 pyarrow-18.1.0 pycparser-2.22 pyct-0.5.0 pylibcudf-cu12-24.12.0 pylibcugraph-cu12-24.12.0 pylibraft-cu12-24.12.0 pynvjitlink-cu12-0.4.0 pynvml-11.4.1 pyogrio-0.10.0 pyproj-3.7.0 python-json-logger-3.2.1 pyviz-comms-3.0.4 pyzmq-26.2.0 raft-dask-cu12-24.12.0 rapids-dask-dependency-24.12.0 referencing-0.36.1 rfc3339-validator-0.1.4 rfc3986-validator-0.1.1 rmm-cu12-24.12.1 rpds-py-0.22.3 scikit-image-0.24.0 scipy-1.15.1 send2trash-1.8.3 shapely-2.0.6 simpervisor-1.0.0 sniffio-1.3.1 soupsieve-2.6 tblib-3.0.0 terminado-0.18.1 tifffile-2025.1.10 tinycss2-1.4.0 toolz-1.0.0 tornado-6.4.2 tqdm-4.67.1 traitlets-5.14.3 treelite-4.3.0 types-python-dateutil-2.9.0.20241206 typing_extensions-4.12.2 tzdata-2025.1 uc-micro-py-1.0.3 ucx-py-cu12-0.41.0 ucxx-cu12-0.41.0 uri-template-1.3.0 webcolors-24.11.1 webencodings-0.5.1 websocket-client-1.8.0 xarray-2025.1.1 xyzservices-2025.1.0 yarl-1.18.3 zict-3.0.0
/home/admins/.zshrc:export:135: not valid in this context: PATH:/usr/lib/jvm/g-vm-java11-20.0.0/bin
❯ sudo apt install  libfreetype6-dev libpng-dev libtiff5-dev libjpeg-dev
[sudo] password for admins: 
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Note, selecting 'libfreetype-dev' instead of 'libfreetype6-dev'
libfreetype-dev is already the newest version (2.13.2+dfsg-1build3).
libfreetype-dev set to manually installed.
libpng-dev is already the newest version (1.6.43-5build1).
libpng-dev set to manually installed.
libjpeg-dev is already the newest version (8c-2ubuntu11).
libjpeg-dev set to manually installed.
The following additional packages will be installed:
  libjbig-dev liblerc-dev libsharpyuv-dev libtiff-dev libtiffxx6 libwebp-dev libwebpdecoder3 libwebpdemux2 libwebpmux3
The following NEW packages will be installed:
  libjbig-dev liblerc-dev libsharpyuv-dev libtiff-dev libtiff5-dev libtiffxx6 libwebp-dev libwebpdecoder3 libwebpdemux2 libwebpmux3
0 upgraded, 10 newly installed, 0 to remove and 1 not upgraded.
Need to get 1,091 kB of archives.
After this operation, 4,399 kB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://us.archive.ubuntu.com/ubuntu noble/main amd64 liblerc-dev amd64 4.0.0+ds-4ubuntu2 [182 kB]
Get:2 http://us.archive.ubuntu.com/ubuntu noble/main amd64 libsharpyuv-dev amd64 1.3.2-0.4build3 [16.0 kB]
Get:3 http://us.archive.ubuntu.com/ubuntu noble/main amd64 libjbig-dev amd64 2.1-6.1ubuntu2 [27.9 kB]
Get:4 http://us.archive.ubuntu.com/ubuntu noble/main amd64 libwebpdemux2 amd64 1.3.2-0.4build3 [12.4 kB]
Get:5 http://us.archive.ubuntu.com/ubuntu noble/main amd64 libwebpmux3 amd64 1.3.2-0.4build3 [25.7 kB]
Get:6 http://us.archive.ubuntu.com/ubuntu noble/main amd64 libwebpdecoder3 amd64 1.3.2-0.4build3 [114 kB]
Get:7 http://us.archive.ubuntu.com/ubuntu noble/main amd64 libwebp-dev amd64 1.3.2-0.4build3 [367 kB]
Get:8 http://us.archive.ubuntu.com/ubuntu noble-updates/main amd64 libtiffxx6 amd64 4.5.1+git230720-4ubuntu2.2 [5,644 B]
Get:9 http://us.archive.ubuntu.com/ubuntu noble-updates/main amd64 libtiff-dev amd64 4.5.1+git230720-4ubuntu2.2 [338 kB]
Get:10 http://us.archive.ubuntu.com/ubuntu noble-updates/main amd64 libtiff5-dev amd64 4.5.1+git230720-4ubuntu2.2 [2,154 B]
Fetched 1,091 kB in 1s (1,365 kB/s)       
Selecting previously unselected package liblerc-dev:amd64.
(Reading database ... 197734 files and directories currently installed.)
Preparing to unpack .../0-liblerc-dev_4.0.0+ds-4ubuntu2_amd64.deb ...
Unpacking liblerc-dev:amd64 (4.0.0+ds-4ubuntu2) ........................................................................................................................................] 
Selecting previously unselected package libsharpyuv-dev:amd64...........................................................................................................................] 
Preparing to unpack .../1-libsharpyuv-dev_1.3.2-0.4build3_amd64.deb ...
Unpacking libsharpyuv-dev:amd64 (1.3.2-0.4build3) ......................................................................................................................................] 
Selecting previously unselected package libjbig-dev:amd64...............................................................................................................................] 
Preparing to unpack .../2-libjbig-dev_2.1-6.1ubuntu2_amd64.deb ...
Unpacking libjbig-dev:amd64 (2.1-6.1ubuntu2) ...........................................................................................................................................] 
Selecting previously unselected package libwebpdemux2:amd64.............................................................................................................................] 
Preparing to unpack .../3-libwebpdemux2_1.3.2-0.4build3_amd64.deb ...
Unpacking libwebpdemux2:amd64 (1.3.2-0.4build3) ........................................................................................................................................] 
Selecting previously unselected package libwebpmux3:amd64...............................................................................................................................] 
Preparing to unpack .../4-libwebpmux3_1.3.2-0.4build3_amd64.deb ...
Unpacking libwebpmux3:amd64 (1.3.2-0.4build3) ...#####..................................................................................................................................] 
Selecting previously unselected package libwebpdecoder3:amd64...........................................................................................................................] 
Preparing to unpack .../5-libwebpdecoder3_1.3.2-0.4build3_amd64.deb ...
Unpacking libwebpdecoder3:amd64 (1.3.2-0.4build3) ...#########..........................................................................................................................] 
Selecting previously unselected package libwebp-dev:amd64.########......................................................................................................................] 
Preparing to unpack .../6-libwebp-dev_1.3.2-0.4build3_amd64.deb ...
Unpacking libwebp-dev:amd64 (1.3.2-0.4build3) ...#####################..................................................................................................................] 
Selecting previously unselected package libtiffxx6:amd64.#################..............................................................................................................] 
Preparing to unpack .../7-libtiffxx6_4.5.1+git230720-4ubuntu2.2_amd64.deb ...
Unpacking libtiffxx6:amd64 (4.5.1+git230720-4ubuntu2.2) ...###################..........................................................................................................] 
Selecting previously unselected package libtiff-dev:amd64.########################......................................................................................................] 
Preparing to unpack .../8-libtiff-dev_4.5.1+git230720-4ubuntu2.2_amd64.deb ...
Unpacking libtiff-dev:amd64 (4.5.1+git230720-4ubuntu2.2) ...##########################..................................................................................................] 
Selecting previously unselected package libtiff5-dev:amd64.###############################..............................................................................................] 
Preparing to unpack .../9-libtiff5-dev_4.5.1+git230720-4ubuntu2.2_amd64.deb ...
Unpacking libtiff5-dev:amd64 (4.5.1+git230720-4ubuntu2.2) ...#################################..........................................................................................] 
Setting up libwebpdemux2:amd64 (1.3.2-0.4build3) ...##############################################......................................................................................] 
Setting up libjbig-dev:amd64 (2.1-6.1ubuntu2) ...##########################################################.............................................................................] 
Setting up libwebpdecoder3:amd64 (1.3.2-0.4build3) ...#############################################################.....................................................................] 
Setting up liblerc-dev:amd64 (4.0.0+ds-4ubuntu2) ...#######################################################################.............................................................] 
Setting up libsharpyuv-dev:amd64 (1.3.2-0.4build3) ...#############################################################################.....................................................] 
Setting up libwebpmux3:amd64 (1.3.2-0.4build3) ...#########################################################################################.............................................] 
Setting up libtiffxx6:amd64 (4.5.1+git230720-4ubuntu2.2) ...#######################################################################################.....................................] 
Setting up libwebp-dev:amd64 (1.3.2-0.4build3) ...#########################################################################################################.............................] 
Setting up libtiff-dev:amd64 (4.5.1+git230720-4ubuntu2.2) ...######################################################################################################.....................] 
Setting up libtiff5-dev:amd64 (4.5.1+git230720-4ubuntu2.2) ...#############################################################################################################.............] 
Processing triggers for libc-bin (2.39-0ubuntu8.3) ...#############################################################################################################################.....] 
Processing triggers for man-db (2.12.0-4build2) ...
Scanning processes...                                                                                                                                                                       
Scanning candidates...                                                                                                                                                                      
Scanning linux images...                                                                                                                                                                    
```

![image](https://github.com/user-attachments/assets/162598ce-300e-463f-9ed4-e40d92a54440)


### INSTALL  CuPy, CuDNN, NCCL,CuTensor

```
pip install cupy-cuda12x
Defaulting to user installation because normal site-packages is not writeable
Requirement already satisfied: cupy-cuda12x in /home/admins/.local/lib/python3.12/site-packages (13.3.0)
Requirement already satisfied: numpy<2.3,>=1.22 in /home/admins/.local/lib/python3.12/site-packages (from cupy-cuda12x) (2.1.3)
Requirement already satisfied: fastrlock>=0.5 in /home/admins/.local/lib/python3.12/site-packages (from cupy-cuda12x) (0.8.3)

╭─ ∅ /usr/lib/jvm ───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────── 2 ✘  with admins@studio-svr  at 05:37:26 ─╮
╰─ python -m cupyx.tools.install_library --cuda 12.x --library cutensor                                                                                                                    ─╯
By downloading and using cuTENSOR, you accept the terms and conditions of the NVIDIA cuTENSOR Software License Agreement:
  https://docs.nvidia.com/cuda/cutensor/license.html

Installing cutensor 2.0.1 for CUDA 12.x to: /home/admins/.cupy/cuda_lib/12.x/cutensor/2.0.1
Downloading https://developer.download.nvidia.com/compute/cutensor/redist/libcutensor/linux-x86_64/libcutensor-linux-x86_64-2.0.1.2-archive.tar.xz...
Extracting...
Installing...
Cleaning up...
Done!

╭─ ∅ /usr/lib/jvm ───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────── 2 ✘  with admins@studio-svr  at 05:41:10 ─╮
╰─  python -m cupyx.tools.install_library --cuda 12.x --library cudnn                                                                                                                      ─╯
By downloading and using cuDNN, you accept the terms and conditions of the NVIDIA cuDNN Software License Agreement:
  https://docs.nvidia.com/deeplearning/cudnn/sla/index.html

Installing cudnn 8.8.1 for CUDA 12.x to: /home/admins/.cupy/cuda_lib/12.x/cudnn/8.8.1
Downloading https://developer.download.nvidia.com/compute/cudnn/redist/cudnn/linux-x86_64/cudnn-linux-x86_64-8.8.1.3_cuda12-archive.tar.xz...
Extracting...
Installing...
Cleaning up...
Done!
╭─ ∅ /usr/lib/jvm ───────────────────────────────────────────────────────────────────────────────────────────────────────────── ✔  took 2m 57s  with admins@studio-svr  at 05:44:16 ─╮
╰─  python -m cupyx.tools.install_library --cuda 12.x --library nccl                                                                                                                       ─╯
Installing nccl 2.16.2 for CUDA 12.x to: /home/admins/.cupy/cuda_lib/12.x/nccl/2.16.2
Downloading https://developer.download.nvidia.com/compute/redist/nccl/v2.16.2/nccl_2.16.2-1+cuda12.0_x86_64.txz...
Extracting...
Installing...
Cleaning up...
Done!
╭─ ∅ /usr/lib/jvm ──────────────────────────────────────────────────────────────────────────────────────────────────────────────── ✔  took 34s  with admins@studio-svr  at 05:45:29 ─╮
╰─ pip install fireducks                                                                                                                                                                   ─╯
Defaulting to user installation because normal site-packages is not writeable
Collecting fireducks
  Downloading fireducks-1.1.8-cp312-cp312-manylinux_2_28_x86_64.whl.metadata (1.0 kB)
Collecting firefw==1.1.8 (from fireducks)
  Downloading firefw-1.1.8-py3-none-any.whl.metadata (818 bytes)
Requirement already satisfied: pandas<2.3.0,>=1.5.3 in /home/admins/.local/lib/python3.12/site-packages (from fireducks) (2.2.3)
Requirement already satisfied: pyarrow<18.2,>=18.1 in /home/admins/.local/lib/python3.12/site-packages (from fireducks) (18.1.0)
Requirement already satisfied: numpy>=1.26.0 in /home/admins/.local/lib/python3.12/site-packages (from pandas<2.3.0,>=1.5.3->fireducks) (2.1.3)
Requirement already satisfied: python-dateutil>=2.8.2 in /usr/lib/python3/dist-packages (from pandas<2.3.0,>=1.5.3->fireducks) (2.8.2)
Requirement already satisfied: pytz>=2020.1 in /usr/lib/python3/dist-packages (from pandas<2.3.0,>=1.5.3->fireducks) (2024.1)
Requirement already satisfied: tzdata>=2022.7 in /home/admins/.local/lib/python3.12/site-packages (from pandas<2.3.0,>=1.5.3->fireducks) (2025.1)
Downloading fireducks-1.1.8-cp312-cp312-manylinux_2_28_x86_64.whl (7.2 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 7.2/7.2 MB 8.1 MB/s eta 0:00:00
Downloading firefw-1.1.8-py3-none-any.whl (12 kB)
Installing collected packages: firefw, fireducks
Successfully installed fireducks-1.1.8 firefw-1.1.8
╭─ ∅ /usr/lib/jvm ──────────────────────────────────────────────────────────────────────────────────────────────────────────────── ✔  took 37s  with admins@studio-svr  at 06:00:11 ─╮
╰─ python3 -m fireducks.pandas your_script.py            
─╯
```
