import cv2
cap = cv2.VideoCapture('"D:\New folder\video.mp4"')
vehicle_cascade = cv2.CascadeClassifier(cv2.data.haarcascades + 'haarcascade_car.xml')


count = 0
prev_count = 0

while True:
    
    ret, frame = cap.read()
    if not ret:
        break
    
    
    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
    
   
    vehicles = vehicle_cascade.detectMultiScale(gray, 1.1, 5)
    
    
    for (x, y, w, h) in vehicles:
        cv2.rectangle(frame, (x, y), (x+w, y+h), (0, 255, 0), 2)
    
    
    cv2.imshow('Frame', frame)
    
    
    count = len(vehicles)
    
   
    if count != prev_count:
        print(f"Vehicle count: {count}")
        prev_count = count
    
   
    if cv2.waitKey(1) & 0xFF == 27:
        break

# Release the video capture object and close all windows
cap.release()
cv2.destroyAllWindows()
