# TSC_EBook_Reader
# Proiect realizat de: DINU Andrei-Marian
# Pentru cursul: Teoria Sistemelor de Calcul, 2025

**OpenBook** este un e-reader open-source proiectat în jurul microcontrollerului ESP32-C6, echipat cu un display E-Ink de 7.5 inch, baterie Li-Po, card microSD și senzori de mediu.



## Mapping pini ESP32-C6

| Semnal        | ESP32 Pin | Funcție                      |
|---------------|-----------|------------------------------|
| EPD_BUSY      | IO3       | Status display               |
| EPD_RST       | IO23      | Reset display                |
| EPD_DC        | IO5       | Data/Command                 |
| EPD_CS        | IO10      | SPI CS pentru e-paper        |
| EPD_CLK       | IO6       | SPI Clock                    |
| EPD_MOSI      | IO7       | SPI Data Out                 |
| SS_SD         | IO4       | SD Card CS                   |
| SD_MISO       | IO2       | SPI MISO                     |
| I2C_SDA       | IO21      | RTC + BME688                 |
| I2C_SCL       | IO22      | RTC + BME688                 |
| RTC_RST       | IO18      | Reset DS3231                 |
| RTC_INT       | IO0       | Interrupt RTC                |
| 32KHz_CLK     | IO1       | Oscilator RTC                |
| IO/BOOT Btn   | IO9       | Boot                         |
| IO/CHANGE Btn | IO15      | Navigare                     |
| RESET         | EN        | Reset MCU                    |

## 🧱 Design Decizii & Trade-offs

- Am ales ESP32-C6 pentru capabilități Wi-Fi/BLE și suport FreeRTOS
- Folosirea unui e-paper reduce drastic consumul în stand-by
- Am optat pentru o singură interfață SPI partajată (e-paper + SD) cu CS separat
- Butoanele au fost puse pe pini liberi fără funcții speciale


## 🔎 Debug & Testare

- Verificat DRC (JLCPCB 2 layer .dru)
- Testat alimentarea cu Li-Po + încărcare
- Verificat interfațare SPI + I2C pe bus logic analyzer
- Verificat consum în deep sleep sub 200µA


