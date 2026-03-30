# API — Zane Temperature Subsystem

## Subsystem Overview

### Subsystem Role
The Zane subsystem receives data from the JT subsystem, reads temperature data from a local temperature sensor, and sends both values to the Abriana subsystem for display on the OLED. This subsystem is part of the UART daisy-chain communication loop, so it must also forward messages intended for other subsystems while processing messages intended for itself.

### Data Flow
**JT Subsystem → Zane Subsystem → Abriana OLED Subsystem**

### Zane Subsystem Responsibilities
- Receive JT data
- Store JT data
- Read temperature sensor data
- Combine JT data and temperature data
- Send combined data to Abriana
- Forward unrelated messages in the daisy chain

---

## Message Protocol Notes

These tables describe only the **message data bytes** inside the class messaging protocol. They do **not** include the packet prefix, suffix, sender, or receiver fields, since those are part of the shared class communication specification.

The message type values shown below are placeholders and must match the final values agreed on by the team.

---

## Messages Received by Zane Subsystem

### Message Type 1 — JT Data Input

This message is received from the JT subsystem and contains the value that the Zane subsystem must store and later forward along with temperature data.

| Byte | Variable Name | Data Type | Number of Bytes | Min Value | Max Value | Example |
|------|---------------|-----------|-----------------|-----------|-----------|---------|
| 1 | `message_type` | `uint8_t` | 1 | 1 | 1 | 1 |
| 2 | `jt_data` | `uint8_t` | 1 | 0 | 255 | 1 |

#### Description
This message is sent from the JT subsystem to the Zane subsystem. The Zane subsystem stores the incoming JT data value and later combines it with the current temperature reading before sending the result to the Abriana subsystem.

---

## Local Sensor Data Used by Zane

### Message Type 2 — Temperature Reading

This message represents the local temperature data measured by the temperature sensor connected to the Zane subsystem.

| Byte | Variable Name | Data Type | Number of Bytes | Min Value | Max Value | Example |
|------|---------------|-----------|-----------------|-----------|-----------|---------|
| 1 | `message_type` | `uint8_t` | 1 | 2 | 2 | 2 |
| 2 | `temperature_c` | `int8_t` | 1 | -40 | 125 | 26 |

#### Description
This message contains the current temperature measured by the local temperature sensor in degrees Celsius. The measured temperature is stored as an integer value and used in the outgoing display-data message.

> **Note:** If the final team design requires decimal precision, this field may need to be changed to a larger type such as `int16_t` and scaled by a factor of 10.

---

## Messages Sent by Zane Subsystem

### Message Type 3 — Combined Display Data to Abriana

This is the main output message sent from the Zane subsystem to the Abriana OLED subsystem.

| Byte | Variable Name | Data Type | Number of Bytes | Min Value | Max Value | Example |
|------|---------------|-----------|-----------------|-----------|-----------|---------|
| 1 | `message_type` | `uint8_t` | 1 | 3 | 3 | 3 |
| 2 | `jt_data` | `uint8_t` | 1 | 0 | 255 | 1 |
| 3 | `temperature_c` | `int8_t` | 1 | -40 | 125 | 26 |

#### Description
This message is sent from the Zane subsystem to the Abriana subsystem. It contains both the stored JT data and the most recent temperature reading. The Abriana subsystem uses this message to display both values on the OLED.

---

## Optional Broadcast or Control Messages

If the team uses broadcast messages such as start, stop, reset, or emergency stop, the Zane subsystem must also handle those messages.

### Example Broadcast Command Message

| Byte | Variable Name | Data Type | Number of Bytes | Min Value | Max Value | Example |
|------|---------------|-----------|-----------------|-----------|-----------|---------|
| 1 | `message_type` | `uint8_t` | 1 | 10 | 10 | 10 |
| 2 | `command` | `uint8_t` | 1 | 0 | 2 | 1 |

### Example Command Values
- `0` = Stop
- `1` = Start
- `2` = Reset

#### Description
These commands may be broadcast to all subsystems on the UART network. If used by the team, the Zane subsystem must recognize the command and respond appropriately.

---

## Handling Code

### Receiver Requirements
The Zane subsystem must implement a message receiver that:
- handles all messages sent through the UART daisy-chain network
- passes on messages intended for someone else
- processes messages intended for the Zane subsystem
- discards messages sent by itself that return through the loop
- ignores messages that are malformed
- ignores messages larger than the local buffer size
- ignores characters outside of a valid message frame

### Receiver Behavior
When a message is received, the Zane subsystem should:
1. check whether the message is properly framed
2. verify that the packet length is valid
3. determine whether the receiver field matches the Zane subsystem or a broadcast address
4. forward packets intended for other subsystems
5. discard packets that originated from the Zane subsystem and returned through the loop
6. process packets addressed to the Zane subsystem

### Processing Rules
- If a JT data message is received, store the JT data value
- If a control message is received, respond according to the command
- If a malformed packet is received, ignore it
- If a valid message for another subsystem is received, pass it along unchanged

---

## Sender Requirements

The Zane subsystem must also implement a message sender that:
- sends properly formatted messages
- sends an example of each message type with time-varying data
- includes the correct prefix and suffix
- uses the correct sender and receiver addresses
- ensures the message data does not contain invalid framing bytes
- does not send data longer than the allowed packet size
- prioritizes forwarding incoming messages before sending its own messages
- limits the sending rate using proper programming techniques such as timers, interrupts, or non-blocking code

### Sender Behavior
The sender should:
1. read the current temperature sensor value
2. retrieve the most recently stored JT data
3. build a valid outgoing message packet
4. send the combined data message to Abriana
5. repeat at a controlled rate

---

## Example Message Flow

### Step 1 — JT Sends Data to Zane
JT sends a message to the Zane subsystem containing:
- `jt_data = 1`

### Step 2 — Zane Stores JT Data
The Zane subsystem receives and stores:
- `jt_data = 1`

### Step 3 — Zane Reads Temperature Sensor
The Zane subsystem reads:
- `temperature_c = 26`

### Step 4 — Zane Sends Combined Message to Abriana
The Zane subsystem sends:
- `jt_data = 1`
- `temperature_c = 26`

This combined message is then used by the Abriana subsystem for OLED display.

---

