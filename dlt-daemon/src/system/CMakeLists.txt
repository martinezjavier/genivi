#######
# Dlt - Diagnostic Log and Trace
# @licence make begin@
#
# Copyright (C) 2011-2012, BMW AG - Alexander Wenzel <alexander.aw.wenzel@bmw.de>
# 
# Contributions are licensed to the GENIVI Alliance under one or more
# Contribution License Agreements.
# 
# This Source Code Form is subject to the terms of the
# Mozilla Public License, v. 2.0. If a  copy of the MPL was not distributed with
# this file, You can obtain one at http://mozilla.org/MPL/2.0/.
#
# @licence end@
########

if(WITH_SYSTEMD_WATCHDOG OR WITH_SYSTEMD)
    message( STATUS "Added ${systemd_SRCS} to dlt-system")
endif(WITH_SYSTEMD_WATCHDOG OR WITH_SYSTEMD)

set(dlt_system_SRCS dlt-system dlt-system-options dlt-system-process-handling 
	dlt-system-filetransfer dlt-system-logfile dlt-system-processes dlt-system-shell
	dlt-system-syslog dlt-system-watchdog)
add_executable(dlt-system ${dlt_system_SRCS} ${systemd_SRCS})
target_link_libraries(dlt-system dlt z)
set_target_properties(dlt-system PROPERTIES LINKER_LANGUAGE C)


install(TARGETS dlt-system
	RUNTIME DESTINATION bin
	COMPONENT base)

INSTALL(FILES 	${CMAKE_CURRENT_SOURCE_DIR}/dlt-system.conf
	DESTINATION /etc
	COMPONENT base)
