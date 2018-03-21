project('xxHash', 'c', version: '0.6.4', license: ['GPL', 'BSD'])

SHELL = find_program('sh')
HAVE_SSE4 = run_command(SHELL, '$(CC) -dM -E - < /dev/null | grep "SSE4" > /dev/null && echo 1 || echo 0')

if HAVE_SSE4 == '0'
	add_global_arguments('-mno-sse4', language: 'c')
endif

add_global_arguments('-Wall', language: 'c')
add_global_arguments('-Wextra', language: 'c')
add_global_arguments('-Wcast-qual', language: 'c')
add_global_arguments('-Wcast-align', language: 'c')
add_global_arguments('-Wshadow', language: 'c')
add_global_arguments('-Wstrict-aliasing=1', language: 'c')
add_global_arguments('-Wswitch-enum', language: 'c')
add_global_arguments('-Wdeclaration-after-statement', language: 'c')
add_global_arguments('-Wstrict-prototypes', language: 'c')
add_global_arguments('-Wundef', language: 'c')

inc_xxhash = include_directories('.')
lib_xxhash = static_library('xxhash', 'xxhash.c')
dll_xxhash = shared_library('xxhash', 'xxhash.c')
exe_xxhsum = executable('xxhsum', 'xxhsum.c', link_with: lib_xxhash)
dep_xxhsum = declare_dependency(include_directories: inc_xxhash, link_with: lib_xxhash)

#
# TODO: Rename tests accordingly
#
test('xxhsum internal bench', exe_xxhsum, workdir: meson.source_root(), args: ['-bi1'])
test('xxhsum file bench', exe_xxhsum, workdir: meson.source_root(), args: ['-bi1', 'xxhash.c'])

