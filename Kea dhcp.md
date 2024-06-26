
{
  "Dhcp4": {
     "interfaces-config": {
    },
	"interfaces": [ "ens3" ]
		"control-socket": {
		},
		"socket-type": "unix",
		"socket-name": "/tmp/kea4-ctrl-socket"
		"lease-database": {
		"type": "memfile",
		"Ifc-interval": 3600
		},
		{
"option-data": [
"name": "domain-name-servers",
"data": "192.168.11.100, 100.100.100.100"
},
{
"name": "domain-search",
"data": "klg.jun.profi"
}
1,
/etc/kea/kea-ancp4.conf
"subnet4": [ { "id": 3, "subnet": "192.168.11.0/24" },
{
"id": 1,
"subnet": "192.168.10.0/24",
"pools": [ { "pool": "192.168.10.11 192.168.10.254" } ], "reservations": [
{
}],
"hw-address": "02:00:02:38:e7:14",
"ip-address": "192.168.10.13"
"option-data": [
{
}
]},{
"id": 2,
"name": "routers",
"data": "192.168.10.1"
"subnet": "192.168.13.0/24",
"pools": [ { "pool": "192.168.13.11
-
192.168.13.254" } ],

{
GNU nano 7.2
"Dhcp4": {
"interfaces-config": {
},
"interfaces": [ "ens3" ]
"control-socket": {
},
"socket-type": "unix",
"socket-name": "/tmp/kea4-ctrl-socket"
"lease-database": {
"type": "memfile",
"Ifc-interval": 3600
},
{
"option-data": [
"name": "domain-name-servers",
"data": "192.168.11.100, 100.100.100.100"
},
{
"name": "domain-search",
"data": "klg.jun.profi"
}
1,
/etc/kea/kea-ancp4.conf
"subnet4": [ { "id": 3, "subnet": "192.168.11.0/24" },
{
"id": 1,
"subnet": "192.168.10.0/24",
"pools": [ { "pool": "192.168.10.11 192.168.10.254" } ], "reservations": [
{
}],
"hw-address": "02:00:02:38:e7:14",
"ip-address": "192.168.10.13"
"option-data": [
{
}
]},{
"id": 2,
"name": "routers",
"data": "192.168.10.1"
"subnet": "192.168.13.0/24",
"pools": [ { "pool": "192.168.13.11
-
192.168.13.254" } ],
A