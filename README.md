1번
문제
* OpenCV를 사용하여 이미지를 불러오고 화면에 출력할 것.
* 원본 이미지와 그레이스케일로 변환된 이미지를 나란히 표현할 것.

원리
1. cv.imread('(파일명)')을 통해서 이미지 파일을 불러 읽도록 한다.
2. 이미지 출력이 제대로 나오도록 cv.resize를 통해서 이미지 크기를 조절한다.
3. 만약 파일이 없을 경우, sys.exit을 통해서 파일이 존재하지 않음을 알리고 종료한다.
4. 불러온 이미지가 있다면, 그 이미지를 가지고 cv.cvtColor(img, cv.COLOR_BGR2GRAY) 을 통해서 그레이스케일 이미지를 생성한다.
5. 생성한 그레이스케일 이미지를 원본 이미지와 나란히 표현하기 위해서는 두 이미지의 형식을 같게 해야한다.
   -> 그러므로, cv.cvtColor(gray, cv.COLOR_GRAY2BGR) 을 통해서 그레이스케일 이미지를 BGR형식으로 변환한다.
6. frames 리스트를 생성하여 두 이미지를 frames 에 추가한다.
7. 그리고, np.hstack을 통해서 두 이미지를 결합하고, imshow를 통해서 이미지를 나란히 표현할 수 있도록 한다.

2번
문제
* 웹캠을 사용하여 실시간 비디오 스트림을 가져온다.
* 각 프레임에서 Canny Edge Dectection을 적용하여 에지를 검출하여 원본 영상과 나란히 출력한다.
* q 키를 눌러서 윈도우 창을 종료할 수 있도록 한다.
  
원리
1. cv.VideoCapture을 통해서 웹캠 연결을 시도하고, CAP_DSHOW를 통해 비디오가 화면에 바로 출력될 수 있도록한다.
2. cap.read()로 프레임 읽기 여부와 프레임 자체를 변수에 저장하고, 만약 ret가 not이라면 프레임 획득 실패로 판단하고 종료한다.
3. 프레임 획득에 성공했을 경우에는 먼저, cv.Canny를 통해서 Canny Edge Detection을 적용하여 에지를 검출한다.
4. cv.cvtColor를 통해서 검출한 에지와 원본 프레임의 BGR 형식과 같은 형식으로 읽을 수 있도록 한다.
5. np.hstack을 통해서 검출한 에지와 원본 영상을 결합하여 imshow를 통해서 영상을 나란히 표현할 수 있도록 한다.
6. 만약 q 키를 눌렀을 경우 종료하게 만들어야 하므로 cv.waitKey(1)로 키 입력을 받도록 하고, ord('q')로 입력받은 키가 q인지 확인할 수 있도록 한다.
7. cap.release()로 카메라 연결을 해제한다.
8. 다음으로, cv.destroyAllWindows()를 통해 왼도우창을 종료한다.

3번
문제
* 이미지를 불러오고 사용자가 마우스를 클릭하고 드래그하여 관심영역(ROI)을 선택할 수 있도록 함.
* 선택한 영역만 따로 저장하거나 표시할 수 있도록 한다.
* r 키로 관심영역을 초기화하여 이미지를 다시 불러오도록 한다.
* s 키로 관심영역을 저장할 수 있도록 한다.
* q 키로 모든 윈도우 창을 종료할 수 있도록 한다.

원리
1. 원본 이미지를 불러오고 출력하는 원리는 1번 문제의 원리와 동일하다.
2. cv.setMouseCallback을 통해 마우스 이벤트를 처리할 수 있도록 한다.
3. cv.EVENT_LBUTTONDOWN으로 마우스 오른쪽 클릭 중임을 확인하고, cv.EVENT_LBUTTONUP으로 마우스 오른쪽 클릭이 끝났음(드래그를 끝냈음)을 확인한다.
4. 마우스 오른쪽을 클릭 했다면, 클릭한 이미지의 좌표를 저정하고, 마우스 클릭이 끝났다면(드래그를 끝냈다면) cv.rectangle을 통해서 클릭을 시작한 좌표와 클릭이 끝난 좌표를 이용해서 관심영역을 표시할 수 있도록 하고,
   그 영역을 roi에 저장하여 imshow로 그 영역을 윈도우 창으로 출력한다.
5. 키를 입력받는 원리는 2번의 원리에서 언급한 것과 동일하다.
6. r 키를 입력받은 경우에는 우선 destroyAllWindows()를 통해서 모든 윈도우 창을 종료하고 다시 imshow를 통해서 원본 이미지를 출력할 수 있도록 한다.
7. s 키를 입력받은 경우에는 imwrite('(파일명)', (관심영역)) 을 통해 관심영역을 이미지로 저장할 수 있도록 한다.
   
