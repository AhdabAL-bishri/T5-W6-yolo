https://drive.google.com/file/d/1smNIjyzRRMLGClq7h-uscYRWCGiykicf/view?usp=share_link

الكود قبل التديل 
import cv2
import numpy as np

TOP_cont = 0
BOUTTOM_cont = 0
RITHT_cont = 0
LEFT_cont = 0

while video.isOpened():
    ret, frame = video.read()
    if not ret:
        break

    results = model.predict(frame)

    for detection in results[0]:
        class_id = detection.boxes.cls.cpu().numpy().astype(int)
        cinfidence = detection.boxes.conf.cpu().numpy()
        xyxy = detection.boxes.xyxy.cpu().numpy()

        for i in range(len(class_id)):
            x1, y1, x2, y2 = map(int, xyxy[i])
            x = x1
            y = y1
            w = x2 - x1
            h = y2 - y1
            object_id = i
            X_center = int(x + w / 2)
            Y_center = int(y + h / 2)

            cv2.rectangle(frame, (x, y), (x + w, y + h),coloe2, 2)

            cv2.circle(frame, (X_center, Y_center), 5, coloe2, -1)

            cv2.putText(frame, f'ID: {object_id} Class: {class_id[i]} Conf: {cinfidence[i]:.2f}',
                (x, y - 10), cv2.FONT_HERSHEY_SIMPLEX, 0.5,coloe2, 2)
            if TOP[1] <= Y_center <= TOP[3] and TOP[0] <= X_center <= TOP[2]:
                TOP_cont += 1
            elif BOUTTOM[1] <= Y_center <= BOUTTOM[3] and BOUTTOM[0] <= X_center     <= BOUTTOM[2]:
                BOUTTOM_cont += 1
            elif RITHT[1] <= Y_center <= RITHT[3] and RITHT[0] <= X_center <= RITHT[2]:
                RITHT_cont += 1
            elif LEFT[1] <= Y_center <= LEFT[3] and LEFT[0] <= X_center <= LEFT[2]:
                LEFT_cont += 1

            cv2.rectangle(frame, (TOP[0], TOP[1]), (TOP[2], TOP[3]), (0, 0, 255), 2)
            cv2.rectangle(frame, (BOUTTOM[0], BOUTTOM[1]), (BOUTTOM[2], BOUTTOM[3]), (0, 0, 255), 2)
            cv2.rectangle(frame, (RITHT[0], RITHT[1]), (RITHT[2], RITHT[3]), (0, 0, 255), 2)
            cv2.rectangle(frame, (LEFT[0], LEFT[1]), (LEFT[2], LEFT[3]), (0, 0, 255), 2)

            cv2.putText(frame, 'Ahdab Albishri', (10, 30), cv2.FONT_HERSHEY_SIMPLEX, 1, coloe1, 2)

            cv2.putText(frame, f'Top: {TOP_cont}', (10, 60), cv2.FONT_HERSHEY_SIMPLEX, 0.7, coloe4, 2)
            cv2.putText(frame, f'Bottom: {BOUTTOM_cont}', (10, 90), cv2.FONT_HERSHEY_SIMPLEX, 0.7, coloe4, 2)
            cv2.putText(frame, f'Right: {RITHT_cont}', (10, 120), cv2.FONT_HERSHEY_SIMPLEX, 0.7, coloe4, 2)
            cv2.putText(frame, f'Left: {LEFT_cont}', (10, 150), cv2.FONT_HERSHEY_SIMPLEX, 0.7, coloe4, 2)

    outPut.write(frame)

video.release()
outPut.release()
print(f"Video saved to {outPut_video}")
 الفديو
 https://drive.google.com/file/d/1Fdmeut5t0vXdddHl4XsjbXQ0nvJql3yx/view?usp=share_link
 
