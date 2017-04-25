# leafpy
lightweight python interface to the nissan leaf

[![PyPI version](https://badge.fury.io/py/leafpy.svg)](https://badge.fury.io/py/leafpy)

# Installation
```
pip install leafpy
```

# Examples:

Login:
----

```python
from leafpy import Leaf
leaf = Leaf('<your-username>', '<your-password>')
```

Or with custom_sessionid & VIN:

```python
from leafpy import Leaf
leaf = Leaf(custom_sesionid='<your-custom_sessionid>', VIN='<your-VIN>')
# you can get these values from a previous login:
# leaf.VIN, leaf.custom_sessionid
```

*Check Battery Status:*
-----
```python
leaf.BatteryStatusRecordsRequest()
```
results in:
```json
{
	"status": 200,
	"BatteryStatusRecords": {
		"BatteryStatus": {
			"BatteryRemainingAmountkWH": "",
			"SOC": {
				"Value": "100"
			},
			"BatteryChargingStatus": "NOT_CHARGING",
			"BatteryRemainingAmount": "240",
			"BatteryCapacity": "240",
			"BatteryRemainingAmountWH": "28880"
		},
		"OperationResult": "START",
		"NotificationDateAndTime": "2017/04/24 23:43",
		"CruisingRangeAcOff": "198000",
		"OperationDateAndTime": "2017/04/24 23:43",
		"CruisingRangeAcOn": "192000",
		"PluginState": "CONNECTED",
		"TargetDate": "2017/04/24 23:43"
	},
	"VoltLabel": {
		"HighVolt": "240",
		"LowVolt": "120"
	}
}
```
*Query for Battery Status:*
-----
```python
response = leaf.BatteryStatusCheckRequest()
# Wait a few seconds for the request to be made to the car
leaf.BatteryStatusCheckResultRequest(resultKey=response['resultKey'])
```
results in:
```json
{
	"status": 200,
	"currentChargeLevel": "0",
	"timeRequiredToFull": {
		"hours": "",
		"minutes": ""
	},
	"timeRequiredToFull200_6kW": {
		"hours": "",
		"minutes": ""
	},
	"operationResult": "START",
	"timeStamp": "2017-04-25 05:23:48",
	"pluginState": "CONNECTED",
	"cruisingRangeAcOff": "198000.0",
	"timeRequiredToFull200": {
		"hours": "",
		"minutes": ""
	},
	"batteryCapacity": "240",
	"cruisingRangeAcOn": "192000.0",
	"responseFlag": "1",
	"batteryDegradation": "240",
	"charging": "NO",
	"chargeStatus": "CT",
	"chargeMode": "NOT_CHARGING"
}
```
