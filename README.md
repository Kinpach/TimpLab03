# Lab_03
export GITHUB_USERNAME=Kinpach
cd ${GITHUB_USERNAME}/workspace
source scripts/activate
git clone https://github.com/${GITHUB_USERNAME}/TimpLab02.git projects/TimpLab03
Клонирование в «projects/TimpLab03»...
remote: Enumerating objects: 50, done.
remote: Counting objects: 100% (50/50), done.
remote: Compressing objects: 100% (41/41), done.
remote: Total 50 (delta 16), reused 11 (delta 0), pack-reused 0 (from 0)
Получение объектов: 100% (50/50), 10.93 КиБ | 10.93 МиБ/с, готово.
Определение изменений: 100% (16/16), готово.
cd projects/TimpLab03
git remote remove origin
git remote add origin https://github.com/${GITHUB_USERNAME}/TimpLab03.git
g++ -std=c++11 -I./include -c sources/print.cpp
ls print.o
print.o
nm print.o | grep print
0000000000000000 T _Z5printRKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEERSo
000000000000002a T _Z5printRKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEERSt14basic_ofstreamIcS2_E
ar rvs print.a print.o
ar: создаётся print.a
a - print.o
file print.a
print.a: current ar archive
g++ -std=c++11 -I./include -c examples/example1.cpp
ls example1.o
example1.o
g++ example1.o print.a -o example1
./example1 && echo
hello
g++ -std=c++11 -I./include -c examples/example2.cpp
nm example2.o
0000000000000000 V DW.ref.__gxx_personality_v0
                 U __gxx_personality_v0
0000000000000000 T main
                 U __stack_chk_fail
                 U _Unwind_Resume
                 U _Z5printRKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEERSt14basic_ofstreamIcS2_E
                 U _ZNSt14basic_ofstreamIcSt11char_traitsIcEEC1EPKcSt13_Ios_Openmode
                 U _ZNSt14basic_ofstreamIcSt11char_traitsIcEED1Ev
0000000000000000 W _ZNSt15__new_allocatorIcED1Ev
0000000000000000 W _ZNSt15__new_allocatorIcED2Ev
0000000000000000 n _ZNSt15__new_allocatorIcED5Ev
                 U _ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEC1EPKcRKS3_
                 U _ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEED1Ev
                 U _ZSt21ios_base_library_initv
