To compile ImarisReader dlls, necessary for PyImarisReader : (access source here : https://github.com/imaris/ImarisReader/tree/main, examples here : https://github.com/imaris/ImarisReaderTest/blob/main/pythonReaderTest.py)

1. CD to the root of the source folder
2. Make a build directory
3. Make sure vcpkg is downloaded on the computer (from : https://github.com/microsoft/vcpkg) (clone it with git)
4. cd to vcpkg cloned source folder
5. run ./boostrap-vcpkg.bat with flag -disableMetrics
6. install the dependancies that ImarisReader needs : .\vcpkg install boost:x64-windows lz4:x64-windows zlib:x64-windows hdf5:x64-windows
7. .\vcpkg integrate install (to auto integrate the toolchain in other projects)
8. Now go back to the ImarisReader folder with cd
9. configure the ImarisReader with the vcpkg toolchain :
   - cmake -S "<chosen_path>\ImarisReader"
     -B "<chosen_path>\ImarisReader\build"
     -DCMAKE_TOOLCHAIN_FILE="<chosen_path>\vcpkg\scripts\buildsystems\vcpkg.cmake"
     -DVCPKG_TARGET_TRIPLET=x64-windows
10. run the build with cmake --build "<chosen_path>\ImarisReader\build" --config Release

Then move or copy the dll files from release, to the python/pyImarisReader/bin folder of the python pyImarisReader package.

The pyproject toml should allow you to easily install the package with pip install .e <the_location_of_your_ImarisReader_folder>
