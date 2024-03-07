set(esp_idf_common "../../../../Documents/git/reusables/golioth-firmware-sdk/examples/esp_idf/common")
set(examples_common "../../../../Documents/git/reusables/golioth-firmware-sdk/examples/common")

set(includes
    "${esp_idf_common}"
    "${examples_common}"
    "."
)

set(srcs
    "wifi_enterprise_main.c"
    "${esp_idf_common}/shell.c"
    "${esp_idf_common}/wifi.c"
    "${esp_idf_common}/nvs.c"
    "${examples_common}/golioth_basics.c"
)

set(deps
    "golioth_sdk"
    "console"
    "spi_flash"
    "nvs_flash"
    "json"
    "driver"
    "esp_hw_support"
    "wpa_supplicant"
    "esp_wifi"
)

idf_component_register(
    INCLUDE_DIRS "${includes}"
    SRCS "${srcs}"
    PRIV_REQUIRES "${deps}"
    EMBED_TXTFILES ca.pem client.crt client.key
)

list(APPEND EXTRA_C_FLAGS_LIST
    -Werror
)

component_compile_options(${EXTRA_C_FLAGS_LIST})