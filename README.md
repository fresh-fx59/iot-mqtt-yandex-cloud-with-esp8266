# Description
This code gives you an ability to blink with embedded diod of NodeMCU ESP8266. Send message to MQTT server in Yandex Cloud and blink embeded diod in NodeMCU on ESP8266

# Prerequistions
- VS Code with PlatformIO installed([video guide](https://youtu.be/AXLhvjKyWWM))
- NodeMCU ESP8266
- Yandex Cloud account
- Postman or [Yandex Cloud (CLI)](https://cloud.yandex.ru/en/docs/cli/quickstart)

# Steps to blink
- register on [Yandex Cloud](https://cloud.yandex.com/)
- enter payment information
- follow [this](https://cloud.yandex.ru/en/docs/iot-core/quickstart) guide to setup registry and device
- clone the project in VS code
- fill in your credentials into _include/secret.h_
- build and upload firmware to NodeMCU
- check that node mcu started, connected to Wi-Fi, MQTT and ready to accept messages
- [generate](https://cloud.yandex.com/en-ru/docs/iam/operations/iam-token/create) Yandex IAM token
- execute the command below to manage the diod

```bash
yc iot mqtt publish \
  --cert cert.pem \
  --key private-key.pem \
  --topic '$devices/YOUR_DEVICE_ID_NOT_NAME/commands' \
  --message '0' \
  --qos 1
```

You should use registry certs to perform this command. Change message to 1 and see what will happen. It is possible to use postman with Bearer token authorisation. And raw body would be

```
{
  "topic": "$devices/YOUR_DEVICE_ID_NOT_NAME/commands",
  "data": "MA=="
}
```

MA== - 0 in bytes

MQ== - 1 in bytes

Based on [this](https://projectalt.ru/publ/arduino_esp8266_i_esp32/programmirovanie/prostoe_podkljuchenie_esp8266_k_jandeks_alise/11-1-0-32) post