0000000000000000 r _ZStL19piecewise_construct
g++ example2.o print.a -o example2
./example2
cat log.txt && echo
hello
rm -rf example1.o example2.o print.o
rm -rf print.a
rm -rf example1 example2
rm -rf log.txt
cat > CMakeLists.txt <<EOF
cmake_minimum_required(VERSION 3.4)
project(print)
EOF
cat >> CMakeLists.txt <<EOF
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
EOF
cat >> CMakeLists.txt <<EOF
include_directories(\${CMAKE_CURRENT_SOURCE_DIR}/include)
EOF
cmake -H. -B_build
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- The C compiler identification is GNU 13.3.0
-- The CXX compiler identification is GNU 13.3.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done (0.6s)
-- Generating done (0.0s)
-- Build files have been written to: /home/Kinpach/workspace/projects/TimpLab03/_build
cmake --build _build
cat >> CMakeLists.txt <<EOF
add_executable(example1 \${CMAKE_CURRENT_SOURCE_DIR}/examples/example1.cpp)
add_executable(example2 \${CMAKE_CURRENT_SOURCE_DIR}/examples/example2.cpp)
EOF
cmake --build _build
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- Configuring done (0.0s)
-- Generating done (0.0s)
-- Build files have been written to: /home/Kinpach/workspace/projects/TimpLab03/_build
[ 25%] Building CXX object CMakeFiles/example1.dir/examples/example1.cpp.o
[ 50%] Linking CXX executable example1
/usr/bin/ld: CMakeFiles/example1.dir/examples/example1.cpp.o: в функции «main»:
example1.cpp:(.text+0x59): undefined reference to `print(std::__cxx11::basic_string<char, std::char_traits<char>, std::allocator<char> > const&, std::ostream&)'
collect2: error: ld returned 1 exit status
gmake[2]: *** [CMakeFiles/example1.dir/build.make:97: example1] Ошибка 1
gmake[1]: *** [CMakeFiles/Makefile2:85: CMakeFiles/example1.dir/all] Ошибка 2
gmake: *** [Makefile:91: all] Ошибка 2
cmake --build _build --target print
gmake: *** Нет правила для сборки цели «print».  Останов.
cat >> CMakeLists.txt <<EOF
target_link_libraries(example1 print)
target_link_libraries(example2 print)
EOF
cmake --build _build
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- Configuring done (0.0s)
-- Generating done (0.0s)
-- Build files have been written to: /home/Kinpach/workspace/projects/TimpLab03/_build
[ 25%] Linking CXX executable example1
/usr/bin/ld: невозможно найти -lprint: Нет такого файла или каталога
collect2: error: ld returned 1 exit status
gmake[2]: *** [CMakeFiles/example1.dir/build.make:97: example1] Ошибка 1
gmake[1]: *** [CMakeFiles/Makefile2:85: CMakeFiles/example1.dir/all] Ошибка 2
gmake: *** [Makefile:91: all] Ошибка 2
cmake --build _build --target print
gmake: *** Нет правила для сборки цели «print».  Останов.
rm -rf CMakeLists.txt
cat CMakeLists.txt && echo
cat: CMakeLists.txt: Нет такого файла или каталога
cat > CMakeLists.txt <<EOF
cmake_minimum_required(VERSION 3.4)
project(print)
EOF
rm -rf CMakeLists.txt
cat > CMakeLists.txt <<EOF
cmake_minimum_required(VERSION 3.4)
project(print)
EOF
cat >> CMakeLists.txt <<EOF
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
EOF
cat >> CMakeLists.txt <<EOF
add_library(print STATIC \${CMAKE_CURRENT_SOURCE_DIR}/sources/print.cpp)
EOF
cat >> CMakeLists.txt <<EOF
include_directories(\${CMAKE_CURRENT_SOURCE_DIR}/include)
EOF
cmake -H. -B_build
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- Configuring done (0.0s)
-- Generating done (0.0s)
-- Build files have been written to: /home/Kinpach/workspace/projects/TimpLab03/_build
cmake --build _build
[ 50%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[100%] Linking CXX static library libprint.a
[100%] Built target print
cat >> CMakeLists.txt <<EOF
add_executable(example1 \${CMAKE_CURRENT_SOURCE_DIR}/examples/example1.cpp)
add_executable(example2 \${CMAKE_CURRENT_SOURCE_DIR}/examples/example2.cpp)
EOF
cat >> CMakeLists.txt <<EOF
target_link_libraries(example1 print)
target_link_libraries(example2 print)
EOF
cmake --build _build
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- Configuring done (0.0s)
-- Generating done (0.0s)
-- Build files have been written to: /home/Kinpach/workspace/projects/TimpLab03/_build
[ 33%] Built target print
[ 50%] Linking CXX executable example1
[ 66%] Built target example1
[ 83%] Building CXX object CMakeFiles/example2.dir/examples/example2.cpp.o
[100%] Linking CXX executable example2
[100%] Built target example2
cmake --build _build --target print
[100%] Built target print
cmake --build _build --target example1
[ 50%] Built target print
[100%] Built target example1
cmake --build _build --target example2
[ 50%] Built target print
[100%] Built target example2
ls -la _build/libprint.a
-rw-rw-r-- 1 Kinpach Kinpach 2246 мар 11 02:03 _build/libprint.a
_build/example1 && echo
hello
_build/example2
cat log.txt && echo
hello
rm -rf log.txt
git clone https://github.com/tp-labs/TimpLab03 tmp
Клонирование в «tmp»...
remote: Enumerating objects: 91, done.
remote: Counting objects: 100% (30/30), done.
remote: Compressing objects: 100% (9/9), done.
remote: Total 91 (delta 23), reused 21 (delta 21), pack-reused 61 (from 1)
Получение объектов: 100% (91/91), 1.02 МиБ | 2.55 МиБ/с, готово.
Определение изменений: 100% (41/41), готово.
mv -f tmp/CMakeLists.txt .
rm -rf tmp
cat CMakeLists.txt
cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

option(BUILD_EXAMPLES "Build examples" OFF)

project(print)

add_library(print STATIC ${CMAKE_CURRENT_SOURCE_DIR}/sources/print.cpp)

target_include_directories(print PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include>
)

if(BUILD_EXAMPLES)
  file(GLOB EXAMPLE_SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/examples/*.cpp")
  foreach(EXAMPLE_SOURCE ${EXAMPLE_SOURCES})
    get_filename_component(EXAMPLE_NAME ${EXAMPLE_SOURCE} NAME_WE)
    add_executable(${EXAMPLE_NAME} ${EXAMPLE_SOURCE})
    target_link_libraries(${EXAMPLE_NAME} print)
    install(TARGETS ${EXAMPLE_NAME}
      RUNTIME DESTINATION bin
    )
  endforeach(EXAMPLE_SOURCE ${EXAMPLE_SOURCES})
endif()

install(TARGETS print
    EXPORT print-config
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
)

install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/include/ DESTINATION include)
install(EXPORT print-config DESTINATION cmake)
cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- Configuring done (0.0s)
-- Generating done (0.0s)
-- Build files have been written to: /home/Kinpach/workspace/projects/TimpLab03/_build
cmake --build _build --target install
[100%] Built target print
Install the project...
-- Install configuration: ""
-- Installing: /home/Kinpach/workspace/projects/TimpLab03/_install/lib/libprint.a
-- Installing: /home/Kinpach/workspace/projects/TimpLab03/_install/include
-- Installing: /home/Kinpach/workspace/projects/TimpLab03/_install/include/print.hpp
-- Installing: /home/Kinpach/workspace/projects/TimpLab03/_install/cmake/print-config.cmake
-- Installing: /home/Kinpach/workspace/projects/TimpLab03/_install/cmake/print-config-noconfig.cmake
tree _install
locales-launch: Data of ru_RU locale not found, generating, please wait...
_install
├── cmake
│   ├── print-config.cmake
│   └── print-config-noconfig.cmake
├── include
│   └── print.hpp
└── lib
    └── libprint.a

4 directories, 4 files
git add CMakeLists.txt
git commit -m"added CMakeLists.txt"
[master 7707dcf] added CMakeLists.txt
 1 file changed, 36 insertions(+)
 create mode 100644 CMakeLists.txt
git push origin master
Username for 'https://github.com': Kinpach
Password for 'https://Kinpach@github.com': 
Перечисление объектов: 53, готово.
Подсчет объектов: 100% (53/53), готово.
При сжатии изменений используется до 8 потоков
Сжатие объектов: 100% (28/28), готово.
Запись объектов: 100% (53/53), 11.55 КиБ | 11.55 МиБ/с, готово.
Всего 53 (изменений 18), повторно использовано 48 (изменений 16), повторно использовано пакетов 0
remote: Resolving deltas: 100% (18/18), done.
To https://github.com/Kinpach/TimpLab03.git
 * [new branch]      master -> master
