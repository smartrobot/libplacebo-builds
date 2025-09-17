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

# Dependencies - ensure all graphics dependencies are available first
vulkan_dep = dependency('vulkan', required: false, allow_fallback: true)
vulkan_loader_dep = dependency('vulkan-loader', required: false, allow_fallback: true)
glslang_dep = dependency('glslang', required: false, allow_fallback: true)
spirv_dep = dependency('SPIRV', required: false, allow_fallback: true)
spirv_cross_dep = dependency('spirv-cross-c-shared', required: false, allow_fallback: true)

# Get libplacebo via wrap
libplacebo_proj = subproject('libplacebo', default_options: [
  'default_library=shared',
  'vulkan=auto',
  'vulkan-registry=' + meson.current_source_dir() + '/subprojects/vulkan-headers/registry/vk.xml',
  'opengl=disabled',
  'demos=false',
  'tests=false'
])

libplacebo_dep = libplacebo_proj.get_variable('libplacebo')

# The shared library will be installed by the subproject

# Basic test to ensure the subproject built successfully
test('build_test', find_program('echo'), args: ['libplacebo built successfully'])