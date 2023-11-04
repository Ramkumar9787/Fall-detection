# Fall-detection
Detect people falling in a video
This Python code is designed to detect falls in a video stream and send a notification to a Telegram bot when a fall is detected. It uses OpenCV (cv2) for video processing and Telepot for Telegram bot communication. Let's break down the code step by step:

1. Import necessary libraries:
   - `cv2`: OpenCV library for computer vision tasks.
   - `numpy`: Library for numerical and array operations.
   - `cv2_imshow`: A custom function for displaying images in Google Colab.
   - `telepot`: A Python library for interacting with the Telegram Bot API.

2. Initialize the Telegram bot:
   - To use the code, you need to create a Telegram bot and obtain its API token. You should replace `'your Telegram bot API token'` with the actual token for your bot.

3. Create a VideoCapture object:
   - It initializes a connection to a video source. In this case, the video source is a video file named `'fall6.mp4'`. You can change the video source to use a webcam or another video file.

4. Initialize variables for fall detection:
   - `frame_count`: A counter to keep track of the current frame being processed.
   - `prev_frame`: A variable to store the previous frame for motion comparison.
   - `motion_threshold`: A threshold value used to determine when motion is considered a fall.(Change value for accuracy relative to video speed rate.)

5. Main processing loop:
   - The code enters a `while` loop that continuously processes video frames until there are no more frames to process.

6. Capture a frame:
   - The `cap.read()` method captures the next frame from the video source.

7. Process the frame:
   - Convert the frame to grayscale (`gray`) and apply a Gaussian blur to reduce noise.
   - If `prev_frame` is `None`, it assigns the current `gray` frame to `prev_frame` and continues to the next iteration.
   - Calculate the absolute difference between the previous frame and the current frame to detect motion.
   - Apply a threshold to the difference frame to create a binary image where motion is highlighted.
   - Dilate the thresholded image to enhance motion regions.
   - Find contours in the thresholded image.

8. Motion detection:
   - Iterate through the detected contours and check if the area of each contour is greater than the `motion_threshold`. If so, set `motion_detected` to `True`.

9. Fall detection:
   - If `motion_detected` is `True`, a fall is detected. The frame where the fall occurred is saved as an image with a filename containing the frame count.

10. Display the frame:
   - The `cv2_imshow` function is used to display the frame where the fall is detected.

11. Send a Telegram notification:
   - The code sends the detected frame as a photo to a specific chat or user with the Telegram bot. The frame is sent with a caption indicating the frame number where the fall was detected.

12. Update the `prev_frame`:
   - Set `prev_frame` to the current `gray` frame for comparison in the next iteration.

13. Release video capture and close windows:
   - After processing all frames, release the VideoCapture object and close any open OpenCV windows.

In summary, this code continuously analyzes video frames, looking for motion that exceeds a specified threshold. When a fall is detected, it saves the frame and sends it to a Telegram chat using a Telegram bot. This code can be used for fall detection and notification in various applications, such as surveillance and eldercare.
