project(
    'pymt_heatf',
    'c', 'cython', 'fortran',
    license: 'MIT',
)

py = import('python').find_installation(pure: false)
fc = meson.get_compiler('fortran')

python_inc = py.get_path('data') / 'include'
numpy_inc = run_command(
    py,
    [
        '-c',
        'import numpy; print(numpy.get_include())'
    ],
    check: true
).stdout().strip()
incs = include_directories(
    [
        meson.project_name() / 'lib',
        python_inc,
        numpy_inc,
    ]
)

# gfortran on Linux/macOS can find these libraries with fc.find_library(); flang 19 on Windows cannot.
bmif_dep = dependency('bmif', method: 'pkg-config')
heatf_dep = dependency('heatf', method: 'pkg-config')
bmiheatf_dep = dependency('bmiheatf', method: 'pkg-config')
deps = [
    bmif_dep,
    heatf_dep,
    bmiheatf_dep,
    py.dependency(),
]

srcs = [
    meson.project_name() / 'lib/bmi_interoperability.f90',
    meson.project_name() / 'lib/heatmodelf.pyx',
]

# Files get copied to <python directory>/site-packages/<subdir>
install_pkg_srcs = [
    meson.project_name() / '__init__.py',
    meson.project_name() / '_bmi.py',
]
py.install_sources(
    install_pkg_srcs,
    subdir: meson.project_name(),
)
install_lib_srcs = [
    meson.project_name() / 'lib/__init__.py',
    meson.project_name() / 'lib/heatmodelf.pyx',
]
py.install_sources(
    install_lib_srcs,
    subdir: meson.project_name() / 'lib',
)

install_subdir(
    'meta/HeatModelF',
    install_dir: py.get_install_dir() / meson.project_name() / 'data',
)

py.extension_module(
    'heatmodelf',
    srcs,
    dependencies: deps,
    include_directories: incs,
    install: true,
    subdir: meson.project_name() / 'lib',
)

# This is a temporary fix for editable installs.
run_command('cp', '-r', meson.project_name() / 'data', 'build', check: false)
