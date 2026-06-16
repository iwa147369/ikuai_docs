# AP List

**Source:** https://www.ikuai8.com/support/ymgn/lyym/ac/1222233332.html

## I. Overview

The AP List page shows all APs that have connected to the AC. You can configure AP names, channels, SSID settings, and other parameters from this page.

![AP List](https://www.ikuai8.com/images/support_202109/aplb12.png)

---

## II. Deployment Steps

Follow this sequence when deploying APs:

1. Configure a DHCP server on the AC to assign IPs to APs.
2. Enable AC Smart Control on the router; configure the default AP config in **Configuration Management**.
3. Ensure the APs and the AC are on the same LAN.

Optional:
4. To customize individual APs, select them on the AP List page and apply specific settings.

---

## III. AP Configuration Priority

1. When an AP first joins, it uses the **default configuration**.
2. After initial setup, each AP can be individually configured. If an AP goes offline and reconnects, it automatically re-applies its last saved configuration.
3. After an AP joins a **group**, it uses the group's configuration. Individual overrides within the group are still possible.
4. When an AP leaves a group, it reverts to its pre-group configuration. Any individual settings applied while in the group are not restored.

---

## IV. Page Controls

![AP List Controls](https://www.ikuai8.com/images/support/aplb11.png)

**Filter controls:**
- **All Groups** — Filter APs by group.
- **All Status** — Filter by status: Normal, Not Connected, Upgrading.
- **All Radio** — Filter by band: 2.4G single-band, or 2.4G+5G dual-band.

**Action buttons:**

| Button | Description |
|---|---|
| Interference Analysis | Detect interference among iKuai APs in this environment |
| Import | Import AP configurations (CSV or TXT format) |
| Export | Export AP configurations (CSV or TXT format) |
| Default Config | Set the default configuration applied to new APs when they first join |
| Bulk Config | Apply the same settings to multiple APs simultaneously |
| Join Group | Add selected APs to an existing AP group |
| Remove from Group | Remove selected APs from their group; APs revert to pre-group config |

---

## V. Column Descriptions

| Column | Description |
|---|---|
| Status | AP connection state: Normal, Not Connected, or Upgrading |
| Group Name | The group this AP belongs to |
| 2.4G SSID | The broadcast name for the 2.4G radio |
| 5G Radio1/2 SSID | The broadcast names for the 5G radios |
| Channel | The current channel being used |
| Uplink Speed | Negotiated speed on the AP's ethernet port |
| Current / Max Clients | Current connected clients vs. maximum allowed |
| Model | AP hardware model |
| Firmware Version | Current AP firmware version |
| Channel Utilization 2.4G | Percentage of channel airtime in use (2.4G) |
| Channel Utilization 5G Radio1/2 | Percentage of channel airtime in use (5G) |
| Noise Floor 2.4G | Background noise level on the 2.4G channel |
| Noise Floor 5G Radio1/2 | Background noise level on the 5G channel(s) |
| Min RSSI 2.4G | Weakest client signal currently connected on 2.4G |
| Min RSSI 5G Radio1/2 | Weakest client signal currently connected on 5G |
| Up/Down Rate | Current upload and download throughput |
| Remark | Custom label for the AP |
| Actions | Edit details, change remark, join group, uninstall |

---

## VI. AP Edit Options

| Option | Description |
|---|---|
| SSID1 Name | Wireless network name (broadcast SSID) |
| SSID1 Security Type | Encryption type. WPA3 is supported on select AP models with updated firmware. |
| SSID1 VLAN | Enable SSID VLAN for this wireless network |
| Hide SSID1 Name | When enabled, the SSID is not broadcast and won't appear in scan results |
| SSID Rate Limit | Shared upload/download limit for all clients on this SSID. Requires AP firmware v1.5.6+ |
| Guest Mode | When enabled, clients can only access the internet — LAN-to-LAN communication is blocked |
| DingTalk Binding | Auto-enabled when DingTalk is bound; SSID3 and SSID4 become reserved |
| Channel | Recommended channels: 2.4G — 1, 6, 11; 5G — 36, 44, 149, 157. Channels 12 and 13 require AP firmware v1.5.6+ |
| Max Clients | Maximum number of connected clients. `0` = unlimited |
| AP Signal Power | Transmit power: 40%, 60%, 80%, or 100% |
| Channel Width | 2.4G: 20 MHz (173 Mbps) or 40 MHz (433 Mbps). 5G: 40 MHz or 80 MHz (866 Mbps) |
| 5G Priority | When enabled with matching SSID names across bands, dual-band capable clients prefer 5G |
| AP Remark | Custom label for this AP |
| Fast Roaming | Enables 802.11r fast BSS transition for seamless roaming |
| Scheduled On | Set a time window during which the AP's radio is active |
| Scheduled Restart | Automatically restart the AP on a schedule |
| Status LED | Enable or disable the AP's LED indicator. Supported on panel-type APs with firmware v1.5.6+ |
| Multi-SSID Mode | Supported models and limits: X3/X5/X6/DX3 — up to 32 SSIDs (16 per band); X7/SW7/L50-R — up to 18 SSIDs (9 per band). Requires latest AP firmware. |
| Gateway Detection | If enabled, the AP automatically disables its radio when the gateway is unreachable |

---

### Multi-SSID Mode Details

In multi-SSID mode, each radio supports up to 16 SSIDs (9 for X7/SW7). Each line in the SSID field defines one network name.

When SSID VLAN is configured in multi-SSID mode, the entered VLAN ID is the **starting VLAN** — each SSID gets an incrementing VLAN ID:

Example: 4 SSIDs (`ikuai01`–`ikuai04`) with starting VLAN 1001:
- `ikuai01` → VLAN 1001
- `ikuai02` → VLAN 1002
- `ikuai03` → VLAN 1003
- `ikuai04` → VLAN 1004

---

### Country/Region

Select the operating region to apply the correct channel and frequency regulations. Supported regions: China, Taiwan, USA. Default: China. Requires AP firmware v2.3.0+.

![Country Selection](https://www.ikuai8.com/images/support_202109/guojdq.png)

---

### Roaming Sensitivity

Controls the signal threshold at which a client roams to a better AP. Requires AP firmware v2.3.0+.

| Level | Signal Threshold |
|---|---|
| Very Low | -70 dBm |
| Low | -67 dBm |
| Medium | -64 dBm |
| High | (stronger threshold) |
| Very High | (strongest threshold) |
