#!/bin/bash
#   termwide prompt with tty number
#      by Giles - created 2 November 98, last tweaked 31 July 2001
#
#     This is a variant on "termwide" that incorporates the tty number.
#

hostnam=$(hostname -s)
usernam=$(whoami)
temp="$(tty)"
#   Chop off the first five chars of tty (ie /dev/):
cur_tty="${temp:5}"
unset temp

function prompt_command {

#   Find the width of the prompt:
TERMWIDTH=${COLUMNS}

#   Add all the accessories below ...
local temp="--(${usernam}@${hostnam}:${cur_tty})---(${PWD})-"

let fillsize=${TERMWIDTH}-${#temp}
if [ "$fillsize" -gt "0" ]
then
	
fill="-------------------------------------------------------------------------------------------------------------------------------------------"
	#   It's theoretically possible someone could need more 
	#   dashes than above, but very unlikely!  HOWTO users, 
	#   the above should be ONE LINE, it may not cut and
	#   paste properly
	fill="${fill:0:${fillsize}}"
	newPWD="${PWD}"
fi

if [ "$fillsize" -lt "0" ]
then
	fill=""
	let cut=3-${fillsize}
	newPWD="...${PWD:${cut}}"
fi
}

PROMPT_COMMAND=prompt_command

function twtty {

local WHITE="\[\033[0;37m\]"
local NO_COLOUR="\[\033[0m\]"
local RED="\[\033[01;31m\]"
local GREEN="\[\033[01;32m\]"
local LIGHT_BLUE="\[\033[1;34m\]"
local YELLOW="\[\033[1;30m\]"

case $TERM in
    xterm*|rxvt*)
        TITLEBAR='\[\033]0;\u@\h:\w\007\]'
        ;;
    *)
        TITLEBAR=""
        ;;
esac

PS1="$TITLEBAR\
$YELLOW-$LIGHT_BLUE-(\
$YELLOW\$usernam$LIGHT_BLUE@$YELLOW\$hostnam$LIGHT_BLUE:$WHITE\$cur_tty\
${LIGHT_BLUE})-${YELLOW}-\${fill}${LIGHT_BLUE}-(\
$YELLOW\${newPWD}\
$LIGHT_BLUE)-$YELLOW-$LIGHT_BLUE-(\
$WHITE\$(date +%H:%M:%S)$LIGHT_BLUE)-$YELLOW--\
\$(__git_ps1 '$LIGHT_BLUE-($RED%s$LIGHT_BLUE)')-$YELLOW--\
$LIGHT_BLUE-($GREEN\$(rvm current)$LIGHT_BLUE)\
\n\
$NO_COLOUR$ " 

PS2="$LIGHT_BLUE-$YELLOW-$YELLOW-$NO_COLOUR "

}

twtty

