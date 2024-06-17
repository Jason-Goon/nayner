#!/bin/bash

# Function to generate a random delay between clicks
generate_random_delay() {
  # Generate a random number between 50 and 200 milliseconds
  delay_ms=$(shuf -i 50-200 -n 1)
  # Convert milliseconds to seconds
  delay=$(awk -v ms=$delay_ms 'BEGIN {print ms / 1000}')
  echo "$delay"
}

# Function to generate a random break time
generate_random_break() {
  # Generate a random number between 5 and 20 seconds
  break_seconds=$(shuf -i 5-20 -n 1)
  echo "$break_seconds"
}

# Function to move the cursor to the center of the screen
move_cursor_to_center() {
  screen_width=$(xdotool getdisplaygeometry | awk '{print $1}')
  screen_height=$(xdotool getdisplaygeometry | awk '{print $2}')
  center_x=$((screen_width / 2))
  center_y=$((screen_height / 2))
  xdotool mousemove $center_x $center_y
}

# Variables to control break time
break_interval=1800  # 30 minutes in seconds
next_break=$(date +%s -d "$break_interval seconds")

# Main loop to perform autoclicking
while true; do
  # Check if it's time for a break
  current_time=$(date +%s)
  if [ $current_time -ge $next_break ]; then
    # Generate a random break time
    break_time=$(generate_random_break)
    echo "Taking a break for $break_time seconds"
    sleep $break_time
    # Schedule the next break
    next_break=$(date +%s -d "$break_interval seconds")
  fi

  # Move cursor to the center of the screen
  move_cursor_to_center

  # Simulate a left mouse button click
  xdotool click 1

  # Generate a random delay
  delay=$(generate_random_delay)

  # Sleep for the random delay
  sleep $delay
done
