# ESPHome Router Supervisor

## Overview

This project uses ESPHome on an ESP8266 to monitor your router's internet connectivity by periodically establishing a TCP connection to 8.8.8.8 on port 53. If three consecutive connectivity checks fail, the firmware triggers a router reboot via a connected relay. After two reboot attempts, the system enters a 30-minute lockout period before retrying, helping prevent continuous reboot cycles.

## Features

- **Automated Connectivity Monitoring:** Checks connectivity every 60 seconds.
- **Automated Reboot:** Triggers a router reboot via a relay after three consecutive failures.
- **Lockout Mechanism:** After two reboot attempts, enters a 30-minute lockout period before trying again.
- **ESPHome Integration:** Easily managed via the ESPHome Dashboard or Home Assistant.

## Hardware Requirements

- ESP8266 board (e.g., ESP01S)
- Relay module (to control router power/reset)
- Appropriate wiring and power supply

## Software Requirements

- [ESPHome](https://esphome.io/)
- ESPHome Dashboard or command-line tool for firmware upload and logs

## Installation

1. **Clone this repository:**
   ```bash
   git clone https://github.com/jpucheu/supervisor.git
   cd supervisor
2. **Edit the YAML file:**
- Open router_rebooter.yaml and update the WiFi credentials.
- Adjust hardware pin assignments if necessary.
3. **Compile and Upload:**
bash
esphome supervisor.yaml run
4. **Monitor Logs:**
Use the ESPHome Dashboard or run:
esphome supervisor.yaml logs
to ensure the connectivity checks and reboot logic are functioning as expected.
## Configuration
- Connectivity Check: The script attempts a TCP connection to 8.8.8.8 on port 53 every 60 seconds.
- Relay Control: The relay is connected to GPIO0 and toggled for 15 seconds during a reboot attempt.
- Lockout Period: After two reboot attempts, the system waits 30 minutes before resetting the counters and resuming normal operation.
## Troubleshooting
- Verify that the ESP8266 is properly connected to your WiFi network.
- Ensure that the wiring for the relay is correct.
- Check the ESPHome logs for messages indicating connectivity status and reboot attempts.
- Adjust intervals and thresholds in the YAML file as needed to suit your network environment.
## Contributing
Contributions are welcome! Please open an issue or submit a pull request with any improvements or bug fixes.

## License
This project is licensed under the MIT License.
