# BuFF
> NeRF를 활용한 변형체 볼륨 가시화  
> 프로젝트 기간 2023.03 ~ 2023.06  
> 프로젝트 인원 : 3명  

## 기술 스택
<table>
    <tr>
        <td style="text-align: center"> OS </td>
        <td>   
            <img src="https://img.shields.io/badge/window-FCC624?style=for-the-badge&logo=window&logoColor=black" alt = "Windows"> 
        </td>
    </tr>
    <tr>
         <td style="text-align: center"> Tool </td> 
         <td>  
             <img src="https://img.shields.io/badge/visualstudio-339AF0?style=for-the-badge&logo=visualstudio&logoColor=white" alt = "Visual Studio">
			 <img src="https://img.shields.io/badge/github-181717?style=for-the-badge&logo=github&logoColor=white" alt = "Github">
			 <img src="https://img.shields.io/badge/git-F05032?style=for-the-badge&logo=git&logoColor=white" alt = "Git">
         </td>
    </tr>
    <tr>
        <td style="text-align: center"> Language </td>
        <td>   
    		  <img src="https://img.shields.io/badge/c-E34F26?style=for-the-badge&logo=c&logoColor=white"alt = "C"> 
             <img src="https://img.shields.io/badge/c++-00599C?style=for-the-badge&logo=c%2B%2B&logoColor=white" alt = "C++">
            <img src="https://img.shields.io/badge/cuda-E34F26?style=for-the-badge&logo=cuda&logoColor=white" alt = "Cuda">
        </td>
    </tr>
</table>




## Description

VoxelFLEX는 4가지의 ngp(neural graphics primitives) 중 하나인 NeRF(Neural radiance fields)를 기반으로 학습된 3D 모델에 볼륨 렌더링 엔진을 추가하여, **실시간으로 모델을 직접 변형**시킬 수 있도록 한다.

지금까지 영상의학과 관련하여 시술 상담을 진행할 때, 시술 이전과 이후를 비교한 예상 결과를 보여주었는데, 이는 정적인 2D영상으로 결과를 제공하여 한정된 정보만 표현이 가능한 어려움을 지니고 있었다. BuFF는 이러한 한계를 극복하기 위해 2D영상을 NeRF를 통해 3D영상으로 변환하여, 이전보다 입체적이고 직관적인 시각 정보를 제공할 수 있도록 한다. 또한, 실시간으로 영상 데이터를 변형시킬 수 있어 시술 이전과 이후의 차이를 보다 구체적으로 전달하여 원활한 의사소통을 할 수 있도록 도와준다.

<table>
    <thead>
        <tr>
            <th style="text-align: center">Before</th>
        	<th style="text-align: center">After</th>
        </tr>
    </thead>
    <tbody>
    	<tr>
        	<th style="text-align: center"><img src="https://github.com/HSUProject/BuFF/blob/main/docs/assets_readme/Before02.jpg" alt="Before" height ="250" width ="250" /></th>
            <th style="text-align: center"><img src="https://github.com/HSUProject/BuFF/blob/main/docs/assets_readme/After02.jpg" alt="After" height ="250" width ="250" /></th>
        </tr>
    </tbody>
</table>



영상의학에서 사용되는 시술 상담은 단순한 예시일 뿐, BuFF는 동영상을 통해 대상을 촬영할 수 있는 모든 곳에 적용시킬 수 있는 확장성을 지니고 있다. 다음 그림과 같이 사람을 대상으로 하지 않은 인형을 촬영하여 표정을 변형시킬 수도 있다.

<table>
    <thead>
        <tr>
            <th style="text-align: center">Before</th>
        	<th style="text-align: center">After</th>
        </tr>
    </thead>
    <tbody>
    	<tr>
        	<th style="text-align: center"><img src="https://github.com/HSUProject/BuFF/blob/main/docs/assets_readme/Before01.jpg" alt="Before" height ="250" width ="250" /></th>
            <th style="text-align: center"><img src="https://github.com/HSUProject/BuFF/blob/main/docs/assets_readme/After01.jpg" alt="After" height ="250" width ="250" /></th>
        </tr>
    </tbody>
</table>


## 역할
---
- 변형체 변형 알고리즘 개발
	1. 실공간과 가상공간으로 공간을 분리하고 두 공간사이의 역변환을 통해 물체의 변형이 이루어 지도록 구현했습니다.
 	2. 사용자의 입력값을 받아 (마우스 클릭 좌표 및 이동 벡터 및 변형 세기, 변형 범위)를 입력 받고, 가상공간의 좌표를 변형시킨다. 이는 가시화시 해당 좌표에서 출력될 실공간의 좌표가 저장되는 것.
  	3. 가시화를 수행할 때 출력 영상은 가상공간에 존재하므로, 가상공간에 해당하는 각 지점에 대응하는 실공간의 좌표를 샘플링하여 변형된 변형체를 가시화 한다.

