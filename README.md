# Создаем переменную GITHUB_USERNAME и GITHUB_EMAIL с нашими значениями
![1](https://github.com/user-attachments/assets/ec61ed75-01cb-4805-b0cf-494b6a37c557)

# Создаем псевдоним для nano
![2](https://github.com/user-attachments/assets/73f36125-0c38-4d2a-8d56-dbaf84afed5a)

# Перемещаемся в нашу рабочую папку и закидываем ее в стек
![3](https://github.com/user-attachments/assets/49c9379e-6608-44cc-9085-5c5d42609550)
![3-1](https://github.com/user-attachments/assets/50212e7d-f280-470e-ab74-f66e16526eb1)

# Копирование файлов в папку с прошлой Л/р
![4](https://github.com/user-attachments/assets/1d9d25b3-1f62-49b3-86b1-bf2956b6cf5f)

# Отключение от прошлой работы и подключение к директории с 6 лаборатоной для работы
![5](https://github.com/user-attachments/assets/b1744ead-6b8e-4c96-8999-5e38b2b18b52)

```sh
# дописывание в указанный файл указанных команд
$ gsed -i '/project(print)/a\
set(PRINT_VERSION_STRING "v\${PRINT_VERSION}")
' CMakeLists.txt
$ gsed -i '/project(print)/a\
set(PRINT_VERSION\
  \${PRINT_VERSION_MAJOR}.\${PRINT_VERSION_MINOR}.\${PRINT_VERSION_PATCH}.\${PRINT_VERSION_TWEAK})
' CMakeLists.txt
$ gsed -i '/project(print)/a\
set(PRINT_VERSION_TWEAK 0)
' CMakeLists.txt
$ gsed -i '/project(print)/a\
set(PRINT_VERSION_PATCH 0)
' CMakeLists.txt
$ gsed -i '/project(print)/a\
set(PRINT_VERSION_MINOR 1)
' CMakeLists.txt
$ gsed -i '/project(print)/a\
set(PRINT_VERSION_MAJOR 0)
' CMakeLists.txt
```

# Просмотр изменений в локальной директории
![6](https://github.com/user-attachments/assets/120668be-bf90-4f4a-973c-655fc8d89c80)

# Создание и редактирование DESCRIPTION
![7](https://github.com/user-attachments/assets/8ca9ddca-e31e-4111-a6ee-894e255e0088)

# Создание changelog
![8](https://github.com/user-attachments/assets/fe2c2813-4daa-4f24-8402-91df2472598a)

# Создание переменной DATE
![9](https://github.com/user-attachments/assets/5b215f09-6056-488f-b423-241c692c846a)

# Добавление данных в Changelog
![10](https://github.com/user-attachments/assets/2e30d35a-e51d-4548-a6b8-4b459223b618)

```sh
# создание отдельного CMake файла с конфигурацией
# запись в указанный файл строки
$ cat > CPackConfig.cmake <<EOF
include(InstallRequiredSystemLibraries)
EOF

# дописывание в файл конфигурации переменных
$ cat >> CPackConfig.cmake <<EOF
set(CPACK_PACKAGE_CONTACT ${GITHUB_EMAIL})
set(CPACK_PACKAGE_VERSION_MAJOR \${PRINT_VERSION_MAJOR})
set(CPACK_PACKAGE_VERSION_MINOR \${PRINT_VERSION_MINOR})
set(CPACK_PACKAGE_VERSION_PATCH \${PRINT_VERSION_PATCH})
set(CPACK_PACKAGE_VERSION_TWEAK \${PRINT_VERSION_TWEAK})
set(CPACK_PACKAGE_VERSION \${PRINT_VERSION})
set(CPACK_PACKAGE_DESCRIPTION_FILE \${CMAKE_CURRENT_SOURCE_DIR}/DESCRIPTION)
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "static C++ library for printing")
EOF

# дополнение конфигурации переменными с путями к файлам лицензии и README
$ cat >> CPackConfig.cmake <<EOF
set(CPACK_RESOURCE_FILE_LICENSE \${CMAKE_CURRENT_SOURCE_DIR}/LICENSE)
set(CPACK_RESOURCE_FILE_README \${CMAKE_CURRENT_SOURCE_DIR}/README.md)
EOF

# добавление в конфигурацию информации о RPM
$ cat >> CPackConfig.cmake <<EOF
set(CPACK_RPM_PACKAGE_NAME "print-devel")
set(CPACK_RPM_PACKAGE_LICENSE "MIT")
set(CPACK_RPM_PACKAGE_GROUP "print")
set(CPACK_RPM_CHANGELOG_FILE \${CMAKE_CURRENT_SOURCE_DIR}/ChangeLog.md)
set(CPACK_RPM_PACKAGE_RELEASE 1)
EOF

# добавление в конфигурацию информации о DEBIAN
$ cat >> CPackConfig.cmake <<EOF
set(CPACK_DEBIAN_PACKAGE_NAME "libprint-dev")
set(CPACK_DEBIAN_PACKAGE_PREDEPENDS "cmake >= 3.0")
set(CPACK_DEBIAN_PACKAGE_RELEASE 1)
EOF

# подключение CPack в CMake конфиг
$ cat >> CPackConfig.cmake <<EOF
include(CPack)
EOF

# подключение дополнительной конфигурации
$ cat >> CMakeLists.txt <<EOF

include(CPackConfig.cmake)
EOF
```

# Изменение README.md
![13!](https://github.com/user-attachments/assets/3038bd68-47a1-4b33-a50f-9cb860cade0b)

# Фиксируем и коммитим
![14](https://github.com/user-attachments/assets/a3daf5b2-8a58-459d-a692-89a4519f85f2)
![15](https://github.com/user-attachments/assets/299a08c3-7905-4cdf-8be0-7e53f6366545)
![16](https://github.com/user-attachments/assets/c2133ffe-8d81-41f7-aa8a-2fa2c0346b77)

# Авторизация в travis
![17](https://github.com/user-attachments/assets/62b8ceb3-fbed-421f-92ea-77a0b719f934)
![18](https://github.com/user-attachments/assets/211b0b49-307a-45ed-8f90-438df99f6cc8)

# Компилируем через CMake и создаем архим через CPack
![19](https://github.com/user-attachments/assets/6df56c0f-05a2-4990-a34d-780af079cf95)

# Сборка собранного файла
![21](https://github.com/user-attachments/assets/d5a73a87-c98b-40b8-9a8e-ab784460f5a6)
![20](https://github.com/user-attachments/assets/0901a4d3-15ab-46b8-ac5c-db91b12aa064)

# Перемещение собранного файла и проверка его наличия
![22](https://github.com/user-attachments/assets/31d87921-05a5-4e32-bb37-b0610cde661e)

## Homework

Текст файла `CPackConfig.cmake`:
```sh
$ cat > CPackConfig.cmake <<EOF
include(InstallRequiredSystemLibraries)
set(CPACK_PACKAGE_CONTACT ${GITHUB_EMAIL})
set(CPACK_PACKAGE_VERSION_MAJOR \${SOLVER_VERSION_MAJOR})
set(CPACK_PACKAGE_VERSION_MINOR \${SOLVER_VERSION_MINOR})
set(CPACK_PACKAGE_VERSION_PATCH \${SOLVER_VERSION_PATCH})
set(CPACK_PACKAGE_VERSION_TWEAK \${SOLVER_VERSION_TWEAK})
set(CPACK_PACKAGE_VERSION \${SOLVER_VERSION})
set(CPACK_PACKAGE_DESCRIPTION_FILE \${CMAKE_CURRENT_SOURCE_DIR}/DESCRIPTION)
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "solver app")

set(CPACK_RPM_PACKAGE_NAME "solver")
set(CPACK_RPM_PACKAGE_LICENSE "MIT")
set(CPACK_RPM_PACKAGE_GROUP "solver")
set(CPACK_RPM_CHANGELOG_FILE \${CMAKE_CURRENT_SOURCE_DIR}/CHANGELOG.md)
set(CPACK_RPM_PACKAGE_RELEASE 1)

set(CPACK_SOURCE_PACKAGE_FILE_NAME "solver-\${SOLVER_VERSION}")
set(CPACK_SOURCE_GENERATOR "TGZ;ZIP")

set(CPACK_DEBIAN_PACKAGE_NAME "solver")
set(CPACK_DEBIAN_PACKAGE_DEPENDS "cmake >= 3.0")
set(CPACK_DEBIAN_PACKAGE_RELEASE 1)

if (CMAKE_INSTALL_PREFIX)
    set(CPACK_OUTPUT_FILE_PREFIX \${CMAKE_INSTALL_PREFIX}/packages)
else()
    set(CPACK_OUTPUT_FILE_PREFIX \${CMAKE_BINARY_DIR}/packages)
endif(CMAKE_INSTALL_PREFIX)

include(CPack)
EOF
```
CMakeLists.txt в корне репозитория:
```sh
$ cat CMakeLists.txt
cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDART 11)
set(CMAKE_CXX_STANDART_REQUIRED ON)

project(solver)

set(SOLVER_VERSION_MAJOR 0)
set(SOLVER_VERSION_MINOR 1)
set(SOLVER_VERSION_PATCH 0)
set(SOLVER_VERSION_TWEAK 0)
set(SOLVER_VERSION
    ${SOLVER_VERSION_MAJOR}.${SOLVER_VERSION_MINOR}.${SOLVER_VERSION_PATCH}.${SOLVER_VERSION_TWEAK})
set(SOLVER_VERSION_STRING "v${SOLVER_VERSION}")

option(INSTALL_FORMATTER "Install libformatter" OFF)
option(INSTALL_FORMATTER_EX "Install libformatter_ex" OFF)
option(INSTALL_HELLOWORLD "Install hello_world" OFF)
option(INSTALL_LIBSOLVER "Install libsolver" OFF)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/hello_world_application)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/solver_application)

include(CPackConfig.cmake)
```

CMakeLists.txt в директории solver_application/   :
```sh
$ cat solver_application/CMakeLists.txt
cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDART 11)
set(CMAKE_CXX_STANDART_REQUIRED ON)

include(${CMAKE_CURRENT_LIST_DIR}/../formatter_ex_lib/CMakeLists.txt)

# specify rule for solver_lib

add_library(libsolver STATIC ${CMAKE_CURRENT_LIST_DIR}/../solver_lib/solver.cpp)

include_directories(${CMAKE_CURRENT_LIST_DIR}/../solver_lib)


add_executable(solver ${CMAKE_CURRENT_LIST_DIR}/equation.cpp)

target_link_libraries(solver formatter_ex libsolver)

if(INSTALL_LIBSOLVER)
    install(TARGETS libsolver 
        RUNTIME DESTINATION bin
        ARCHIVE DESTINATION lib
        LIBRARY DESTINATION lib
    )
endif(INSTALL_LIBSOLVER)

if (WIN32)
    install(TARGETS solver
        RUNTIME DESTINATION Release
    )
else()
    install(TARGETS solver 
        RUNTIME DESTINATION bin
    )
endif()
```

Текст файла travis.yml
```sh
os:
    - linux
    - osx

language: cpp
compiler:
    - clang
    - gcc

git:
    depth: 1

tags: true

sudo: true

addons:
    apt:
        - cmake
        - cmake-data
        - rpm

script:
    - cmake -H. -Bbuild -DCMAKE_INSTALL_PREFIX=install
    - cmake --build build/
    - cd build/
    - cpack --config CPackSourceConfig.cmake
    - if [ "${TRAVIS_OS_NAME}" = "osx" ]; then cpack -G DragNDrop; fi
    - if [ "${TRAVIS_OS_NAME}" = "linux" ]; then cpack -G RPM; cpack -G DEB; fi
    - cd ..

deploy:
    provider: releases
    api_key: ####################################
    file_glob: true
    file:
        - "install/packages/*.deb"
        - "install/packages/*.rpm"
        - "install/packages/*.dmg"
        - "install/packages/*.tar.gz"
        - "install/packages/*.zip"
    skip_cleanup: true
    on:
        tags: true
```

Измененный .appveyor.yml:
```sh
image: Visual Studio 2022

platform:
    - x86
    - x64

configuration: Release
build:
    parallel: true

build_script:
    - cmake -H. -Bbuild -DCMAKE_INSTALL_PREFIX=install
    - cmake --build build
    - cmake --build build --target install
    - cmake -H. -Bbuild -DCPACK_GENERATOR=WIX 
    - cmake --build build --target package

artifacts:
    - path: install\packages\*.msi
      name: solver

deploy:
    description: 'Some minor fixes'
    provider: GitHub
    auth_token:
        secure: ################################
    draft: false
    prerelease: false
    on:
        APPVEYOR_REPO_TAG: true
```

