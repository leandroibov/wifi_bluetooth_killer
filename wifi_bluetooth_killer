#!/bin/bash
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

