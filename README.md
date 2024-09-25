# STM32L4 Flash Memory Library
 A useful library for STM32L4 microcontrollers to interface with internal flash memory. This library provides functions to erase flash pages, write data to flash, and read data from flash memory.
 
 # Features
 
 - **Erase** specified flash pages
 - **Write** data to flash memory
 - **Ready** data from flash memory
 - Support multiple memory sizes (128KB, 256KB, 512KB)
 
 
  ## Requirments
  
  - **STM32L4 series mirocontroller**
  - **STM32L4xx HAL drivers**
  - **ARM Cortex-M compiler** (e.g., GCC Arm Embedded)

  ## Installation

   1. Clone the repository and include it in your STM32 project:

   ```bash
   git clone https://github.com/DarthFelus/STM32L4-Flash-Memory-Library.git
   ```
   2. Add Files to Project: Include **Flash.h**, **Flash.c**, and **FlashAdresses.h** in your project source files.
   3. Include Header: Add the following line to your source code where flash operations are needed:
   ```c 
   #include "Flash.h"
   ```
   
   ## Configuration
   Define your microcontroller's flash memory size by adding one of the following macros before including the library:
   
   ```c 
   #define MEMORY_128KB
   // or
   #define MEMORY_256KB
   // or
   #define MEMORY_512KB
   ```
   These definitions ensure that the correct last page address is calculated based on your device's flash memory size.
   
   ## Usage
   
   1. **Erase a Flash Page:**
   ```c 
   uint32_t pageAddress = ADDR_FLASH_PAGE_63; // Replace with your target page address

   HAL_StatusTypeDef status = FlashErase(pageAddress);

   if (status == HAL_OK) {
     // Erase successful
   } else {
     // Handle error
   }
   ```
   2. **Write Data to Flash:**
   ```c 
	uint32_t flashAddress = 0x0801F800; // Replace with your target flash address
	uint64_t data = 0x12345678ABCDEF00; // Data to write (64-bit)

	HAL_StatusTypeDef status = FlashWrite(flashAddress, data);

	if (status == HAL_OK) {
		// Write successful
	} else {
		// Handle error
	}
   ```
   
   3. **Read Data from Flash**
   ```c 
	uint32_t flashAddress = 0x0801F800; // Replace with your target flash address

	uint64_t data = FlashRead(flashAddress);

		// Use the read data
   ```   
   
   ## API Reference
   
1. **FlashErase**
   ```c 
	HAL_StatusTypeDef FlashErase(uint32_t PageAddress);
   ```
   Erases the specified flash memory page.

- **Parameters**
        *PageAddress*: The starting address of the flash page to erase.
- **Returns**
        *HAL_OK* on success, or an error code.
2. **FlashWrite**
  ```c 
	HAL_StatusTypeDef FlashWrite(uint32_t Address, uint32_t Data);
  ```
    Writes a 64-bit double word to the specified flash memory address.
	
- **Parameters**
	*Address*: The flash memory address where data will be written. Must be double-word aligned.
	*Data*: The 64-bit data to write.
-**Returns**
	*HAL_OK* on success, or an error code.
		
3. **FlashRead**
	```c 
	uint64_t FlashRead(uint32_t Address);
    ```	
    Reads a 64-bit double word from the specified flash memory address.
	
- **Parameters**
	*Address*: The flash memory address to read from. Must be double-word aligned.
- **Returns**
	The 64-bit data read from flash memory.
		
   ## Important Notes
- The library internally handles the **unlocking and locking of flash memory.**
- Ensure that the addresses used are correct and aligned as required by the **STM32 flash memory specifications.**
- Ensure the flash memory region you're accessing is not **write-protected.**
- Always verify the written data by reading it back.
- Be cautious when performing erase operations to avoid unintentional **data loss.**
- Avoid flash operations while executing code from flash memory to prevent **unexpected behavior.**

   ## Files Description

 **Flash.h**: Header file containing function prototypes and necessary includes.
 **Flash.c**: Source file with the implementation of flash operations.
 **FlashAdresses.h**: Header file defining flash page addresses based on the STM32L4 microcontrollers memory size.

   ## Version History

  v1.0.0 (29.07.2024)
     Initial release

   ## License
   
   This project is licensed under the MIT License. See the LICENSE file for details.

   ## Contributing

   Feel free to contribute by opening issues or submitting pull requests.
	
	
