node-opencv
====

Installing on a Mac ([like this](http://ghost-jasontest0325381.rhcloud.com/getting-node-opencv-to-work-on-my-mac/) except without any editing):

- `brew tap homebrew/science`
- `brew install opencv`

Unforunately, you get this at runtime:

```OpenCV Error: Bad flag (parameter or structure field) (Unrecognized or unsupported array type) in cvGetMat, file /tmp/opencv-20170224-53144-14ui611/opencv-2.4.13.2/modules/core/src/array.cpp, line 2482```

- Wait, that's just because there was no file at the path given to OpenCV. Brutal. Works if the file path is valid.

Python opencv 3 setup
===

- Install with `brew install opencv@3`.
- [Upgrade pip so it can install stuff](https://stackoverflow.com/questions/49748063/pip-install-fails-for-every-package-could-not-find-a-version-that-satisfies)
- `echo /usr/local/opt/opencv@3/lib/python2.7/site-packages >> venv/lib/python2.7/site-packages/opencv3.pth` to [make OpenCV available to virtualenv](https://gravityjack.com/news/opencv-python-3-homebrew/).
