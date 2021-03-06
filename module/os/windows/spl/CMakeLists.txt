
use_clang()

file(GLOB CSOURCES CONFIGURE_DEPENDS "*.c")

list(REMOVE_ITEM CSOURCES "${CMAKE_CURRENT_SOURCE_DIR}/spl-wmsum.c")

set(TMH_FILE_LIST "")
tmh_generation("${CSOURCES}" TMH_FILE_LIST)
message(STATUS "SPLKERN:- ${TMH_FILE_LIST}")

wdk_add_library(splkern
  spl-atomic.c
  spl-condvar.c
  spl-cred.c
  spl-ddi.c
  spl-debug.c
  spl-err.c
  spl-kmem.c
  spl-kstat.c
  spl-list.c
  spl-md5.c
  spl-mount.c
  spl-mutex.c
  spl-policy.c
  spl-proc.c
  spl-processor.c
  spl-proc_list.c
  spl-rwlock.c
  spl-seg_kmem.c
  spl-taskq.c
  spl-thread.c
  spl-time.c
  spl-tsd.c
  spl-uio.c
  spl-vmem.c
  spl-vnode.c
  spl-windows.c
  spl-xdr.c
  spl-lookasidelist.c
  ${TMH_FILE_LIST}
)

# set(CMAKE_TOOLCHAIN_FILE $ENV{CMAKE_TOOLCHAIN_FILE})

target_include_directories(splkern BEFORE PUBLIC "${CMAKE_SOURCE_DIR}/include/os/windows/" PUBLIC "${CMAKE_SOURCE_DIR}/include/os/windows/spl")
