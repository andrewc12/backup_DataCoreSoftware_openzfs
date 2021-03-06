
use_clang()

file(GLOB CSOURCES CONFIGURE_DEPENDS "*.c")

list(REMOVE_ITEM CSOURCES "${CMAKE_CURRENT_SOURCE_DIR}/zfs_vnops_os.c"
 "${CMAKE_CURRENT_SOURCE_DIR}/zfs_vnops_windows.c"
 "${CMAKE_CURRENT_SOURCE_DIR}/zfs_vnops_windows_lib.c"
 "${CMAKE_CURRENT_SOURCE_DIR}/zfs_vnops_windows_mount.c"
 "${CMAKE_CURRENT_SOURCE_DIR}/zfs_windows_zvol.c"
 "${CMAKE_CURRENT_SOURCE_DIR}/zvol_os.c")

set(TMH_FILE_LIST "")
tmh_generation("${CSOURCES}" TMH_FILE_LIST)

message(STATUS "ZFSKERN_OS:- ${TMH_FILE_LIST}")

wdk_add_library(zfskern_os
  KMDF 1.9
abd_os.c
arc_os.c
qat.c
qat_compress.c
qat_crypt.c
spa_misc_os.c
vdev_disk.c
vdev_file.c
zfs_acl.c
zfs_racct.c 
zfs_ctldir.c
zfs_debug.c
zfs_dir.c
zfs_file_os.c
zfs_fuid_os.c
zfs_ioctl_os.c
zfs_kstat_windows.c
zfs_vfsops.c
zfs_vnops_os.c
zfs_vnops_windows.c
zfs_vnops_windows_lib.c
zfs_vnops_windows_mount.c
zfs_windows_zvol.c
zfs_windows_zvol_scsi.c
zfs_windows_zvol_wmi.c
zfs_znode.c
zio_crypt.c
zvol_os.c
${TMH_FILE_LIST}
)

target_link_libraries(zfskern_os PRIVATE splkern icpkern)
