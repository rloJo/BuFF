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
             <img src="https://img.shields.io/badge/imgui-339AF0?style=for-the-badge&logo=imgui&logoColor=white" alt = "Visual Studio">
         </td>
    </tr>
    <tr>
        <td style="text-align: center"> Language </td>
        <td>   
    		  <img src="https://img.shields.io/badge/c-E34F26?style=for-the-badge&logo=c&logoColor=white"alt = "C"> 
             <img src="https://img.shields.io/badge/c++-00599C?style=for-the-badge&logo=c%2B%2B&logoColor=white" alt ="C++">
            <img src="https://img.shields.io/badge/cuda-3776AB?style=for-the-badge&logo=cuda&logoColor=white" alt = "cuda"> 
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
- C++로 작성된 변형 코드를 CUDA로 작성하여 실행속도 개선
- UI 수정 
