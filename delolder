#!/bin/bash

v=0
d=0
days=""
dirs=()

while [ $# -gt 0 ]; do
    case "$1" in
        -v)
            v=1
            shift
            ;;
        -d)
            d=1
            shift
            ;;
        --)
            shift
            dirs+=("$@")
            break
            ;;
        -*)
            echo "Error: bad option $1" >&2
            exit 1
            ;;
        *)
            if [ -z "$days" ]; then
                days="$1"
            else
                dirs+=("$1")
            fi
            shift
            ;;
    esac
done

if [ -z "$days" ] || [ ${#dirs[@]} -eq 0 ]; then
    echo "Use: delolder [-v|-d] N [--] dir1 dir2..." >&2
    exit 1
fi

for dir in "${dirs[@]}"; do
    if [ ! -d "$dir" ]; then
        echo "Skip $dir - not dir" >&2
        continue
    fi

    if [ $d -eq 1 ]; then
        find "$dir" -type f -mtime "+$days"
    elif [ $v -eq 1 ]; then
        find "$dir" -type f -mtime "+$days" -print -delete
    fi
done

exit 0
