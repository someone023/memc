project('memc', 'c',
  version : '0.1',
  default_options : ['warning_level=3', 'b_lto=true', 'b_sanitize=address', 'b_lundef=false', 'buildtype=relwithdebinfo'])

cc = meson.get_compiler('c')

# Compiler-specific flags for performance optimization
common_flags = cc.get_supported_arguments([
  '-march=native', # Optimize for the local machine
])
add_project_arguments(common_flags, language : 'c')

# Conditional configuration based on build type
if get_option('buildtype') == 'debug'
  debug_flags = cc.get_supported_arguments([
    '-Og', # Optimization that does not interfere with debugging
    '-fno-omit-frame-pointer', # Keep the frame pointer for stack traces
  ])
  add_project_arguments(debug_flags, language : 'c')
endif

# The link_args conditional setup for AddressSanitizer is handled via 'b_sanitize' option
exe = executable('memc', 'src/memc.c', install : true)

# Unit test
test('basic', exe)
