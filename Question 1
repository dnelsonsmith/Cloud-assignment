# Create 4 script with the .sh file script.sh script1.sh script2.sh script3.sh inside the particular folder
# create a countscript.sh file in the same folder
# use nano to edit thre countscript.sh file annd include the bash code to be able to count all the shebangs
#!/bin/bash

# Specify the directory to analyze
directory="/home/dnelsonsmith/"

# Arrays to store shebangs and their corresponding counts
declare -a shebangs
declare -a counts

# Iterate through each file in the directory
for file in "$directory"/*; do
    # Check if it's a regular file, has execute permission, and contains a shebang line
    if [[ -f "$file" && -x "$file" && $(head -n 1 "$file" | grep -c -P '#!\s*\K\S+') -gt 0 ]]; then
        # Extract the shebang line from the file
        shebang=$(head -n 1 "$file" | grep -o -P '#!\s*\K\S+')

        # Check if the shebang is already in the array
        found=false
        for i in "${!shebangs[@]}"; do
            if [ "${shebangs[$i]}" == "$shebang" ]; then
                found=true
                ((counts[$i]++))  # Increment the count for existing shebang
                break
            fi
        done

        # If shebang is not in the array, add it along with count 1
        if [ "$found" == false ]; then
            shebangs+=("$shebang")
            counts+=(1)
        fi
    fi
done

# Display the results
for i in "${!shebangs[@]}"; do
    count=${counts[$i]}
    shebang=${shebangs[$i]}
    echo "$shebang : There are $count shebangs files"
done

# Explanation of key sections:
# $(head -n 1 "$file" | grep -c -P '#!\s*\K\S+'): Checks if the file has a shebang line using a regular expression. It counts the number of matches for lines starting with #! followed by optional spaces (\s*) and captures the interpreter (\K\S+).

# for i in "${!shebangs[@]}"; do ... done: Iterates through the indices of the shebangs array to check if the current shebang is already present.

# ((counts[$i]++)): Increments the count for the existing shebang.

# shebangs+=("$shebang") and counts+=(1): If the shebang is not found in the array, it adds the shebang to the shebangs array and initializes the count to 1.
