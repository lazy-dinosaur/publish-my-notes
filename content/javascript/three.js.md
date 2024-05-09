---
id: three.js
aliases: []
tags: []
date: "2024-05-08"
description: ""
draft: false
---

#three-js #web-gl #javascript 

>[!summary]
>Three.js 는 웹에 3D 경험을 창조할 수 있도록 하는 자바스크립트 라이브러리 이다.

three js 를 사용하기 위해서는 기본적으로 4가지 요소가 필요하다
- Scene
- Objects
- Camera
- Renderer

## Scene

객체와 모델들과 입자들, 그리고 빛 등등을 담기 위한 container 의성격

*Scene* class 을 실행시켜 주어야 한다.

```js
const scene = new THREE.Scene();
```

>[! caution] 주의
>three.js 의 Naming Convention 은 Pascal Case 를 따른다.



## Objects

원시적인 geometries 나 모델들 혹은 입자 혹은 광원 등을 뜻한다. 즉 *Scene* 에 오브젝트를 불러와 담는다.
### object 의 변형

모든 객체는 다음의 속성을 변화시켜 변형시킬 수 있다.
1. 위치(position)
2. 회전(rotation)
3. 비율(scale) 
4. 사원수(quaternion)

>[! caution] 주의
>mesh 등의 객체를  생성한 이후에 scene 에 추가해 주어야 렌더링을 하게 된다.
>하지만 객체의 크기나 위치 같은 값을 scene 에 추가한 이후에 업데이트 한다면 업데이트한 값은 적용되지 않는다.
>업데이트 이후 수정된 객체를 다시한번 scene 에 넣어 주어야 한다. 


`posiiton` 의 값은 *Vector3* 에서 상속된 값이다.


Scene 을 렌더링 할때 이론적인 시각 (point of view)
다양한 카메라를 사용할 수 있지만 일반적으로 하나만 사용한다.
가장 기본적으로는 PerspectiveCamera 클래스를 활용한다.

### PerspectiveCamera
해당 클래스에는 두가지 중요하고 필수적인 매개변수가 있다.
1. 시야(field of view)
   보게 되는 각도를 설정하는것 수직을 기준으로 표현된다.
2. 종횡비(aspect ratio)
   종축 대비 횡축의 길이
   
### AxesHelper
물체를 아무 것도 없는 곳에 덩그러니 놓으면 위치를 잡기 쉽지 않다.
중간에서 얼마나 멀리 떨어져 있는지 혹시 위가 아래이고 아래가 위는 아닌지 등등 아무것도 없는 빈 공간에서 물체를 조작하기란 쉽지 않다.
`AxesHelper` 를 활용하면 위치를 잡는데에 도움을 줄 수 있다.
공간 안의 중심으로 부터 x,y,z 축이 다른 색상으로 나타나게 된다.

```js
const axesHelper = new THREE.AxesHelper();
scene.add(axesHelper);
```
scene 에 동일하게 넣어 주어야 한다.
### Rotate Object

물체를 회전시키는 방법은 두가지가 존재한다.
1. `rotation`
2. `quaternion`
우선 중요하게 알아 두어야 할 것은 둘중 아무거나 활용해도 같은 결과를 가질 수 있으며 하나를 수정하면 자동적으로 다른 값도 변경된다는 것이다.

일반 rotation의 경우 물체에 축에 해당하는 막대기가 나와있다고 생각하고 조정하면 된다.
매우 쉬운 방식 이지만 실제로 사용하면서 많은 문제가 발생하게 된다.

quaternion 의 경우 훨씬 복잡한 수학으로 이루어져 있다.
하지만 많은 문제들이 해결된다. 

quaternion 은 상상하기가 여렵다.



## Renderer

렌더러는 카메라의 시각으로 부터 장면을 렌더링 해준다.
결과물은 canvas 를 통해 나타난다.

수동으로 canvas . 를만들어 주거나 렌더러를 통해 생성하여 페이지에 추가할 수 있다.

>[! attention] 주의
>초기 카메라와 객체의 위치는 둘다 0,0,0 으로 센터에 위치해 있다.




