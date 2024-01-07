

lv_drivers_src = [
	'display/GC9A01.c',
	'display/ILI9341.c',
	'display/R61581.c',
	'display/SHARP_MIP.c',
	'display/ST7565.c',
	'display/UC1610.c',
	'display/fbdev.c',
	'display/SSD1963.c',
	'gtkdrv/gtkdrv.c',
	'indev/AD_touch.c',
	'indev/xkb.c',
	'indev/evdev.c',
	'indev/FT5406EE8.c',
	'indev/XPT2046.c',
	'indev/libinput.c',
	'sdl/sdl.c',
	'sdl/sdl_gpu.c',
	'sdl/sdl_common.c',
	'wayland/smm.c',
	'wayland/wayland.c',
]

lv_drivers_headers = [
	'display/UC1610.h',
	'display/SSD1963.h',
	'display/ILI9341.h',
	'display/ST7565.h',
	'display/fbdev.h',
	'display/SHARP_MIP.h',
	'display/drm.h',
	'display/R61581.h',
	'display/GC9A01.h',
	'display/monitor.h',
	'gtkdrv/gtkdrv.h',
	'indev/XPT2046.h',
	'indev/evdev.h',
	'indev/AD_touch.h',
	'indev/libinput_drv.h',
	'indev/mouse.h',
	'indev/xkb.h',
	'indev/FT5406EE8.h',
	'indev/mousewheel.h',
	'indev/keyboard.h',
	'lv_drv_conf_template.h',
	'sdl/sdl_common.h',
	'sdl/sdl.h',
	'sdl/sdl_gpu.h',
	'sdl/sdl_common_internal.h',
	'wayland/smm.h',
	'wayland/wayland.h',
]

lv_drivers_deps = [
	lvgl,
]

if libdrm_dep.found()
  lv_drivers_deps += [libdrm_dep]
  lv_drivers_src += ['display/drm.c']
endif

lv_drivers_lib = static_library(
	'lv_drivers',
	lv_drivers_src,
	dependencies: lv_drivers_deps,
	c_args: [
		'-DLV_CONF_INCLUDE_SIMPLE=1',
		'-DLV_LVGL_H_INCLUDE_SIMPLE=1',
		'-I@0@'.format(HACK_unl0kr_dir),
	],
)

# This doesn't work as intended
install_headers(lv_drivers_headers, install_dir: 'lv_drivers', preserve_path: true)

lv_drivers = declare_dependency(
	link_with: lv_drivers_lib,
	# FIXME: awful horrific hack to make includes work
	# we should instead use a custom generator to "build" the headers
	# so that they can be included that way. This is BAD
	include_directories: [
		'..',
	],
)
