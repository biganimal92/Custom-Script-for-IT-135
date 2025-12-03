# Custom-Script-for-IT-135
## This script is designed to organize files into separate folders based on their extensions and types.
#!/bin/bash

# Define the directory to organize. Default to the current directory.
DIR=${1:-.}

# Define file type extensions and their corresponding folder names.
declare -A FILE_TYPES=(
    [jpg]="Images" [jpeg]="Images" [png]="Images" [gif]="Images" [webp]="Images" [bmp]="Images" [svg]="Images"
    [pdf]="Documents" [doc]="Documents" [docx]="Documents" [txt]="Documents" [md]="Documents" [rtf]="Documents" [odt]="Documents" [xls]="Documents" [xlsx]="Documents" [ppt]="Documents" [pptx]="Documents"
    [zip]="Archives" [tar]="Archives" [gz]="Archives" [bz2]="Archives" [xz]="Archives" [7z]="Archives" [rar]="Archives"
    [mp3]="Audio" [wav]="Audio" [ogg]="Audio" [flac]="Audio" [m4a]="Audio"
    [mp4]="Video" [mkv]="Video" [mov]="Video" [webm]="Video" [avi]="Video"
    [sh]="Scripts" [py]="Scripts" [js]="Scripts" [ts]="Scripts" [html]="Scripts" [css]="Scripts" [json]="Scripts" [yml]="Scripts" [yaml]="Scripts" [c]="Scripts" [cpp]="Scripts" [java]="Scripts" [go]="Scripts" [rb]="Scripts" [php]="Scripts"
)

# Create folders and move files into them based on their extensions.
for file in "$DIR"/*; do
    if [[ -f "$file" ]]; then
        filename=$(basename "$file")
        extension="${filename##*.}"
        if [[ "$filename" == "$extension" ]]; then # No extension found
            folder_name="Others"
        else
            folder_name="${FILE_TYPES[${extension,,}]}" # Convert extension to lowercase
            if [[ -z "$folder_name" ]]; then # If extension not in FILE_TYPES
                folder_name="Others"
            fi
        fi
        
        mkdir -p "$DIR/$folder_name"
        mv "$file" "$DIR/$folder_name/"
        echo "Moved $filename to $folder_name/"
    fi
done

echo "File organization completed."
## 🤝 Attribution and Professional Disclosure

### Base Repository/Code Reference

This project was based on initial concepts and structures derived from the "Linux Text Processing Tools" module at North Seattle College (IT135).

### AI/Chatbot Assistance Policy

In line with academic integrity and modern development practices, I utilized Google's AI summaries when aggregating the following:

1.  **Proper Syntax** Google's AI helped in assisting me with finding the correct syntax for this organization script.
2.  **Code Review:** Verifying best practices for shell variable usage and quoting.
3.  **Documentation Drafting:** Structuring and refining the language used in this `README.md` and the initial project overview.

No copyrighted code was used, and the final script logic was engineered and tested independently.

-----

## 👤 Author

  * **Lindsey Powell**
  * **powell_ld@outlook.com**