- Cuda 언어로 재작성하여 실행 속도 95% 향상
- Imgui를 활용한 UI 수정


## 트러블 슈팅
---
1. 가상공간과 실공간을 vec3의 3차원 배열로 생성시, 메모리 문제로 배열이 생성되지 않는 문제가 발생하였다.
	- 3차원 배열을 1차원으로 만들어서 해결.
	- 볼륨 데이터는 -1.5 ~ 2.5 의 각 길이 4 의 정육면체 형태로 나타난다.
	- 따라서 각 1 복셀을 256 개로 나누려면 각 복셀마다 1/(256/4)의 차이를 갖는다.
	- 일차원 배열로 나타내기 때문에 각 칸을 다 채우면 좌표 초기화에 유의해야한다.
	``` c++
   	// Volume Data 크기 정의 (클수록 화질 향상)
	constexpr int VOLX = 256; // width
	constexpr int VOLY = 256; // height
	constexpr int VOLZ = 256; // depth

	constexpr int VOL_SIZE = VOLX * VOLY * VOLZ;
	constexpr int VOL_SIZE_DIGIT = 64; // (256/4)

	// 볼륨 데이터 초기화 메소드
 	void generate_volume()
	{
	vec3 pos = { -1.5f, -1.5f, -1.5f };
	float step = 1.0f / VOL_SIZE_DIGIT;

	for (int z = 0; z < VOLZ; z++) {
		for (int y = 0; y < VOLY; y++) {
			for (int x = 0; x < VOLX; x++) {
				int idx = z * VOLX * VOLY + y * VOLX + x;
				h_vol[idx] = pos;
				h_vol_deform_area[idx].x = x;
				h_vol_deform_area[idx].y = y;
				h_vol_deform_area[idx].z = z;
				pos.x += step;
			}
			pos.x = -1.5f;
			pos.y += step;
		}
		pos.y = -1.5f;
		pos.z += step;
	}
   ```

2. 가상공간의 복셀 하나씩 순회하며 변형 범위인지 판단하고 변형을 가하는 것은 변형 범위 및 가상공간의 크가 커질수록 실행시간이 최대 413ms 까지 증가하여 사용자 경험을 방해하였다.
   - C++로 작성된 변형 코드를 CUDA로 작성하여 실행속도 개선
   - 변형 계산은 고도의 병렬성을 갖는다는 것을 파악 후, GPU Cuda Core를 이용해 변형 계산을 병렬적으로 수행
   - 실생속도 413ms => 20ms로 대폭 향상.
  ```c++
__global__ void generate_deformed_volume(
	const uint32_t vol_size,
	vec3* vol,
	vec3* vol_buf,
	DeformArea* vol_deform_area,
	vec3 epicenter, // 마우스를 클릭한 지점
	vec3 dir, // 마우스를 드래그해서 나온 벡터
	float force // 가중치 (사용가가 UI로 설정)
) {
	const uint32_t i = threadIdx.x + blockIdx.x * blockDim.x; // Cuda core는 번호로 쓰레드를 구별한다.
	if (i >= vol_size) return;

	if (!vol_deform_area[i].active) return; // 변형 공간 판단

	// 좌표를 인덱스로 변환
	vec3 pos = vec3(0.0f);
	pos.x = vol[i].x ;
	pos.y = vol[i].y ;
	pos.z = vol[i].z ;

	// 거리에 따라 가중치가 달라진다. 변형 중심으로 부터 좌표가 멀어질 수록 가중치가 세져 변형이 약해짐.
	int idx_x = vol_deform_area[i].x;
	int idx_y = vol_deform_area[i].y;
	int idx_z = vol_deform_area[i].z;
	
	int distance = abs(epicenter.x - idx_x) + abs(epicenter.y - idx_y) + abs(epicenter.z - idx_z); // 각 거리는 맨해튼 디스턴스로 계산
	float weight = pow(force, distance); // 변형세기는 사용자가 입력한 가중치를 밑으로 하고 거리의 크기 지수 만큼 값을 갖는다.

	// 가상공간의 좌표를 수정한다. 역변환을 하기 때문에 벡터 * 가중치 만큼 원래 좌표에서 빼줘야 한다.
	vol_buf[i].x = pos.x - dir.x * weight;
	vol_buf[i].y = pos.y - dir.y * weight;
	vol_buf[i].z = pos.z - dir.z * weight;
}


 ```

## 프로젝트 빌드하는 법
> <a href = "https://github.com/rloJo/BuFF/tree/main/docs"> 빌드하는 법 </a>
