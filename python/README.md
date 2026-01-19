To compile ImarisReader dlls, necessary for PyImarisReader : (access source here : https://github.com/imaris/ImarisReader/tree/main, examples here : https://github.com/imaris/ImarisReaderTest/blob/main/pythonReaderTest.py)

0. Open a terminal and clone this repository with `git clone https://github.com/imaris/ImarisReader`
1. Change directory to the root of the cloned folder with `cd ImarisReader`
2. Make a build directory with `mkdir build`
3. Make sure vcpkg is downloaded on the computer. It will be necessary to link the required C++ dependancies that ImarisReader is using. For that, move one folder up with `cd ..` and clone vcpkg with `git clone https://github.com/microsoft/vcpkg`
4. Move to the vcpkg cloned folder with `cd vcpkg`
5. Run the command `./boostrap-vcpkg.bat -disableMetrics` to install vcpkg.
6. Download the dependancies that ImarisReader needs with this command : `.\vcpkg install boost:x64-windows lz4:x64-windows zlib:x64-windows hdf5:x64-windows`
7. Run `.\vcpkg integrate install` (to auto integrate in other projects with the toolchain)
8. Now go back to the ImarisReader folder (one folder up then into ImarisReader) : `cd ../ImarisReader`
9. configure the ImarisReader with the vcpkg toolchain : (change the paths accordingly if you placed your vcpkg folder differentely, for example)

```bash
cmake -S "." -B ".\build" -DCMAKE_TOOLCHAIN_FILE="..\vcpkg\scripts\buildsystems\vcpkg.cmake" -DVCPKG_TARGET_TRIPLET=x64-windows
```

10. run the build with `cmake --build "<chosen_path>\ImarisReader\build" --config Release`
11. Then move or copy manually the .dll files that have been created in the `Release` folder, to the `.\python\pyImarisReader\bin` folder of the python `pyImarisReader` package.

The preconfigured ``pyproject.toml`` file should allow you to easily install the package with ``pip install .e <the_location_of_your_ImarisReader_folder>`` from your venv of preference.

You can find examples of PyImarisReader at this url : ``https://github.com/imaris/ImarisReaderTest/blob/main/pythonReaderTest.py``
