# Windows SDK Data

Windows API listing in JSON format - generated from SDK headers + SDK API documentation for SAL notations. You can use it for fuzzing, writing Windbg extensions, PyKD script to dump parameters or writing Frida script that understands parameters.

* [windef.json](data/windef.json) contains common definitions used in other json files.
* [winbase.json](data/winbase.json) contains common base definitions used in other json files.

---
## JSON Scheme

---
### typedefs

The entry typedefs has the list of type definitions used in the function definitions.

   - name: name of the type
   - data_type: usually TypeDecl
   - type: original type

```
"typedefs": [
   {
      "name": "uintptr_t",
      "data_type": "TypeDecl",
      "type": "unsigned long long int"
   },
   {
      "data_type": "PtrDecl",
      "type": {
            "name": "va_list",
            "data_type": "TypeDecl",
            "type": "char"
      }
   },
```

---
#### typedefs -> struct

Following shows an entry that are using typedef to define structure named __crt_locale_data_public.

   - elements: contains list of structure/union elements

```
{
   "name": "__crt_locale_data_public",
   "data_type": "TypeDecl",
   "type": {
         "name": "__crt_locale_data_public",
         "data_type": "Struct",
         "elements": [
            {
               "data_type": "PtrDecl",
               "type": {
                     "name": "_locale_pctype",
                     "data_type": "TypeDecl",
                     "type": "unsigned short"
               }
            },
            {
               "name": "_locale_mb_cur_max",
               "data_type": "TypeDecl",
               "type": "int"
            },
            {
               "name": "_locale_lc_codepage",
               "data_type": "TypeDecl",
               "type": "unsigned int"
            }
         ]
   }
},
```

---
### structs

The structs entry has the list of structures used in the function definitions. The entry type_data.elements contains list of structure members.

```
    "structs": [

        {
            "name": "_SYSTEM_LOGICAL_PROCESSOR_INFORMATION_EX",
            "type_data": {
                "name": "_SYSTEM_LOGICAL_PROCESSOR_INFORMATION_EX",
                "data_type": "Struct",
                "elements": [
                    {
                        "name": "Relationship",
                        "data_type": "TypeDecl",
                        "type": "LOGICAL_PROCESSOR_RELATIONSHIP"
                    },
                    {
                        "name": "Size",
                        "data_type": "TypeDecl",
                        "type": "DWORD"
                    },
                    {
                        "data_type": "Union",
                        "elements": [
                            {
                                "name": "Processor",
                                "data_type": "TypeDecl",
                                "type": "PROCESSOR_RELATIONSHIP"
                            },
                            {
                                "name": "NumaNode",
                                "data_type": "TypeDecl",
                                "type": "NUMA_NODE_RELATIONSHIP"
                            },
                            {
                                "name": "Cache",
                                "data_type": "TypeDecl",
                                "type": "CACHE_RELATIONSHIP"
                            },
                            {
                                "name": "Group",
                                "data_type": "TypeDecl",
                                "type": "GROUP_RELATIONSHIP"
                            }
                        ]
                    }
                ]
            }
        },
```

---
### funcdefs

The funcdefs entry contains list of function definitions.
   - type: return type
   - arguments: list of arguments. SAL notations are extracted from SDK documents and sometimes it is missed.
   - api_locations: this information is also retrieved from SDK documents and it designates where the API exists.

```
    "funcdefs": [
        {
            "name": "BluetoothGATTGetServices",
            "type": {
                "data_type": "TypeDecl",
                "type": "HRESULT"
            },
            "arguments": [
                {
                    "name": "hDevice",
                    "data_type": "TypeDecl",
                    "type": "HANDLE",
                    "sal": [
                        "in"
                    ]
                },
                {
                    "name": "ServicesBufferCount",
                    "data_type": "TypeDecl",
                    "type": "USHORT",
                    "sal": [
                        "in"
                    ]
                },
                {
                    "name": "ServicesBuffer",
                    "data_type": "TypeDecl",
                    "type": "PBTH_LE_GATT_SERVICE",
                    "sal": [
                        "out",
                        "optional"
                    ]
                },
                {
                    "data_type": "PtrDecl",
                    "type": {
                        "name": "ServicesBufferActual",
                        "data_type": "TypeDecl",
                        "type": "USHORT"
                    },
                    "sal": [
                        "out"
                    ]
                },
                {
                    "name": "Flags",
                    "data_type": "TypeDecl",
                    "type": "ULONG",
                    "sal": [
                        "in"
                    ]
                }
            ],
            "api_locations": [
                "BluetoothAPIs.dll",
                "Ext-MS-Win-Bluetooth-APIs-l1-1-0.dll"
            ]
        },
```
