if get_option('pipewire')
	user_hint = 'If you rather not build this, set "pipewire=false".'

	if not get_option('backend-drm')
		error('Attempting to build the pipewire plugin without the required DRM backend. ' + user_hint)
	endif

	deps_pipewire = [ dep_libweston_private ]

	dep_libpipewire = dependency('libpipewire-0.3', required: false)
	if not dep_libpipewire.found()
		dep_libpipewire = dependency('libpipewire-0.2', required: false)
	endif
	if not dep_libpipewire.found()
		error('Pipewire plugin requires libpipewire which was not found. ' + user_hint)
	endif
	deps_pipewire += dep_libpipewire

	dep_libspa = dependency('libspa-0.2', required: false)
	if not dep_libspa.found()
		dep_libspa = dependency('libspa-0.1', required: false)
	endif
	if not dep_libspa.found()
		error('Pipewire plugin requires libspa which was not found. ' + user_hint)
	endif
	deps_pipewire += dep_libspa

	plugin_pipewire = shared_library(
		'pipewire-plugin',
		'pipewire-plugin.c',
		include_directories: common_inc,
		dependencies: deps_pipewire,
		name_prefix: '',
		install: true,
		install_dir: dir_module_libweston
	)
	env_modmap += 'pipewire-plugin.so=@0@;'.format(plugin_pipewire.full_path())
	install_headers('pipewire-plugin.h', subdir: dir_include_libweston_install)
endif
