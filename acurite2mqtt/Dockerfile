ARG BUILD_FROM
FROM ${BUILD_FROM}

# Define environment variables
# Use this variable when creating a container to specify the MQTT broker host.
ENV MQTT_HOST=127.0.0.1 \
    MQTT_PORT=1883 \
    MQTT_USERNAME="" \
    MQTT_PASSWORD="" \
    MQTT_RETAIN=True \
    MQTT_TOPIC=rtl_433 \
    PROTOCOL="" \
    WHITELIST_ENABLE=False \
    EXPIRE_AFTER=0 \
    WHITELIST="" \
    DISCOVERY_PREFIX=homeassistant \
    DISCOVERY_INTERVAL=600 \
    AUTO_DISCOVERY=True \
    DEBUG=False \
    LANG=C.UTF-8

LABEL Maintainer="Jeffrey Stone" \
io.hass.name="acurite2mqtt" \
io.hass.type="addon" \
io.hass.description="This image is used to start the RTL433 to HASS script that will monitor for 433Mhz devices and send the data to an MQTT server"

WORKDIR /data

# Copy scripts
COPY entry.sh rtl_433_mqtt_hass.py /scripts/
# install rtl_433, rtl-sdr, libusb, mosquitto-clients, python3 py3-paho-mqtt; and deps of rtl_433_mqtt_hass.py.
# make entry.sh and rtl_433_mqtt_hass.py executable.
RUN apk add --no-cache bash 
RUN apk add --no-cache libusb 
RUN apk add --no-cache mosquitto-clients 
RUN apk add --no-cache python3 
RUN apk add --no-cache py3-paho-mqtt
#RUN apk add --no-cache rtl-sdr rtl_433 libusb mosquitto-clients python3 py3-paho-mqtt 
    #chmod +x /scripts/entry.sh && \
    #chmod +x /scripts/rtl_433_mqtt_hass.py

# Execute entry script
ENTRYPOINT [ "/scripts/entry.sh" ]
