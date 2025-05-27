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
