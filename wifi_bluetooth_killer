#!/bin/bash

####METHOD1
####METHOD1
####METHOD1
usb_1() {

echo;
echo "Enable or Disable Wi-Fi and Bluetooth network adapters or USB ports"
echo "Developer: leandroibov";
echo "lsusb";
lsusb;
echo;

echo "Select the idProduct and idVendor";
echo "Example: ID 0cf2:3011, in this order, 0cf2 is idvendor and 3011 is idproduct"
read -rp "Enter the id_Vendor name: " vendor_select
echo "The chosen id_Vendor name is: $vendor_select"
read -rp "Enter the id_Product name: " product_select
echo "The chosen id_Product name is: $product_select"
echo;

device_found=false

# Loop through all USB devices
for dir in /sys/bus/usb/devices/*; do
    if [ -f "$dir/idVendor" ] && [ -f "$dir/idProduct" ]; then
        vendor=$(cat "$dir/idVendor")
        product=$(cat "$dir/idProduct")
        if [ "$vendor" == "$vendor_select" ] && [ "$product" == "$product_select" ]; then
            device_found=true
            
            echo "Device found! Directory path: $dir"
            echo "Navigating to the directory..."
            cd "$dir"
            echo "Now in directory: $(pwd)"
            pwd;
            ls;
            echo "";
            echo "cat $dir/idProduct";
            cat "$dir/idProduct";
            echo "";
            echo "cat $dir/idVendor";
            cat "$dir/idVendor";
            echo "";
            echo "cat $dir/authorized";
            cat "$dir/authorized";
            echo "";
            
            echo "Do you want to enable (yes) or disable (no) the Wi-Fi or USB device? (yes/no)"
            read answer

            # Enable or disable device
            if [[ "$answer" == "yes" ]]; then
                echo "Enabling the device..."
                sudo echo 1 > "$dir/authorized"
            else
                echo "Disabling the device..."
                sudo echo 0 > "$dir/authorized"
            fi

            echo ""
            echo "cat $dir/authorized";
            cat "$dir/authorized";
            break
        fi
    fi
done

# If device was not found, show error message and exit after 10 seconds
if [ "$device_found" == false ]; then
    echo "Device with vendor ID $vendor_select and product ID $product_select not found!"
    echo "Exiting in 10 seconds..."
    sleep 10
    exit 1
fi

# Restart NetworkManager
echo "Restarting Network..."
sudo systemctl stop NetworkManager
sudo systemctl disable NetworkManager
sudo systemctl enable NetworkManager
sudo systemctl start NetworkManager

}

####METHOD2
####METHOD2
####METHOD2
pci_2() {
echo "All pci devices...";
lspci;
echo;
echo "wifi, bluetooth, ethernet modules and drivers in use..."
echo "---------------------------------------------------------------";
echo "wireless";
lspci -k | grep -A 3 -i wireless;
echo "---------------------------------------------------------------";
echo "bluetooth";
lspci -k | grep -A 3 -i bluetooth;
echo "---------------------------------------------------------------";
echo "ethernet";
lspci -k | grep -A 3 -i ethernet;
echo "---------------------------------------------------------------";
echo;

echo "Select the kernel driver in use or module (in use or not)"
echo "Example: Kernel driver in use or module: ath9k. Type 'ath9k'..."
read -rp "Enter the module name: " module
echo "The chosen module is: $module"
echo;

echo "Do you want to enable (yes) or disable (no) the Wi-Fi or Bluetooth? (yes/no)"
            read answer

            # Enable or disable device
            if [[ "$answer" == "yes" ]]; then
            echo;
                echo "Enabling the device..."
                sudo modprobe $module;
            else
            echo;
                echo "Disabling the device..."
                sudo rmmod $module;
                sudo modprobe -r $module;
            fi
            
          echo;
          echo "wifi, bluetooth, ethernet modules and drivers in use..."
echo "---------------------------------------------------------------";
echo "wireless";
lspci -k | grep -A 3 -i wireless;
echo "---------------------------------------------------------------";
echo "bluetooth";
lspci -k | grep -A 3 -i bluetooth;
echo "---------------------------------------------------------------";
echo "ethernet";
lspci -k | grep -A 3 -i ethernet;
echo "---------------------------------------------------------------";
echo;  
echo "---------------------------------------------------------------";
echo "Network Interfaces with nmcli";
nmcli;
echo "---------------------------------------------------------------";    
echo;
# Restart NetworkManager
echo "Restarting Network..."
sudo systemctl stop NetworkManager
sudo systemctl disable NetworkManager
sudo systemctl enable NetworkManager
sudo systemctl start NetworkManager              
}



####METHOD3
####METHOD3
####METHOD3
pci_3() {


echo "All pci devices...";
lspci;
echo;
echo "wifi, bluetooth, ethernet modules and drivers in use..."
echo "---------------------------------------------------------------";
echo "wireless";
lspci -k | grep -A 3 -i wireless;
echo "---------------------------------------------------------------";
echo "bluetooth";
lspci -k | grep -A 3 -i bluetooth;
echo "---------------------------------------------------------------";
echo "ethernet";
lspci -k | grep -A 3 -i ethernet;
echo "---------------------------------------------------------------";
echo;

echo "Select the kernel driver in use or module (in use or not)"
echo "Example: Kernel driver in use or module: ath9k. Type 'ath9k'..."
read -rp "Enter the module name: " module
echo "The chosen module is: $module"
echo;


echo "Disabling the device..."
sudo rmmod $module;
sudo modprobe -r $module;
echo;

echo "Adding module to blacklist...";
echo "sudo echo "$modulo" > /etc/modprobe.d/blacklist.conf;";
sudo echo "$modulo" > /etc/modprobe.d/blacklist.conf;
echo "sudo update-initramfs -u;";
sudo update-initramfs -u;
            
          echo;
          echo "wifi, bluetooth, ethernet modules and drivers in use..."
echo "---------------------------------------------------------------";
echo "wireless";
lspci -k | grep -A 3 -i wireless;
echo "---------------------------------------------------------------";
echo "bluetooth";
lspci -k | grep -A 3 -i bluetooth;
echo "---------------------------------------------------------------";
echo "ethernet";
lspci -k | grep -A 3 -i ethernet;
echo "---------------------------------------------------------------";
echo;  
echo "---------------------------------------------------------------";
echo "Network Interfaces with nmcli";
nmcli;
echo "---------------------------------------------------------------";    
echo;
# Restart NetworkManager
echo "Restarting Network..."
sudo systemctl stop NetworkManager
sudo systemctl disable NetworkManager
sudo systemctl enable NetworkManager
sudo systemctl start NetworkManager  


}

####METHOD4
####METHOD4
####METHOD4
exit_4() {
    echo;
    echo "Exiting the program in 6 seconds..."
    sleep 6
}







# Main loop
while true; do
echo;
    echo "-------------------------------------------------------------------------------------------------------------------------------------";
    echo "To turn off or turn on the WiFi and Bluetooth of the system, you need to use one of the first two options. Which one would you like?"
    echo "Option 1: WiFi and Bluetooth via USB"
    echo "Option 2: WiFi and Bluetooth via PCI"
    echo "Option 3: Disable WiFi and Bluetooth via PCI permanently before boot"
    echo "Option 4: Exit the program"

    read -p "Please choose an option (1/2/3/4): " choice
    echo "-------------------------------------------------------------------------------------------------------------------------------------";
    case $choice in
        1)
            usb_1
            ;;
        2)
            pci_2
            ;;
            
        3)
            pci_3
            ;;
        4)
            exit_4
            break
            ;;
        *)
            echo "Invalid option. Please choose 1, 2, or 3."
            ;;
    esac
done

