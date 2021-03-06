# $FreeBSD$

SRCDIR=	${.CURDIR:H}/drivers/gpu/drm/i915

.PATH:	${SRCDIR}

KMOD=	i915kms
SRCS=	\
	dvo_ch7017.c \
	dvo_ch7xxx.c \
	dvo_ivch.c \
	dvo_ns2501.c \
	dvo_sil164.c \
	dvo_tfp410.c \
	i915_cmd_parser.c \
	i915_debugfs.c \
	i915_drv.c \
	i915_gem.c \
	i915_gemfs.c \
	i915_gem_batch_pool.c \
	i915_gem_clflush.c \
	i915_gem_context.c \
	i915_gem_dmabuf.c \
	i915_gem_evict.c \
	i915_gem_execbuffer.c \
	i915_gem_fence_reg.c \
	i915_gem_gtt.c \
	i915_gem_internal.c \
	i915_gem_object.c \
	i915_gem_render_state.c \
	i915_gem_request.c \
	i915_gem_stolen.c \
	i915_gem_shrinker.c \
	i915_gem_tiling.c \
	i915_gem_timeline.c \
	i915_gem_userptr.c \
	i915_gpu_error.c \
	i915_memcpy.c \
	i915_oa_hsw.c \
	i915_params.c \
	i915_pci.c \
	i915_irq.c \
	i915_suspend.c \
	i915_sw_fence.c \
	i915_syncmap.c \
	i915_trace_points.c \
	i915_vgpu.c \
	i915_vma.c \
	intel_acpi.c \
	intel_atomic.c \
	intel_atomic_plane.c \
	intel_audio.c \
	intel_bios.c \
	intel_breadcrumbs.c \
	intel_cdclk.c \
	intel_color.c \
	intel_crt.c \
	intel_csr.c \
	intel_ddi.c \
	intel_device_info.c \
	intel_display.c \
	intel_dp.c \
	intel_dp_aux_backlight.c \
	intel_dp_link_training.c \
	intel_dp_mst.c \
	intel_dpio_phy.c \
	intel_dpll_mgr.c \
	intel_dsi.c \
	intel_dsi_dcs_backlight.c \
	intel_dsi_vbt.c \
	intel_dsi_pll.c \
	intel_dvo.c \
	intel_fbc.c \
	intel_engine_cs.c \
	intel_fbdev.c \
	intel_fifo_underrun.c \
	intel_freebsd.c \
	intel_frontbuffer.c \
	intel_guc.c \
	intel_guc_ct.c \
	intel_guc_fw.c \
	intel_guc_log.c \
	intel_guc_submission.c \
	intel_hangcheck.c \
	intel_hdmi.c \
	intel_hotplug.c \
	intel_huc.c \
	intel_i2c.c \
	intel_lrc.c \
	intel_lspcon.c \
	intel_lvds.c \
	intel_modes.c \
	intel_mocs.c \
	intel_opregion.c \
	intel_overlay.c \
	intel_panel.c \
	intel_pipe_crc.c \
	intel_pm.c \
	intel_psr.c \
	intel_renderstate_gen6.c \
	intel_renderstate_gen7.c \
	intel_renderstate_gen8.c \
	intel_renderstate_gen9.c \
	intel_ringbuffer.c \
	intel_runtime_pm.c \
	intel_sdvo.c \
	intel_sideband.c \
	intel_sprite.c \
	intel_tv.c \
	intel_uc.c \
	intel_uc_fw.c \
	intel_uncore.c


# i915_perf.c         # This one opens a can of worms. Hold off for now.
# intel_lpe_audio.c   # Need platform and irq_chip support

# In case we want to build gvt some day...
# GVT_DIR	= ${SRCDIR}/gvt
# SRCS	+= ${GVT_DIR}/aperture_gm.c
# SRCS	+= ${GVT_DIR}/cfg_space.c
# SRCS	+= ${GVT_DIR}/cmd_parser.c
# SRCS	+= ${GVT_DIR}/display.c
# SRCS	+= ${GVT_DIR}/edid.c
# SRCS	+= ${GVT_DIR}/execlist.c
# SRCS	+= ${GVT_DIR}/firmware.c
# SRCS	+= ${GVT_DIR}/gtt.c
# SRCS	+= ${GVT_DIR}/gvt.c
# SRCS	+= ${GVT_DIR}/handlers.c
# SRCS	+= ${GVT_DIR}/interrupt.c
# SRCS	+= ${GVT_DIR}/kvmgt.c
# SRCS	+= ${GVT_DIR}/mmio.c
# SRCS	+= ${GVT_DIR}/opregion.c
# SRCS	+= ${GVT_DIR}/render.c
# SRCS	+= ${GVT_DIR}/sched_policy.c
# SRCS	+= ${GVT_DIR}/scheduler.c
# SRCS	+= ${GVT_DIR}/trace_points.c
# SRCS	+= ${GVT_DIR}/vgpu.c

CLEANFILES+= ${KMOD}.ko.full ${KMOD}.ko.debug

CFLAGS+= -I${.CURDIR:H}/linuxkpi/gplv2/include
CFLAGS+= -I${SYSDIR}/compat/linuxkpi/common/include
CFLAGS+= -I${.CURDIR:H}/linuxkpi/dummy/include

CFLAGS+= -I${.CURDIR:H}/include
CFLAGS+= -I${.CURDIR:H}/include/drm
CFLAGS+= -I${.CURDIR:H}/include/uapi
CFLAGS+= -I${SRCDIR:H:H}

CFLAGS+= '-DKBUILD_MODNAME="${KMOD}"'
CFLAGS+= '-DLINUXKPI_PARAM_PREFIX=i915_'
CFLAGS+= -include ${SRCDIR:H}/drm_os_config.h

