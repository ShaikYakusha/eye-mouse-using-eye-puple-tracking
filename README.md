
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

The main loop of the program continuously reads frames from the webcam, processes the frames to detect facial landmarks, and then maps the eye positions to screen coordinates. If a blink is detected, the application triggers a mouse click.

```python
import cv2
import mediapipe as mp
import pyautogui

# Initialize webcam and FaceMesh
cam = cv2.VideoCapture(0)
face_mesh = mp.solutions.face_mesh.FaceMesh(refine_landmarks=True)
screen_w, screen_h = pyautogui.size()

while True:
    _, frame = cam.read()
    frame = cv2.flip(frame, 1)
    rgb_frame = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)
    output = face_mesh.process(rgb_frame)
    landmark_points = output.multi_face_landmarks
    frame_h, frame_w, _ = frame.shape
    
    if landmark_points:
        landmarks = landmark_points[0].landmark
        
        # Track eye landmarks for mouse movement
        for id, landmark in enumerate(landmarks[474:478]):
            x = int(landmark.x * frame_w)
            y = int(landmark.y * frame_h)
            cv2.circle(frame, (x, y), 3, (0, 255, 0))
            
            if id == 1:
                screen_x = screen_w * landmark.x
                screen_y = screen_h * landmark.y
                pyautogui.moveTo(screen_x, screen_y)
        
        # Track landmarks for blink detection
        left = [landmarks[145], landmarks[159]]
        for landmark in left:
            x = int(landmark.x * frame_w)
            y = int(landmark.y * frame_h)
            cv2.circle(frame, (x, y), 3, (0, 255, 255))
        
        if (left[0].y - left[1].y) < 0.004:
            pyautogui.click()
            pyautogui.sleep(1)
    
    cv2.imshow('Eye Controlled Mouse', frame)
    cv2.waitKey(1)
Usage
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
