### **Top-Level Keys**

1. **type**: E.g., "Laptop"
2. **brand**: E.g., "Apple"
3. **model_identifier**: E.g., "A1707"
4. **model_description**: E.g., "MacBook Pro (15-inch, 2018)"
5. **release_date**: E.g., "2018-07-12"
6. **discontinued_date**: E.g., "2019-05-21"
7. **model_number**: E.g., "MV962LL/A"
8. **repairability_score**: E.g., 1–10 scale
9. **version**: E.g., 1

### **Hardware Details**

#### Memory

10. **memory.format**: E.g., "DDR3L"
11. **memory.available_sizes**: E.g., ["8GB", "16GB"]
12. **memory.max_ram**: E.g., "16GB"
13. **memory.speed**: E.g., "2133MHz"
14. **memory.ecc**: Boolean
15. **memory.soldered**: Boolean
16. **memory.channels**: E.g., 2

#### Storage

17. **storage.type**: E.g., "SSD", "HDD"
18. **storage.capacity**: E.g., "256GB"
19. **storage.connector**: E.g., "Proprietary PCIe"
20. **storage.max_capacity**: E.g., "1TB"
21. **storage.removable**: Boolean
22. **storage.raid_support**: Boolean

#### Processor

23. **processor.model**: E.g., "Intel Core i7-8750H"
24. **processor.socket**: E.g., "BGA1440"
25. **processor.architecture**: E.g., "64-bit"
26. **processor.cores**: E.g., 4
27. **processor.threads**: E.g., 8
28. **processor.base_clock**: E.g., "2.2GHz"
29. **processor.boost_clock**: E.g., "4.1GHz"
30. **processor.tdp**: E.g., "45W"

#### GPU

31. **gpu.model**: E.g., "AMD Radeon Pro 560X"
32. **gpu.type**: E.g., "Dedicated"
33. **gpu.memory**: E.g., "4GB GDDR5"
34. **gpu.connector**: E.g., "PCIe"
35. **gpu.cooling_type**: E.g., "Active"

#### Screen

36. **screen.size**: E.g., "13.3 inches"
37. **screen.resolution**: E.g., "2560x1600"
38. **screen.aspect_ratio**: E.g., "16:10"
39. **screen.panel_type**: E.g., "Retina Display (IPS)"

#### Ports

40. **port_types.type**: E.g., "USB-C"
41. **port_types.version**: E.g., "Thunderbolt 3"
42. **port_types.quantity**: E.g., 4
43. **port_types.features**: E.g., ["Power Delivery", "Video Output"]

#### Wireless

44. **wireless.wifi.standard**: E.g., "802.11ac"
45. **wireless.wifi.frequency_bands**: E.g., ["2.4GHz", "5GHz"]
46. **wireless.bluetooth.version**: E.g., "5.0"

### **Optical**

47. **optical.drive_type**: E.g., "None"

### **Repairability Insights**

48. **repairability_insights.battery.accessibility**: E.g., "Difficult"
49. **repairability_insights.ram_storage.accessibility**: E.g., "Not Upgradeable"
50. **repairability_insights.adhesive_level**: E.g., "High"

### **Additional Metadata**

51. **repair_difficulty**: E.g., "High"
52. **disassembly_steps**: E.g., 25
53. **known_issues**: E.g., ["Battery degradation", "Keyboard issues"]