# `phcpy` installation instructions

```console
sudo apt update
sudo apt install curl build-essential
cd ~/Downloads/
curl -L "https://repo.continuum.io/archive/Anaconda3-4.4.0-Linux-x86_64.sh" > anaconda.sh
bash anaconda.sh (installs in /home/$USER/anaconda3; prepend install path to .bashrc)
source ~/.bashrc
conda create --name phcpy numpy matplotlib sympy jupyter scipy pytest

cd ~/Downloads/
curl -L "http://crd.lbl.gov/~dhbailey/mpdist/qd-2.3.17.tar.gz" > qd.tar.gz
tar zxvf qd.tar.gz
cd qd-2.3.17
./configure CXX=/usr/bin/g++ CXXFLAGS="-fPIC -O3"
make
sudo make install (installs in /usr/local/lib)

cd ~/Downloads/
curl -L "http://mirrors.cdn.adacore.com/art/591c6d80c7a447af2deed1d7" > gnat-gpl.tar.gz
tar zxvf gnat-gpl.tar.gz
cd gnat-gpl-2017-x86_64-linux-bin/
sudo ./doinstall (installs in /usr/gnat)
sed -i '$ a\PATH="/usr/gnat/bin:$PATH"; export PATH' ~/.bashrc
source ~/.bashrc

cd ~/Downloads/
curl -L "https://github.com/janverschelde/PHCpack/archive/v2.4.40.tar.gz" > PHC.tar.gz
tar zxvf PHC.tar.gz
cd PHCpack-2.4.40/src/Objects
set MAKEFILE = makefile_unix in makefile
inside makefile_unix, set
  PYTHON3=/home/berceanu/anaconda3/envs/phcpy/include/python3.6m
  ADALIB=/usr/gnat/lib/gcc/x86_64-pc-linux-gnu/6.3.1/adalib
make clean
make phcpy2c3.so
cd ../Python/PHCpy3
source activate phcpy
python setup.py install (installs in /home/berceanu/anaconda3/envs/phcpy/lib/python3.6/site-packages/phcpy)
cd phcpy
python examples.py
```