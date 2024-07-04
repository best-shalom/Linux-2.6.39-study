###
# scripts contains sources for various helper programs used throughout
# the kernel for the build process.
# ---------------------------------------------------------------------------
# kallsyms:      Find all symbols in vmlinux
# pnmttologo:    Convert pnm files to logo files
# conmakehash:   Create chartable
# conmakehash:	 Create arrays for initializing the kernel console tables
c_flags := $(filter-out -fPIC -fPIE, $(c_flags) -fno-pic)
a_flags := $(filter-out -fPIC -fPIE, $(a_flags) -fno-pic)

# Debug information
$(info c_flags=$(c_flags))
$(info a_flags=$(a_flags))


hostprogs-$(CONFIG_KALLSYMS)     += kallsyms
hostprogs-$(CONFIG_LOGO)         += pnmtologo
hostprogs-$(CONFIG_VT)           += conmakehash
hostprogs-$(CONFIG_IKCONFIG)     += bin2c
hostprogs-$(BUILD_C_RECORDMCOUNT) += recordmcount

always		:= $(hostprogs-y) $(hostprogs-m)

# The following hostprogs-y programs are only build on demand
hostprogs-y += unifdef

# This target is used internally to avoid "is up to date" messages
PHONY += build_unifdef
build_unifdef: scripts/unifdef FORCE
	@:

subdir-$(CONFIG_MODVERSIONS) += genksyms
subdir-y                     += mod
subdir-$(CONFIG_SECURITY_SELINUX) += selinux
subdir-$(CONFIG_DTC)         += dtc

# Let clean descend into subdirs
subdir-	+= basic kconfig package selinux
