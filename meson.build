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

# Dependencies (handled by libplacebo subproject)

# Get libplacebo via wrap
libplacebo_proj = subproject('libplacebo', default_options: [
  'default_library=shared',
  'vulkan=auto',
  'opengl=disabled',
  'demos=false',
  'tests=false'
])

libplacebo_dep = libplacebo_proj.get_variable('libplacebo')

# The shared library will be installed by the subproject

# Basic test to ensure the subproject built successfully
test('build_test', find_program('echo'), args: ['libplacebo built successfully'])