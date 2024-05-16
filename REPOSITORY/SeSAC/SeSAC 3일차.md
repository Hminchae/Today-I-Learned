#SeSAC #강의노트 #iOS 

### 복습

- Asset 에서 사진이 1배수 하나만 차있으면 어떻게 될까? -> 그 하나로 비어있는 배수를 채우게 됨
- JPG PNG <-권장! jPEG  대 SVG
	- JPG PNG <-권장! jPEG : 비트맵
	- SVG : 벡터 이미지 
		- SVG 일 때 Preserve Vector Data <- 이 체크박스가 비어있으면 벡터로 다뤄지지 않음
		- PDF와 비슷
	- 1배수, 2배수 관리가 필요 없는 경우엔 그룹에 직접 추가하여도 됨
- Xcode -> Build Phases
	- Copy Bundle Resource 에 내가 추가한 이미지와 에셋이 추가됨. 
	- 만약 파일 추가할 때 target 추가 하지 않으면 나중에 여기에 다시 와서 추가해주어야 하기 때문에 귀찮아짐
	- 만약 지울 때!
		- Move to Trash
		- Remove Reference : Xcode 상에서만 사라지고..파일엔 아직 살아있어서 추후 문제가 생길 수 있음

