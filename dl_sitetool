#!/bin/bash

# Logo & Menù 
menu() {
        clear
	echo "   __   __       ___           _____          ";
	echo "  /  \ / /     ,' _/ ()/7  __ /_  _/_   _   /7";
	echo " / o |/ /_    _\  . /7/_7,'o/  / /,'o|,'o| // ";
	echo "/__,'/___/   /___,'////  |_(  /_/ |_,'|_,'//  ";
	echo "                                              ";                                                                              
        echo "   Choose an option:"
    	echo "1. Download only textual extraction"
    	echo "2. Download site"
    	echo "3. Download only photo"
    	echo "4. Exit"
}


# Choose site for textual extraction
option1() {
    read -p "Paste URL: " url

    if [ -z "$url" ]; then
        echo "URL not valid. Exit.."
        sleep 2
        return
    fi

    filename=$(basename "$url")
    w3m -dump "$url" | tr " " "\n" | grep -E '^[A-Za-z0-9\!-/\^]+$' | sort -u | tee -a "$filename.txt"
    
    echo "Ho contato" | wc -l "$filename.txt" "lines"
    #echo "Ho contato " sort -u "$filename.txt" | wc -l  echo "linee "  
        
    if [ $? -eq 0 ]; then
        echo "Site content successfully saved to $filename.txt"
    else
        echo "An error occurred while retrieving site content."
    fi

    read -n 1 -s -r -p "Press any key to continue..."
}


# Choose site for download
option2() {

    domain=$(echo "$url" | grep -oP '(?<=://)[^/]+')
    #echo "Dominio: $domain"

    read -p "Paste URL: " url

    if [ -z "$url" ]; then
        echo "URL not valid. Exit.."
        sleep 2
        return
    fi

    filename=$(basename "$url")
    wget --recursive --page-requisites --html-extension --convert-links --restrict-file-names=windows --domains "$domain" --no-parent -P ./site "$url" > "$filename"

    if [ $? -eq 0 ]; then
        echo "Site content successfully saved to $filename.txt"
    else
        echo "An error occurred while retrieving site content."
    fi

    read -n 1 -s -r -p "Press any key to continue..."
}


# Choose site for download only photo
option3() {
    read -p "Paste URL: " url

    if [ -z "$url" ]; then
        echo "URL not valid. Exit.."
        sleep 2
        return
    fi

    filename=$(basename "$url")
    wget -A "*.jpeg,*.jpg,*.bmp,*.gif,*.png" -r -nd -P ./site "$url" > "$filename"

    if [ $? -eq 0 ]; then
        echo "Site content successfully saved to $filename.txt"
    else
        echo "An error occurred while retrieving site content."
    fi

    read -n 1 -s -r -p "Press any key to continue..."
}

# Loop principale
while true; do
    menu
    read -p "Choose: " option

    case $option in
        1) option1 ;;
        2) option2 ;;
        3) option3 ;;
        4) echo "Exit..."; exit 0 ;;
        *) echo "Invalid option, try again." ;;
    esac
done
