project('d2sqlite3', 'd',
    meson_version: '>=0.46',
    license: 'BSL-1.0',
    version: '0.16.2'
)

project_soversion    = '0'

src_dir = include_directories('source/')
pkgc = import('pkgconfig')

sqlite_dep = dependency('sqlite3')

d2sqlite3_src = [
    'source/d2sqlite3/database.d',
    'source/d2sqlite3/internal/memory.d',
    'source/d2sqlite3/internal/util.d',
    'source/d2sqlite3/package.d',
    'source/d2sqlite3/results.d',
    'source/d2sqlite3/sqlite3.d',
    'source/d2sqlite3/statement.d',
]
install_subdir('source/d2sqlite3/', install_dir: 'include/d/d2sqlite3/')

d2sqlite3_lib = library('d2sqlite3',
        [d2sqlite3_src],
        include_directories: [src_dir],
        dependencies: [sqlite_dep],
        install: true,
        version: meson.project_version(),
        soversion: project_soversion
)

pkgc.generate(name: 'd2sqlite3',
              libraries: d2sqlite3_lib,
              subdirs: 'd/d2sqlite3/',
              version: meson.project_version(),
              requires: ['sqlite3'],
              description: 'A small wrapper around SQLite for the D programming language.'
)

# for use by others which embed this as subproject
d2sqlite3_dep = declare_dependency(
    link_with: [d2sqlite3_lib],
    dependencies: [sqlite_dep],
    include_directories: [src_dir]
)
