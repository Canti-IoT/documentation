Command for Configuring Recurrence over Bluetooth:

To configure recurrence, use the following command format. When writing the command along with the parameter index, the subsequent read operation will retrieve the same command and parameter index, with the following four bytes containing the value of the recurrence.

    Byte 0: 0xF1 - Command for accessing recurrence configuration.
    Byte 1: Parameter index.
    Bytes 2-5: Value of the recurrence for the given index. If this part is omitted, the entire configuration for the specified parameter will be readable in the next cycle.

For resetting to default recurrence:

    Byte 0: 0xF2 - Command for accessing recurrence configuration.
    Byte 1: Parameter index.

Command for Configuring Alarms over Bluetooth:

The protocol for setting alarms follows this format:

    Byte 0: 0xA{0..2} - Command to set the alarm parameter, where 0..2 represents the index of the alarm.
    Byte 1: Parameter index. If only this byte is written, the entire settings' value will be readable in the next cycle.
    Byte 2: Type of the interval {disabled, inside, outside}. If the next values are not provided, the value in the configuration will be updated, retaining old values for interval limits.
    Bytes 3-6: Lower value of the interval (optional). If not set, these values will be read in the next cycle.
    Bytes 7-10: Upper value of the interval (optional). If not set, these values will be read in the next cycle.

For disabling an alarm:

    Byte 0: 0xB{0..2}

For deleting an alarm:

    Byte 0: 0xD{0..2}


| **Command**              | **Byte 0** | **Byte 1** | **Bytes 2**      | **Bytes 3,4,5,6**       | **Bytes 7,8,9,10**      |
| ------------------------ | ---------- | ---------- | ---------------- | ----------------------- | ----------------------- |
| Recurrence Configuration | 0xF1       | Parameter  |                  | Recurrence              |                         |
|                          |            | Index      |                  | Value                   |                         |
| Resetting to Default     | 0xF2       | Parameter  |                  |                         |                         |
|                          |            | Index      |                  |                         |                         |
| Alarm Setting            | 0xA{0..2}  | Parameter  | Type of Interval | Lower value of interval | of interval Upper value |
|                          |            | Index      | type             | value                   | value                   |
| Disabling an Alarm       | 0xB{0..2}  |            |                  |                         |                         |
|                          |            |            |                  |                         |                         |
| Deleting an Alarm        | 0xD{0..2}  |            |                  |                         |                         |
