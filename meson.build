project('libplacebo-builds', 'c', 'cpp',
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
cpp = meson.get_compiler('cpp')

cmake = import('cmake')

# Build shaderc from source
opt_var = cmake.subproject_options()
opt_var.add_cmake_defines({
  'CMAKE_POSITION_INDEPENDENT_CODE': true,
  'CMAKE_C_FLAGS': '-fPIC',
  'CMAKE_CXX_FLAGS': '-fPIC',
  'SHADERC_SKIP_TESTS': true,
  'SHADERC_SKIP_EXAMPLES': true,
  'SHADERC_SKIP_COPYRIGHT_CHECK': true,
  'SPIRV_BUILD_TESTS': false,
  'SPIRV_TOOLS_BUILD_STATIC': true,
  'BUILD_SHARED_LIBS': false
})
shaderc_sub_proj = cmake.subproject('shaderc', options: opt_var)

# Use the regular shaderc library instead of shaderc_combined
shaderc_main_dep = shaderc_sub_proj.dependency('shaderc')

# Create a proper dependency with version info for libplacebo
shaderc_dep_with_version = declare_dependency(
  dependencies: shaderc_main_dep,
  version: '2025.1'
)

# Override the shaderc dependency for libplacebo
meson.override_dependency('shaderc', shaderc_dep_with_version)

# Try to get SPIRV library from the CMake subproject
try_spirv = shaderc_sub_proj.dependency('SPIRV')
meson.override_dependency('SPIRV', try_spirv)

# Get libplacebo via wrap - it should now find shaderc
libplacebo_proj = subproject('libplacebo', default_options: [
  'default_library=shared',
  'vulkan=enabled',
  'opengl=disabled',
  'demos=false',
  'tests=false',
  'shaderc=enabled',
  'glslang=enabled'
])

libplacebo_dep = libplacebo_proj.get_variable('libplacebo')

# The shared library will be installed by the subproject

# No tests needed - build verification only
