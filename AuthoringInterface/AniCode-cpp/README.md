# Building backend binaries for AniCode

Note that below steps are used on Ubuntu 18.04.1 LTS
- [Install OpenCV](https://docs.opencv.org/3.4.5/d7/d9f/tutorial_linux_install.html)
- [Install ZXing C++](https://github.com/glassechidna/zxing-cpp), remember to run `make` and `make install` after `cmake -G "Unix Makefiles" ..`
- `cmake -DTYPE=0 . && make` to build `segment`
- `cmake -DTYPE=1 . && make` to build `match`
- `cmake -DTYPE=2 . && make` to build `animate`
