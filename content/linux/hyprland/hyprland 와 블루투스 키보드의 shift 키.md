---
id: hyprland 와 shift 키
aliases:
  - 문제의 발생
  - 문제 설명
  - 문제의 원인
  - 해결 방법
tags:
  - hyprland
  - linux
  - fcitx5
  - zmk
date: "2024-05-08"
description: ""
draft: false
---
# 문제의 발생

>[!bug]
> 닫는 괄호를 입력할 때 왜 숫자 0 이 입력되는거야??

linux 와 hyprland를 잘 세팅하고 사용하고 있는 와중, 멀쩡하던 블루투스 키보드의 입력에 문제가 발생하기 시작했다.

다른 일반적인 키보드를 사용할 때에는 느끼지 못했지만 [zmk](https://zmk.dev/) 로 설정된 블루투스 키보드에서 [콤보 기능]( https://zmk.dev/docs/features/combos ) 과 [Capsword 기능](https://zmk.dev/docs/behaviors/caps-word)을 사용하면서 문제가 발생했다.

>[!note] Combo 와 Capsword
>
> - Combo : 두개 이상의 키를 동시에 눌러서 다른 키를 입력하는 기능
> - Capsword : 하나의 모드로서 동작하며 켜져 있을때는 Shift 가 지속적으로 눌려 Capslock 과 같은 기능을 하지만 설정되지 않은 키를 누를때는 모드가 풀리며 기본 키보드 설정으로 돌아와 동작한다.

## 문제가 발생한 키보드의 키맵

[내 설정](https://github.com/DevToBeLazy/zmk-config-corne-cirque)

지금 사용하고 있는 키맵은  [urob 유저의 설정](https://github.com/urob/zmk-config) 을 기반으로 변형된 세팅을 사용하고 있는 중이다. 이 키맵의 특징은 Home Row 와 Combo 키를 매우 공격적으로 사용한다는 것이다 
 ![urob-config]( https://github.com/urob/zmk-config/blob/main/img/keymap.png?raw=true )
출처: [urob/zmk-config](https://github.com/urob/zmk-config?tab=readme-ov-file)


# 문제 설명

1. 콤보키중 `'(',')'` 키를 입력할 때 `0,9`, 가 입력된다.
2. CapsWord를 사용할 때 특정 키들이 대문자로 나타나지 않는다. 

최근 키보드의 설정을 수정했기 때문에 혹시 키보드에 문제가 있는것인가 싶어 여러가지 설정값들을 수정해 보았지만 해결되지 않았다.

키보드의 문제가 아니라고 판단하고  OS 별로 테스트 해 보자 다음과 같은 결과가 나왔다. 

1. Windows : 문제 없음
2. MacOS : 문제 없음
3. Linux : Hyprland 사용시 문제 발생
 
Linux 에서만 문제가 발생하였고 gnome 과 kde plasma 등 다른 데스크탑 환경에서도 테스트를 해보았지만 **Hyprland** 에서만 문제가 발생하였다    

# 문제의 원인

Linux 와 Hyprland 조합을 사용할 때에만 발생하는 문제이기 때문에
Hyprland 과 관련된 환경 설정 혹은 사용중인 입력 방식인 `fcitx` 둘 중 하나가 문제일 수 있다.

## 환경 변수의 문제인가?

Hyprland 의 설정이 제대로 되지 않았다면 fcitx 가 동작하지 않을것이고 한영 전환이 되지 않아야 한다. 하지만 fcitx 는 정상적으로 동작하고 있기 때문에 환경 변수의 문제는 아닌것으로 보인다.

## Fcitx 의 문제인가?

이후 `wev` 라이브러리 를 활용하여`'('` 키의 입력을 테스트 해 보았다 

### zmk 의 콤보 기능을 사용하여 '(' 키를 입력한 결과

![[wev-input-check.png]]

### 일반 키보드를 사용하여 '(' 키를 입력한 결과

![[wev-input-check2.png]]
위의 두가지의 경우를 비교해보면 키의 입력 프로세스가 다르게 동작하는것을 확인할 수 있다. 

일반적인 키보드를 사용할때의 프로세스는 다음과 같다.
1. shift 키가 눌린다.
2. '(' 키가 눌린다.
3. '(' 키가 떼어진다.
4. shift 키가 떼어진다. 

하지만 zmk 의 콤보 기능을 사용할때의 프로세스는 3 번과 4번과정의 순서가 바뀌어 있다.
즉 shift 키가 떼어진 후에 '(' 키가 떼어지면서 해당 값이 숫자 9 로 입력이 된다.  

리눅스의 다른 데스크탑 환경에서도 동일한 프로세스로 동작하지만 Hyprland 에서만 문제가 발생하였다.

키 입력이 발생 된 이후 키가 때어지는 과정에서 마지막으로 인식된 키값을 사용하여 최종 출력하면서 생기는 문제인 것 같다.

# 해결 방법

Hyprland 와 zmk 그리고 kitty 터미널을 사용하는 동일한 셋업의 유저중 한명도 같은 문제를 격고 있는것으로 보이고 해당 문제를 해결하기 위해서 kitty 측 Hyprland 측 둘다 노력중인것으로 보인다  

이 과정 중 fcitx 의 설정 값을 통해 해결할 수 있는 방법을 찾았다.
[JeffDess 유저의 해결방법](https://github.com/hyprwm/Hyprland/issues/5815#issuecomment-2087946680)

- 먼저 `waylandim.conf` 이름의 파일을 아래 경로에 만들어 준다

```bash
~/.config/fcitx5/conf/waylandim.conf
```

- 그리고 아래의 문자열을 추가해 준다.

```C 
# Forward key event instead of commiting text if it is not handled
PreferKeyEvent=False
```


