import cv2

def open_usb_camera(camera_index):
    # Open a connection to the USB camera
    cap = cv2.VideoCapture(camera_index)

    # Check if the camera is opened successfully
    if not cap.isOpened():
        print("Error: Could not open USB camera.")
        return

    # Load the pre-trained Haarcascades classifier for face detection
    face_cascade = cv2.CascadeClassifier(cv2.data.haarcascades + 'haarcascade_frontalface_default.xml')

    # Set the video window size (optional)
    # cap.set(cv2.CAP_PROP_FRAME_WIDTH, 640)
    # cap.set(cv2.CAP_PROP_FRAME_HEIGHT, 480)

    # Read and display frames from the camera
    while True:
        ret, frame = cap.read()

        # Break the loop if there's an issue reading the frame
        if not ret:
            print("Error: Could not read frame.")
            break

        # Convert the frame to grayscale for face detection
        gray_frame = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)

        # Perform face detection
        faces = face_cascade.detectMultiScale(gray_frame, scaleFactor=1.3, minNeighbors=5)

        # Draw green rectangles around the detected faces
        for (x, y, w, h) in faces:
            cv2.rectangle(frame, (x, y), (x+w, y+h), (0, 255, 0), 2)

        # Display the frame with face detection
        cv2.imshow('USB Camera with Face Detection', frame)

        # Check for key press events
        key = cv2.waitKey(1) & 0xFF

        # Break the loop when 'q' key is pressed
        if key == ord('q'):
            break
        # Capture an image when 'c' key is pressed
        elif key == ord('c'):
            capture_image(frame)

    # Release the camera and close the window
    cap.release()
    cv2.destroyAllWindows()

def capture_image(frame):
    # Save the captured image
    cv2.imwrite('captured_image.jpg', frame)
    print("Image captured!")

# Change the camera_index parameter if you have multiple cameras
open_usb_camera(camera_index=1)
