#
# Copyright (c) 2023 Nordic Semiconductor
#
# SPDX-License-Identifier: LicenseRef-Nordic-5-Clause
#

zephyr_library()
zephyr_library_include_directories(${APP_ROOT}/lib/bsec/src/inc)
zephyr_library_include_directories(${APP_ROOT}/lib/bme68x/src/bme68x)
zephyr_library_sources(${APP_ROOT}/lib/bme68x/src/bme68x/bme68x.c)

zephyr_library_compile_definitions(
  BSEC_SAMPLE_RATE=BSEC_SAMPLE_RATE_LP
  # BSEC_SAMPLE_RATE_IAQ=BSEC_SAMPLE_RATE_ULP
  BSEC_SAMPLE_RATE_IAQ=BSEC_SAMPLE_RATE_LP
  BSEC_SAMPLE_PERIOD_S=3
)

if (CONFIG_FP_HARDABI)
  if (CONFIG_CPU_CORTEX_M4)
    zephyr_library_import(bsec_lib ${APP_ROOT}/lib/bsec/src/cortex-m4/fpv4-sp-d16-hard/libalgobsec.a)
  else()
    assert(0 "Unsupported configuration.")
  endif()
else()
  zephyr_library_compile_definitions(BME68X_DO_NOT_USE_FPU)
  if (CONFIG_CPU_CORTEX_M4)
    zephyr_library_import(bsec_lib ${APP_ROOT}/lib/bsec/src/cortex-m4/libalgobsec.a)
  else()
    assert(0 "Unsupported configuration.")
  endif()
endif()

zephyr_library_sources(bme68x_iaq.c)
