set(CAN_SOURCES
    mcp2515.c
    mcp2515_buffer.c
    mcp2515_get_message.c
    mcp2515_send_message.c
    mcp2515_set_dyn_filter.c
    mcp2515_get_dyn_filter.c
    mcp2515_static_filter.c
    mcp2515_write_id.c
    mcp2515_read_id.c
    mcp2515_error_register.c
    mcp2515_regdump.c
    mcp2515_set_mode.c
    mcp2515_sleep.c
    spi.c

    at90can.c
    at90can_buffer.c
    at90can_disable_dyn_filter.c
    at90can_set_dyn_filter.c
    at90can_get_dyn_filter.c
    at90can_send_message.c
    at90can_send_buf_message.c
    at90can_get_message.c
    at90can_get_buf_message.c
    at90can_error_register.c
    at90can_set_mode.c

    sja1000.c
    sja1000_buffer.c
    sja1000_send_message.c
    sja1000_get_message.c
    sja1000_error_register.c

    can_buffer.c
)

foreach(f ${CAN_SOURCES})
    list(APPEND CAN_SOURCE_PATHS "src/${f}")
endforeach()

add_avr_library(can
    ${CAN_SOURCE_PATHS}
)
avr_target_compile_definitions(can
    PUBLIC
        HAS_CAN_CONFIG_H=1
)
avr_target_include_directories(can
    PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR} # can.h
        # The client has to add the directory which contains the can_config.h
)

# The original Makefile adds the following compiler flags:
# -funsigned-char
# -funsigned-bitfields
# -fpack-struct
# -fshort-enums
# -Wall
# -Wstrict-prototypes
