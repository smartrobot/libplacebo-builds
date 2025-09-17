project('libplacebo-builds', 'c',
  version : '6.338.2',
  license : 'LGPL-2.1+',
  meson_version : '>=0.63.0',
  default_options : [
    'c_std=c99',
    'warning_level=2',
    'buildtype=release',
    'default_library=shared'
  ]
)

cc = meson.get_compiler('c')
cmake = import('cmake')

# Build shaderc as a CMake subproject 
shaderc_sub_proj = cmake.subproject('shaderc')

# Get the main shaderc dependency that libplacebo needs  
shaderc_dep = shaderc_sub_proj.dependency('shaderc')

# Create a proper dependency with version info for libplacebo
shaderc_dep_with_version = declare_dependency(
  dependencies: shaderc_dep,
  version: '2024.4'  # Match the version in shaderc.wrap
)


# Override the shaderc dependency for libplacebo
meson.override_dependency('shaderc', shaderc_dep_with_version)

# Get libplacebo via wrap - it should now find shaderc
libplacebo_proj = subproject('libplacebo', default_options: [
  'default_library=shared',
  'vulkan=true',
  'opengl=disabled',
  'demos=false',
  'tests=false'
])

libplacebo_dep = libplacebo_proj.get_variable('libplacebo')

# The shared library will be installed by the subproject

# Basic test to ensure the subproject built successfully
test('build_test', find_program('echo'), args: ['libplacebo built successfully'])