.if ${MACHINE_CPUARCH} == "amd64"
SRCS+= i915_ioc32.c
.endif

SRCS	+=			\
	opt_acpi.h		\
	opt_compat.h		\
	opt_drm.h		\
	opt_syscons.h		\
	acpi_if.h		\
	bus_if.h		\
	fb_if.h			\
	device_if.h		\
	pci_if.h		\
	vnode_if.h

.include <bsd.kmod.mk>

# Re-instate -Wno-cast-qual for all files
# Reason: More or less all files need it due to use of test_bit() macro
# error: cast from 'const unsigned long *' to 'volatile unsigned long *'
CWARNFLAGS += -Wno-pointer-arith -Wno-format -Wno-cast-qual

CWARNFLAGS.dvo_ch7017.c=	-Wno-cast-qual
CWARNFLAGS.dvo_ch7xxx.c=	-Wno-cast-qual
CWARNFLAGS.dvo_ivch.c=		-Wno-cast-qual
CWARNFLAGS.dvo_ns2501.c=	-Wno-cast-qual
CWARNFLAGS.dvo_sil164.c=	-Wno-cast-qual
CWARNFLAGS.dvo_tfp410.c=	-Wno-cast-qual

CWARNFLAGS.intel_audio.c=	-Wno-cast-qual
CWARNFLAGS.intel_bios.c=	-Wno-cast-qual
CWARNFLAGS.intel_color.c=	-Wno-missing-prototypes
CWARNFLAGS.intel_csr.c=		-Wno-cast-qual
CWARNFLAGS.intel_dp.c=		-Wno-enum-conversion -Wno-format -Wno-unused
CWARNFLAGS.intel_ddi.c=		-Wno-enum-conversion -Wno-compare-distinct-pointer-types -Wno-unused
CWARNFLAGS.intel_display.c=	-Wno-tautological-pointer-compare -Wno-enum-conversion -Wno-cast-qual -Wno-incompatible-pointer-types-discards-qualifiers
CWARNFLAGS.intel_dpll_mgr.c=	-Wno-compare-distinct-pointer-types -Wno-missing-prototypes
CWARNFLAGS.intel_dsi_panel_vbt.c= -Wno-cast-qual
CWARNFLAGS.intel_engine_cs.c= -Wno-cast-qual
CWARNFLAGS.intel_fbdev.c=	-Wno-initializer-overrides
CWARNFLAGS.intel_guc_ct.c=	-Wno-address-of-packed-member # probably false positive
CWARNFLAGS.intel_guc_submission.c= -Wno-cast-qual
CWARNFLAGS.intel_hdmi.c=	-Wno-enum-conversion
CWARNFLAGS.intel_hotplug.c=	-Wno-missing-prototypes
CWARNFLAGS.intel_lrc.c=		-Wno-cast-qual -Wno-unused-variable
CWARNFLAGS.intel_lvds.c=	-Wno-unused
CWARNFLAGS.intel_overlay.c=	-Wno-tautological-pointer-compare
CWARNFLAGS.intel_pm.c=		-Wno-cast-qual -Wno-incompatible-pointer-types-discards-qualifiers -Wno-unused-const-variable
CWARNFLAGS.intel_psr.c=		-Wno-cast-qual
CWARNFLAGS.intel_runtime_pm.c=		-Wno-cast-qual 
CWARNFLAGS.intel_sdvo.c=	-Wno-cast-qual -Wno-enum-conversion
CWARNFLAGS.intel_tv.c=		-Wno-unused

CWARNFLAGS.i915_cmd_parser.c= -Wno-cast-qual
CWARNFLAGS.i915_debugfs.c=	-Wno-unused-function -Wno-cast-qual -Wno-format -Wno-dangling-else
CWARNFLAGS.i915_drv.c=		-Wno-initializer-overrides -Wno-cast-qual -Wno-missing-prototypes
CWARNFLAGS.i915_gem.c=		-Wno-tautological-pointer-compare -Wno-pointer-arith -Wno-cast-qual -Wno-int-conversion
CWARNFLAGS.i915_gem_batch_pool.c= -Wno-cast-qual
CWARNFLAGS.i915_gem_context.c= -Wno-cast-qual
CWARNFLAGS.i915_gem_dmabuf.c= -Wno-cast-qual
CWARNFLAGS.i915_gem_evict.c= -Wno-cast-qual
CWARNFLAGS.i915_gem_execbuffer.c= -Wno-tautological-pointer-compare -Wno-tautological-constant-out-of-range-compare -Wno-pointer-arith -Wno-cast-qual
CWARNFLAGS.i915_gem_fence_reg.c= -Wno-cast-qual
CWARNFLAGS.i915_gem_gtt.c=	-Wno-tautological-pointer-compare -Wno-cast-qual
CWARNFLAGS.i915_gem_internal.c= -Wno-cast-qual
CWARNFLAGS.i915_gem_render_state.c= -Wno-cast-qual
CWARNFLAGS.i915_gem_request.c= -Wno-cast-qual
CWARNFLAGS.i915_gem_shrinker.c= -Wno-cast-qual
CWARNFLAGS.i915_gem_stolen.c= -Wno-cast-qual
CWARNFLAGS.i915_gem_tiling.c=	-Wno-tautological-pointer-compare -Wno-cast-qual
CWARNFLAGS.i915_gem_timeline.c= -Wno-cast-qual
CWARNFLAGS.i915_gem_userptr.c= -Wno-cast-qual
CWARNFLAGS.i915_gpu_error.c= -Wno-cast-qual -Wno-unused-function
CWARNFLAGS.i915_pci.c=		-Wno-initializer-overrides 
CWARNFLAGS.i915_sw_fence.c= -Wno-unused-function
