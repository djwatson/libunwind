project(libunwind C ASM)
cmake_minimum_required(VERSION 2.8)

set(libsrc mi/init.c mi/flush_cache.c mi/mempool.c mi/strerror.c
  mi/backtrace.c mi/dyn-cancel.c mi/dyn-info-list.c mi/dyn-register.c
  mi/Ldyn-extract.c mi/Lfind_dynamic_proc_info.c
  mi/Lget_accessors.c
  mi/Lget_proc_info_by_ip.c
  mi/Lget_proc_name.c
  mi/Lput_dynamic_unwind_info.c
  mi/Ldestroy_addr_space.c
  mi/Lget_reg.c
  mi/Lset_reg.c
  mi/Lget_fpreg.c
  mi/Lset_fpreg.c
  mi/Lset_caching_policy.c
  mi/Lset_cache_size.c
  os-linux.c
  x86_64/is_fpreg.c
  x86_64/regname.c
  x86_64/setcontext.S
  x86_64/Lapply_reg_state.c
  x86_64/Lreg_states_iterate.c
  x86_64/Lcreate_addr_space.c
  x86_64/Lget_save_loc.c
  x86_64/Lglobal.c
  x86_64/Linit.c
  x86_64/Linit_local.c
  x86_64/Linit_remote.c
  x86_64/Lget_proc_info.c
  x86_64/Lregs.c
  x86_64/Lresume.c
  x86_64/Lstash_frame.c
  x86_64/Lstep.c
  x86_64/Ltrace.c
  x86_64/Los-linux.c
  x86_64/getcontext.S
  dwarf/global.c dwarf/Lexpr.c dwarf/Lfde.c dwarf/Lparser.c dwarf/Lpe.c
  dwarf/Lfind_proc_info-lsb.c dwarf/Lfind_unwind_table.c elf64.c
  )
include_directories(../include . ../include/tdep-x86_64)

add_library(unwind OBJECT ${libsrc})
set_property(TARGET unwind PROPERTY POSITION_INDEPENDENT_CODE 1)

add_library(unwind_shared SHARED $<TARGET_OBJECTS:unwind>)
add_library(unwind_static STATIC $<TARGET_OBJECTS:unwind>)

set(libx86_64
  dwarf/global.c dwarf/Lexpr.c dwarf/Lfde.c dwarf/Lparser.c dwarf/Lpe.c
  dwarf/Lfind_proc_info-lsb.c dwarf/Lfind_unwind_table.c elf64.c
  x86_64/is_fpreg.c x86_64/regname.c
  x86_64/Gapply_reg_state.c x86_64/Greg_states_iterate.c
  x86_64/Gcreate_addr_space.c x86_64/Gget_save_loc.c
  x86_64/Gglobal.c x86_64/Ginit.c x86_64/Ginit_local.c x86_64/Ginit_remote.c
  x86_64/Gget_proc_info.c x86_64/Gregs.c x86_64/Gresume.c
  x86_64/Gstash_frame.c x86_64/Gstep.c x86_64/Gtrace.c
  x86_64/Gos-linux.c
  os-linux.c
  )

add_library(unwind-x86_64 OBJECT ${libx86_64})
set_property(TARGET unwind-x86_64 PROPERTY POSITION_INDEPENDENT_CODE 1)

add_library(unwind-x86_64_shared SHARED $<TARGET_OBJECTS:unwind-x86_64>)
add_library(unwind-x86_64_static STATIC $<TARGET_OBJECTS:unwind-x86_64>)
