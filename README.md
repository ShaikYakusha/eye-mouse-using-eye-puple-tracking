
# eye-mouse-using-eye-puple-tracking
# Eye-Controlled Mouse

This is a Python application that uses computer vision and machine learning to allow users to control their mouse pointer with their eyes. The application leverages OpenCV, MediaPipe, and PyAutoGUI to track facial landmarks, particularly focusing on the eyes, to move the mouse pointer and perform clicks.

## Features

- **Eye Tracking**: Detects and tracks eye movement in real-time using a webcam.
- **Mouse Control**: Moves the mouse pointer according to the position of the eyes.
- **Blink Detection**: Performs a mouse click when the user blinks.

## Requirements

To run this project, you need to have Python installed along with the following libraries:

- OpenCV: `pip install opencv-python`
- MediaPipe: `pip install mediapipe`
- PyAutoGUI: `pip install pyautogui`

## How It Works

1. **Face Mesh Detection**: The application uses MediaPipe's FaceMesh to detect and track facial landmarks in real-time.
2. **Eye Landmark Extraction**: Specific landmarks around the eyes are used to calculate the position and movement of the eyes.
3. **Mouse Movement**: The position of the eyes is mapped to the screen coordinates, allowing the mouse pointer to follow the user's eye movement.
4. **Blink Detection**: The vertical distance between two specific eye landmarks is used to detect blinks. If a blink is detected, a mouse click is simulated.



## Code Explanation

Clone this repository to your local machine.
Install the required Python packages.
Run the Python script using the command:
bash
Copy code
python eye_controlled_mouse.py
Make sure your webcam is working and positioned properly.
Move your eyes to control the mouse pointer on the screen. Blink to perform a click.
Notes
Accuracy: The performance of this application may vary depending on the quality of your webcam and the lighting conditions.
Delay: There may be a slight delay in mouse movement and blink detection due to processing time.
Contributing
Feel free to fork this repository, make improvements, and submit pull requests.
