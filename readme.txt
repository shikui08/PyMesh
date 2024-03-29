######NEED gcc 10
#NEED up-to-date pybind11 if python>=3.11
------------
git submodule sync --recursive
cd <submodule_dir> 

git fetch
git checkout origin/master
git branch master -f
git checkout master
------------


sudo update-alternatives --install /usr/bin/cc cc /usr/bin/gcc-10 10
sudo update-alternatives --install /usr/bin/c++ c++ /usr/bin/g++-10 20

export CFLAGS="-fPIC -fcommon"
export CXXFLAGS="-fPIC -fcommon"
export LDFLAGS="-fPIC -fcommon"
export NUM_CORES=32 

ls */CMakeCache.txt */**/**/CMakeCache.txt | xargs -i rm {}

conda activate <.../venv_3.11>
VERBOSE=1 CXX=g++-10 CC=gcc-10 python3 setup.py build