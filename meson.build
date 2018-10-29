project('AtkD', 'd',
    license: 'LGPL-3.0',
    version: '2.0.0'
)

project_soversion = 0

pkg_conf = import('pkgconfig')

source_root = meson.current_source_dir()
build_root = meson.current_build_dir()
gen_dir = 'generated'

#
# Dependencies
#
atk_dep   = dependency('atk')
glibd_dep = dependency('glibd-2.0')

#
# Build interfaces from GIR
#
gir_to_d_prog = find_program('girtod')
gir_wrap_dir = join_paths(source_root, 'src')
gir_d_intf_dir = join_paths(build_root, gen_dir)

message('Generating D interfaces from GIR...')
girtod_gen = run_command(gir_to_d_prog,
                         '-i', gir_wrap_dir,
                         '-o', gir_d_intf_dir,
                         '--print-files', 'relative,' + source_root)
if girtod_gen.returncode() != 0
    error('Unable to build D intefaces from GIR:\n' + girtod_gen.stderr())
endif

gir_bind_dir = include_directories(gen_dir)
# Enlist D GIR interface sources
gir_binding_sources = girtod_gen.stdout().strip().split('\n')

atkd = library('atkd-2.0',
    [gir_binding_sources],
    include_directories: [gir_bind_dir],
    dependencies: [atk_dep, glibd_dep],
    install: true,
    soversion: project_soversion,
    version: meson.project_version())

install_subdir(join_paths(build_root, gen_dir, 'atk'), install_dir: 'include/d/atkd-2/')

pkg_conf.generate(atkd,
    name: 'atkd-2.0',
    subdirs: 'd/atkd-2',
    version: meson.project_version(),
    requires: [atk_dep, glibd_dep],
    description: 'D bindings for the Atk Accessibility Toolkit.')

# for use by others which embed this as subproject
atkd_dep = declare_dependency(
    link_with: [atkd],
    include_directories: [gir_bind_dir]
)
