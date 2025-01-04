- 3D 오브젝트 
	- 감마, 그림자와 또 그림자
		- Ground shadow, Ambient Occlusion 
	- 광원 추정
	- Camera Grain
	- World Tracking
	- Raycast 
	- Scene Reconstruction
	- Scene Reconstruction
		- mesh를 통해 수행 가능한 기능 
			- 실제 표면
	- 자연스러운 섬세한 배치
	- ToF 기술이 들어간 센서를 가지고 있는 기기에 한하여 Scene Reconstruction 기능 사용
		- 이동간의 고도 차이를 계산
		- 실시간으로 Raycast 
	- 진짜 같은 배치 - People / Object Occlusion
		- object Occlusion : 실제 환경의 사물을 통해 가상의 오브젝트를 가리는 기능
		- ![[Pasted image 20250104180432.png]]
### 겪었던 문제 ??
- 높은 배터리 사용량
- 발열의 불쾌감, 성능 저하
- 메인 콘텐츠로 한 시간 이상 사용 가능?
- 서로 다른 모바일 환경 및 AR SDK 차이
- 시간 경과에 따른 상태 측정

![[Pasted image 20250104180908.png]]

- 랜더링 최적화
	- 3D 모델 데이터 구조
		- 메타 정보(.gltf)
		- 지오메트리 및 애니메이션(.bin)
		- 텍스처(png, jpg)
	- 지오메트리(메쉬) 및 애니메이션 압축
		- 모델의 원본 형태는 최대한 유지하면서 폴리곤의 갯수를 줄임 
		- Draco : mesh/point cloud compression
		- Meshoptimizer : bin 전체 압축, gpu 전체 압축, gpu 
	- 텍스처 압축 
		- KTX2/basis
		- GPU 압축 픽셀 형식으로 transcode
		- 더 작은 파일 크기, 더 작은 GPU/메모리 사용