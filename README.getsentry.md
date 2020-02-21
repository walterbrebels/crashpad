# Sentry Modifications

- File attachments support for MacOS and Windows. Based on changes made in
  https://github.com/Youw/crashpad/, distributed with Apache 2.0 License.
- Add `throws` declaration to `memfd_create` for compatibility with different
  libc versions.
- Build System Changes Listed Below

# Build System Changes

In order to minimize external dependencies, and to better integrate with
`sentry-native`, this fork replaced usage of `depo_tools` with explicit
submodules, and added CMake files for building.

Both submodules and CMake files currently only support building on macOS and
Windows, and do only export the necessary libraries and executables to
integrate the crashpad client.

When updating this fork, make sure to keep the files in sync, as explained
below.

## Submodules

For macOS and Windows support, only `third_party/mini_chromium` and
`third_party/zlib` are needed.

The specific submodule commit hashes can be found in the `./DEPS` file.

## CMake Integration

To allow building crashpad with CMake, the following CMake files were created
by manually translating the `BUILD.gn` files in the same folders (and following
included files):

- `./CMakeLists.txt`
- `./client/CMakeLists.txt`
- `./compat/CMakeLists.txt`
- `./handler/CMakeLists.txt`
- `./minidump/CMakeLists.txt`
- `./snapshot/CMakeLists.txt`
- `./third_party/getopt/CMakeLists.txt`
- `./third_party/mini_chromium/CMakeLists.txt`
- `./third_party/lib/CMakeLists.txt`
- `./tools/CMakeLists.txt`
- `./util/CMakeLists.txt`

The important thing here is to keep the list of source files in sync when
updating.

# How To Update

- Bump the submodules to the commit hashes specified in `./DEPS`
- Go through the changes in `BUILD.gn` files, and apply them to the
  corresponding `CMakeLists.txt`. See the list above.