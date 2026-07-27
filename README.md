# Update a File Through a Python Algorithm

## Project Description
Company systems restrict content access using an IP address allow list stored in `allow_list.txt`. To maintain security, a separate remove list identifies IP addresses that must lose access. I developed a Python algorithm to automate updating `allow_list.txt` by removing these unauthorized IP addresses. 

*Note: The complete, executable script can be found in the Summary section at the bottom of this file.*

---

## Algorithm Steps

### 1. Open the File That Contains the Allow List
To begin, I assigned the file name as a string to the `import_file` variable and used a `with` statement to open it securely:

```python
import_file = "allow_list.txt"

with open(import_file, "r") as file:
```

The algorithm uses `with open(import_file, "r") as file:` to open the allow list. The `open()` function takes the file path and the `"r"` parameter to read the stored IP addresses. Using the `with` keyword automatically closes the file afterward, while the `as` keyword assigns the file object to the variable `file` for use within the block.

### 2. Read the File Contents
Next, I used the `.read()` method to convert the file contents into a string format:

```python
    ip_addresses = file.read()
```

Inside the `with` statement, calling `.read()` on the `file` variable converts the contents into a string. I assigned this string output to the variable `ip_addresses`. This process converts the `allow_list.txt` file into a string format, enabling my Python program to later organize and extract the data.

### 3. Convert the String into a List
To manipulate individual IP addresses, I split the string into a structured list:

```python
ip_addresses = ip_addresses.split()
```

Applying `.split()` to the `ip_addresses` string converts it into a list by splitting the text at each whitespace. Reassigning this list back to `ip_addresses` makes it easier to remove specific IP addresses later in the algorithm.

### 4. Iterate Through the Remove List
I set up a loop to cycle through every unauthorized IP address that needs to be restricted:

```python
for element in remove_list:
```

The `for` loop iterates through the `remove_list` sequence, executing the block for each item. The `for element in remove_list:` syntax assigns each individual IP address to the loop variable `element` during each iteration.

### 5. Remove IP Addresses That Are on the Remove List
Inside the loop, the algorithm evaluates each address and purges it from the allow list safely:

```python
    if element in ip_addresses:
        ip_addresses.remove(element)
```

The algorithm removes any IP address from `ip_addresses` that appears in `remove_list`. Since `ip_addresses` contains no duplicate entries, I used a conditional statement to check if `element` is in `ip_addresses` before running `ip_addresses.remove(element)`. This prevents a runtime error if an IP address from the removal list is not present.

### 6. Update the File with the Revised List of IP Addresses
Finally, I prepared the data and updated `allow_list.txt` by overwriting its contents:

```python
ip_addresses = "\n".join(ip_addresses)

with open(import_file, "w") as file:
    file.write(ip_addresses)
```

The `.join()` method converts the `ip_addresses` list into a single string, using `"\n"` as a separator to place each address on a new line. This string is then passed to the `.write()` method inside a new `with` statement using the `"w"` argument to open the file in write mode. Calling `file.write(ip_addresses)` replaces the old data with the updated string, ensuring the removed IP addresses no longer have access.

---

## Summary
I created an algorithm to remove IP addresses from `remove_list` from the `allow_list.txt` file. The script reads the file into a list, safely removes the matching unauthorized addresses using a loop, and then converts the list back into a string to overwrite the original file.

### Complete Final Code
```python
# Define the file path and the list of IPs to remove
import_file = "allow_list.txt"
remove_list = ["192.168.1.10", "192.168.1.11"]  # Example removal list

# Open the file and read the contents
with open(import_file, "r") as file:
    ip_addresses = file.read()

# Convert the string of IP addresses into a list
ip_addresses = ip_addresses.split()

# Loop through the removal list and remove matching IPs
for element in remove_list:
    if element in ip_addresses:
        ip_addresses.remove(element)

# Convert the list back into a newline-separated string
ip_addresses = "\n".join(ip_addresses)

# Overwrite the original file with the updated string
with open(import_file, "w") as file:
    file.write(ip_addresses)
```