|                 Componentă                |                                                     Link Datasheet                                                            |                                                          LINK                                                                           |
|-------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| USB Connector 112A-TAAR-R03               | [ESP32-C6-WROOM-1](https://www.attend.com.tw/data/download/file/112A-TAAR-R03_Spec.pdf)                                       | [Status display](https://www.digikey.com/en/products/detail/attend-technology/112A-TAAR-R03/17633923)                                   |
| Inductor 68uH (Würth)                     | [7.5" V2 e-Paper](https://www.we-online.com/components/products/datasheet/784373170680.pdf)                                   | [Reset display ](https://eu.mouser.com/ProductDetail/Wurth-Elektronik/784373170680?qs=sGAEpiMZZMv126LJFLh8yzGkpireax1GgDeN9GF1EUQ%3D)   |
| LED Bridgelux                             | [DS3231](https://www.bridgelux.com/sites/default/files/resource_media/DS51_Rev%20F%20Bridgelux%20SMD%203030%20Data%20sheet.pdf)  | [Data/Command](https://www.digikey.com/en/products/detail/bridgelux/BXEM-27E0000-0-000/6618599)                                      |
| Voltage Detector BD5229G                  | [BME688 ](https://fscdn.rohm.com/en/products/databook/datasheet/ic/power/voltage_detector/bd52xxg-e.pdf)                      | [SPI CS pentru e-paper        ](https://www.digikey.com/en/products/detail/rohm-semiconductor/BD5229G-TR/658502)                        |
| Butoane TL3315                            | [XC6221B331MR-G](https://fscdn.rohm.com/en/products/databook/datasheet/ic/power/voltage_detector/bd52xxg-e.pdf)               | [SPI Clock                    ](https://www.digikey.com/en/products/detail/rohm-semiconductor/BD5229G-TR/658502)                        |
| Supercapacitor 0.011F 3.3V                | [MCP73831T-2ACI/OT ](https://mm.digikey.com/Volume0/opasdata/d220001/medias/docus/6537/rev05-CPHCPM.pdf)                      | [SPI Data Out                ](https://www.digikey.com/en/products/detail/seiko-instruments/cph3225a/8692444)                           |
| RTC DS3231SN                              | [LP584174 (1800mAh) ](https://www.analog.com/media/en/technical-documentation/data-sheets/DS3231.pdf)                         | [SD Card CS ](https://www.digikey.com/en/products/detail/analog-devices-inc-maxim-integrated/DS3231SN/1197576)                          |
| Capacitor 0402YD104MAT2A                  | [FH34SRJ-24S-0.5SH(50)](https://eu.mouser.com/datasheet/2/40/cx5r_KGM-3223198.pdf)                                            | [SPI MISO                  ](https://eu.mouser.com/ProductDetail/KYOCERA-AVX/0402YD104MAT2A?qs=4PckX6MNpMErOINbbZj3Cw%3D%3D)            |
| ESP32-C6-WROOM-1-N8                       | [W25Q64JV             ](https://www.espressif.com/sites/default/files/documentation/esp32-c6-wroom-1_wroom-1u_datasheet_en.pdf)  | [RTC + BME688                ](https://www.digikey.com/en/products/detail/espressif-systems/ESP32-C6-WROOM-1-N8/17728866)            |
| Varistor USB PFMF.050.2                   | [Molex 104031-0811     ](https://ro.mouser.com/datasheet/2/358/typ_PFMF-1275918.pdf)                                          | [RTC + BME688               ](https://ro.mouser.com/ProductDetail/Schurter/PFMF.050.2?qs=1auRipcfynCums5v1iucSA%3D%3D)                  |
| DiodA Schottky SD0805S020S1R0             | [USB4110-GF-A           ](https://datasheets.kyocera-avx.com/schottky.pdf)                                                    | [Reset DS3231                ](https://www.digikey.com/en/products/detail/kyocera-avx/sd0805s020s1r0/3749517)                           |
| Senzor BME680                             | [SS14                  ](https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bme680-ds001.pdf)      | [ Interrupt RTC  ](https://www.digikey.com/en/products/detail/bosch-sensortec/bme680/7401317)                                           |
| Rezistori SMD 0402                        | [PFMF05S050T2          ](https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf)   | [Oscilator RTC ](https://www.digikey.com/en/products/detail/yageo/RC0402JR-07100KL/726416)                                              |
| P-MOS DMG2305UX-7                         | [TS-1187A-B-A-B        ](https://www.diodes.com/assets/Datasheets/DMG2305UX.pdf)                                              | [Boot                        ](https://www.digikey.com/en/products/detail/diodes-incorporated/DMG2305UX-7/4340667)                      |
| MCP73831T (Charger IC)                    | [RC0402FR-07100KL       ](https://ww1.microchip.com/downloads/en/DeviceDoc/MCP73831-Family-Data-Sheet-DS20001984H.pdf)        | [Navigare   ](https://www.digikey.com/en/products/detail/microchip-technology/MCP73831T-2ACI-OT/964301)                  |
| Hirose FH34SRJ-24S-0.5SH                  | [GRM155R61A105KE15D    ](https://ro.mouser.com/datasheet/2/185/FH34SRJ_24S_0_5SH_99__CL0580_1255_6_99_2DDrawing_0-1615044.pdf)| [Reset MCU                   ](https://ro.mouser.com/ProductDetail/Hirose-Connector/FH34SRJ-24S-0.5SH99?qs=vcbW%252B4%252BSTIpKBl5ap9J8Fw%3D%3D) |
| Battery Monitor MAX17048                  | https://www.analog.com/media/en/technical-documentation/data-sheets/max17048-max17049.pdf                                     | https://www.digikey.com/en/products/detail/analog-devices-inc-maxim-integrated/MAX17048G-T10/3758921 |
| Diodă MBR0530                             | https://ro.mouser.com/datasheet/2/258/MBR0520_MBR0580_SOD123_-2492194.pdf                                                     | https://ro.mouser.com/ProductDetail/Micro-Commercial-Components-MCC/MBR0530-TP?qs=KFo7JewZbUECRHkxGanrdg%3D%3D |
| ESD Suppressor – PGB1010603MR             | https://www.littelfuse.com/assetdocs/pulseguard-esd-suppressors-pgb1-datasheet?assetguid=8a337998-d54d-466b-be4e-dc5bcd1f9321 | https://www.digikey.com/en/products/detail/littelfuse-inc/PGB1010603MR/715755 |
| Qwiic Connector OM-E-QWIIC                | https://www.sparkfun.com/qwiic                                                                                                | https://www.digikey.com/en/products/detail/onion-corporation/om-e-qwiic/9922970 |
| Capacitor 0.5pF–100uF GCQ1555C1HR50WB01   | https://ro.mouser.com/datasheet/2/281/1/GCQ1555C1HR50WB01_01A-3146956.pdf                                                     | https://ro.mouser.com/ProductDetail/Murata-Electronics/GCQ1555C1HR50WB01D?qs=0lQeLiL1qybSG%2FOlONlvIA%3D%3D |
| USB-C Conector USB4110-GF-A               | https://gct.co/files/drawings/usb4110.pdf                                                                                     | https://eu.mouser.com/ProductDetail/GCT/USB4110-GF-A?qs=KUoIvG%2F9IlYiZvIXQjyJeA%3D%3D |
| Rezistor                                  | https://industrial.panasonic.com/ww/products/pt/general-purpose-chip-resistors/models/ERJ2GE0R00X                             | https://www.digikey.com/en/products/detail/panasonic-electronic-components/ERJ-2GE0R00X/146727 |
