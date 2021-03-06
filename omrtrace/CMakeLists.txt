###############################################################################
# Copyright (c) 2017, 2017 IBM Corp. and others
#
# This program and the accompanying materials are made available under
# the terms of the Eclipse Public License 2.0 which accompanies this
# distribution and is available at https://www.eclipse.org/legal/epl-2.0/
# or the Apache License, Version 2.0 which accompanies this distribution and
# is available at https://www.apache.org/licenses/LICENSE-2.0.
#
# This Source Code may also be made available under the following
# Secondary Licenses when the conditions for such availability set
# forth in the Eclipse Public License, v. 2.0 are satisfied: GNU
# General Public License, version 2 with the GNU Classpath
# Exception [1] and GNU General Public License, version 2 with the
# OpenJDK Assembly Exception [2].
#
# [1] https://www.gnu.org/software/classpath/license.html
# [2] http://openjdk.java.net/legal/assembly-exception.html
#
# SPDX-License-Identifier: EPL-2.0 OR Apache-2.0
###############################################################################

add_library(omrtrace STATIC
	omrtraceapi.cpp
	omrtracecomponent.cpp
	omrtraceformatter.cpp
	omrtracelog.cpp
	omrtracemain.cpp
	omrtracemisc.cpp
	omrtraceoptions.cpp
	omrtracepublish.cpp
	omrtracewrappers.cpp
)

if(OMR_WARNINGS_AS_ERRORS)
	target_compile_options(omrtrace PRIVATE ${OMR_WARNING_AS_ERROR_FLAG})
endif()

if(OMR_ENHANCED_WARNINGS)
	target_compile_options(omrtrace PRIVATE ${OMR_ENHANCED_WARNING_FLAG})
endif()

target_link_libraries(omrtrace
	PUBLIC
	${OMR_THREAD_LIB}
	omrutil
)
#TODO: check if following makefile fragment still required:
#ifeq (gcc,$(OMR_TOOLCHAIN))
## disable builtin strncpy buffer length check for optimized builds (_FORTIFY_SOURCE=1 requires -O3)
	#ifeq ($(OMR_OPTIMIZE),1)
		#MODULE_CXXFLAGS+=-U_FORTIFY_SOURCE -D_FORTIFY_SOURCE=1
	#endif
#endif
