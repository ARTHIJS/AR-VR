import cv2
import numpy as np

# Load the marker image
marker_image = cv2.imread('marker.jpg')
marker_size = (100, 100)  # Size of the marker image

# Initialize the camera
cap = cv2.VideoCapture(0)

while True:
    ret, frame = cap.read()
    if not ret:
        break

    # Detect the marker in the camera feed
    gray_frame = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
    aruco_dict = cv2.aruco.Dictionary_get(cv2.aruco.DICT_6X6_250)
    parameters = cv2.aruco.DetectorParameters_create()
    corners, ids, _ = cv2.aruco.detectMarkers(gray_frame, aruco_dict, parameters=parameters)

    if ids is not None:
        # Draw the marker outline and ID on the frame
        cv2.aruco.drawDetectedMarkers(frame, 
