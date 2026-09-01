project(
    'vsgi',
    'vala',
    'c',
    version: '0.5.0-dev',
    license: 'LGPL',
    meson_version: '>=1.10.0',
)

version_split = meson.project_version().split('.')
MAJOR_VERSION = version_split[0].to_int()
MINOR_VERSION = version_split[1].to_int()

if version_split.length() > 2
    if '-' in version_split[2]
        initial_micro = version_split[2].split('-')
        MICRO_VERSION = initial_micro[0].to_int()
        VERSION_SUFFIX = initial_micro[1]
    else
        MICRO_VERSION = version_split[2].to_int()
        VERSION_SUFFIX = ''
    endif
else
    MICRO_VERSION = 0
    VERSION_SUFFIX = ''
endif
api_version = f'@MAJOR_VERSION@.@MINOR_VERSION@'

add_project_arguments(
    [
        '--enable-experimental',
        '--enable-deprecated',
        '--vapidir',
        join_paths(meson.current_source_dir(), 'vapi'),
        '--metadatadir',
        join_paths(meson.current_build_dir(), 'src'),
    ],
    language: 'vala',
)
glib_version = '2.80'
glib = dependency('glib-2.0', version: '>=@0@'.format(glib_version))
gobject = dependency('gobject-2.0', version: '>=@0@'.format(glib_version))
gio = dependency('gio-2.0', version: '>=@0@'.format(glib_version))
gio_unix = dependency('gio-unix-2.0', version: '>=@0@'.format(glib_version))
gmodule = dependency('gmodule-2.0', version: '>=@0@'.format(glib_version))
soup = dependency('libsoup-3.0', version: '>=3.6.6')
openssl = dependency('openssl')
posix = meson.get_compiler('vala').find_library('posix')

if meson.get_compiler('c').has_function('memmem')
    add_project_arguments('--define=HAVE_MEMMEM', language: 'vala')
endif

subdir('src')
subdir('bin')
if get_option('enable_tests')
    subdir('tests')
endif
